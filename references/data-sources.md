# Data sources (no login required)

All of these work without authentication from a normal machine. Use them to
build the plan file and to fill gaps live. Replace `<YYYY>` with the season and
adjust the scoring path (`half-ppr`, `ppr`, `standard`) to match the league.

## Sleeper API (draft board, rosters, players)

Base: `https://api.sleeper.app/v1`

- **League → drafts:** `/league/<LEAGUE_ID>/drafts` (newest = current season)
- **Draft meta / slots:** `/draft/<DRAFT_ID>` → `draft_order` (user_id → slot),
  `settings`, `type`.
- **Live picks:** `/draft/<DRAFT_ID>/picks` → array; length = picks made. Each has
  `pick_no`, `round`, `draft_slot`, `picked_by`, `metadata.{first_name,last_name,position,team}`.
- **League settings:** `/league/<LEAGUE_ID>` → `roster_positions`,
  `settings.num_teams`, `scoring_settings` (`rec`: 1=PPR, 0.5=half, 0=standard).
- **User lookup:** `/user/<USERNAME>` → `user_id`.
- **Player master (big, ~5MB):** `/players/nfl` → per-player `depth_chart_order`,
  `injury_status`, `status`, `team`, `position`. This is how you catch a starter
  who's quietly on IR. Cache it; don't refetch during a live draft.
- **Prior-year picks per owner** (to model how a room drafts):
  `/league/<PREV_LEAGUE_ID>/drafts` → `/draft/<PREV_DRAFT_ID>/picks`.

## Projections (exact points)

- **Sleeper season projections (preferred, exact):**
  `https://api.sleeper.com/projections/nfl/<YYYY>?season_type=regular&position[]=QB&position[]=RB&position[]=WR&position[]=TE&order_by=pts_half_ppr`
  — note the `.com` host (not `.app`). Each entry: `player` + `stats.pts_half_ppr`
  (or `pts_ppr` / `pts_std`).
- **ESPN projections (backup):**
  `https://lm-api-reads.fantasy.espn.com/apis/v3/games/ffl/seasons/<YYYY>/segments/0/leaguedefaults/3?view=kona_player_info`
  with header `X-Fantasy-Filter: {"players":{"limit":150}}`.
  half-PPR points = PPR `appliedTotal` − 0.5 × receptions.

## ADP (what the room will actually do)

- **Sleeper-specific ADP** (real Sleeper drafts — best when the league is on
  Sleeper): `https://yafsb.com/fantasy-football/adp-rankings/half-ppr/` via
  WebFetch. Swap `half-ppr` for `ppr`/`standard` as needed. ~180 players with
  pick-number ADP. **Treat this as truth for what a Sleeper room will do.**
- **FantasyFootballCalculator JSON (has stdev + byes):**
  `https://fantasyfootballcalculator.com/api/v1/adp/half-ppr?teams=12&year=<YYYY>`
  — plain curl, no auth. Change `teams` to the league size.

## Expert consensus (VALUE / REACH flags)

- **FantasyPros ECR:** WebFetch tends to drop the table. Instead `curl` the
  half-PPR cheatsheet page raw and parse the inline `var ecrData = {...}` JSON —
  900+ players with `rank_ecr`, `tier`, `pos_rank`, `rank_std`.
- DraftSharks is paywalled — skip.

## How to combine them (the three-number system)

In the plan's tiers, show each player as **(SLP ADP / FFC ADP / ECR rank)**:
- **SLP** = real Sleeper ADP — primary; what this room will actually do.
- **FFC** = FantasyFootballCalculator mock ADP — sanity check + stdev + bye.
- **ECR** = expert-consensus rank — drives the VALUE / REACH flags. A player whose
  ECR rank is well *above* (better than) his ADP is a VALUE; one going well
  *earlier* than his ECR in this room is a REACH.

Rule of thumb for "will he be there at my pick P":
`SLP ADP ≥ P + 8` → probably there · within ±5 → coin flip · `≤ P − 5` → gone.

For non-Sleeper leagues, lean on FFC ADP + ECR and skip the yafsb source.
