---
name: sleeper-draft-copilot
description: >
  Live fantasy football draft co-pilot driven by the public Sleeper API. Use
  whenever the user is drafting on Sleeper and wants pick recommendations —
  triggers on "my pick", "who's up", "who should I take", "I'm on the clock",
  or any point during a live Sleeper draft. Reads the live draft board over
  Sleeper's public read-only API (no login needed), tracks who's gone, and
  recommends the pick against the user's tier sheet and strategy. Also use to
  set up before a draft (find the draft_id, confirm the user's slot and roster
  settings) and to build or update the tier sheet from live ADP.
---

# Sleeper Draft Co-Pilot

A live draft co-pilot for fantasy football drafts run on Sleeper. When the user
is on the clock, read the current Sleeper draft board, figure out who's still
available, and recommend a pick fast — there is usually a pick clock running.

Works for **any Sleeper league, any draft slot, any season**. Nothing about a
specific league is hard-coded in this file. The first time it's used, run
**Setup** to learn the user's league, slot, roster settings, and turn structure,
and to build their plan file.

## The plan file is the authority

Each league/season gets one plan file, e.g. `draft_plan_<season>.md` in the
user's working directory. **That file is the single source of truth** — the
turn-by-turn plan, pre-made decisions, tiers, injury/suspension flags, the
handcuff map, and bye rules. Read it in full before the first recommendation.
Where anything in this skill and the plan disagree, **the plan wins**. This
skill only says how to read the board, how to build the plan, and how to talk.

`references/strategy.md` is the generic half-PPR strategy playbook (RB/WR
priority, QB streaming, TE tiers, handcuffs, byes, VALUE/REACH). Use it to
*build* a plan when none exists, and as background — don't take round-by-round
orders from it once a plan file exists.

`references/data-sources.md` lists the ADP / projection / injury endpoints that
work with no login. `references/plan-template.md` is the blank tier-sheet the
plan file is built from.

## Setup (before the draft) — run this once per season

Ask the user for their Sleeper league URL or league ID, and their Sleeper
username, then:

1. **Find the draft_id:**
   `https://api.sleeper.app/v1/league/<LEAGUE_ID>/drafts` → newest draft's `draft_id`.
2. **Read league settings:**
   `https://api.sleeper.app/v1/league/<LEAGUE_ID>` → `roster_positions` (the
   exact starting lineup + bench), `settings.num_teams`, and `scoring_settings`
   (`rec` = 1.0 full PPR, 0.5 half PPR, 0 standard). Confirm scoring with the user.
3. **Find the user's slot:**
   `https://api.sleeper.app/v1/user/<USERNAME>` → `user_id`, then
   `https://api.sleeper.app/v1/draft/<DRAFT_ID>` → `draft_order` maps `user_id` →
   slot (1..num_teams). **Cross-check with the user; never recommend for the
   wrong seat.** Slots can change year to year — confirm every season.
4. **Work out the turn structure for their slot** (see *Snake turn math* below)
   and tell the user which picks are back-to-back "turns."
5. **Build the plan file** if one doesn't exist for this season: pull ADP and
   projections from `references/data-sources.md`, follow the method in
   `references/strategy.md`, and fill in `references/plan-template.md`. Confirm
   the big pre-made decisions (elite QB target, when to take TE, handcuff plan)
   with the user before draft day.

## Snake turn math (works for any slot)

In a snake draft of `N` teams, the user at slot `s` picks at:
`s`, then `2N-s+1`, `2N+s`, `4N-s+1`, `4N+s`, ... (round `r` pick number is
`(r-1)*N + s` on odd rounds and `r*N - s + 1` on even rounds).

- **Slots near the turn (1–2 or N-1..N) pick nearly back-to-back** across the
  round boundary — plan those two picks as one "best two on the board," and
  order the pair by what the manager(s) picking between them are likely to take.
- **Middle slots pick evenly spaced** — simpler, one pick at a time, but never
  get the elite falling-player gifts the turn slots get.
- The long gap (from an odd-round pick to the next even-round pick) is the only
  real danger window — about `2N-2` picks pass. That's where runs happen.

Tell the user their actual pick numbers for the season so they think in turns.

## On the clock — the core loop

When the user says "my pick" (or similar):

1. **Fetch drafted players:**
   `https://api.sleeper.app/v1/draft/<DRAFT_ID>/picks`
   Each entry has `pick_no`, `round`, `draft_slot`, `picked_by`, and
   `metadata.{first_name,last_name,position,team}`. Array length = picks so far,
   so the next pick number is `len + 1`.
2. **Cross off drafted players** against the plan's tiers. Track the user's own
   roster (their `draft_slot`) so you fill real needs, and glance at the rosters
   of whoever picks before their next turn — it decides pick order in a pair.
3. **Find the current turn in the plan** and recommend from its lists, in the
   plan's stated order, honoring the pre-made decisions.
4. **Talk in ROUND numbers**, not raw pick numbers. "Your Round 2 pick," never
   "pick 23." Do the conversion for the user.
5. **Recommend in this exact format** so the user can act in seconds:

   > **Take: [Player] (POS, TEAM)** — [one-line why].
   > Then at your next pick: [Player] (backup: [Player]).
   > Queue for the next turn: [3–4 names].

6. Keep it to that. No essays while the clock runs.

## Live monitoring between picks

The user can ask you to watch the board. Re-fetch `/picks` on request (or on a
short interval if asked) and flag:
- A **position run** (3+ of one position gone since their last turn) that threatens
  their plan for the upcoming turn.
- Any **player in their plan's next-turn list** getting taken — update the queue.
- When they are **~2 picks away**, proactively surface the recommendation so
  they're ready when the clock hits them.

Sleeper's API is public and read-only, so polling `/picks` is the whole
mechanism — no login, no browser, no websocket needed.

## General rules (the plan overrides all of these)

These are sane defaults for building a plan and for filling gaps live. The
plan file's specific calls always win.

- **RB/WR first.** The best chances to land startable RB and WR are rounds 1–7.
  Don't spend an early pick on QB/TE/K/DEF unless the plan says so.
- **QB:** in a 1-QB league, either land one elite target at a real discount or
  stream two mid/late QBs on offset bye weeks. Never pay a mid-round price for a
  pocket passer with no rushing floor. (See the streaming path in the plan.)
- **TE:** take one from your tier before it empties, then stop. Don't reach a
  round early for a name; don't chase a second TE.
- **Handcuffs:** at most one insurance handcuff, and only for your own early-round
  RB stud, late. Don't draft other managers' handcuffs.
- **Byes:** ignore until the middle rounds; from then on use bye week only as a
  tiebreaker between close options, never to jump tiers.
- **VALUE / REACH:** a player flagged VALUE (falling below expert rank) wins ties
  inside a tier; a REACH (going well above rank in this room) is never taken at
  the room's price.
- **K and DEF:** last two picks only. Stream both in-season.

## After the draft

Save the final roster and an in-season routine to the user's working directory
(waiver strategy, weekly lineup routine, bye clusters, injury watch list) so next
season's setup is faster. See `references/strategy.md` for the in-season template.

## Notes

- Prefer the Sleeper API over reading the draft room in a browser — it's public,
  read-only, and faster.
- Player-name spellings in a user's notes are sometimes garbled; match on intent
  (e.g. "Devan Echan" = De'Von Achane).
- All endpoints and their quirks are in `references/data-sources.md`.
