# Draft strategy playbook (half-PPR, generalizable)

Use this to *build* a plan file when none exists, and as background. Once a plan
file exists, take round-by-round orders from the plan, not from here.

## Scoring: confirm it first, then adjust the whole board

**Before ranking anyone, confirm the league's scoring with the user** — ask
"full PPR, half PPR, or standard?" and check it against `scoring_settings.rec`
(1.0 = full, 0.5 = half, 0 = standard). Scoring reshapes the entire draft, so
never assume it, and pull the matching ADP/projection feed to match.

- **Full PPR (`rec` = 1.0):** receptions are king — a point per catch.
  - **Push up:** high-volume slot/possession WRs, pass-catching / third-down RBs
    (a back with 60+ catches can out-score a bigger-name early-down grinder),
    and target-hog TEs (a clear top TE is worth reaching for a round earlier
    than in half-PPR).
  - **Fade:** TD-dependent, low-catch WRs and committee/early-down-only RBs whose
    value is all yardage and touchdowns.
  - **Practical effect:** WR depth is deeper and more valuable, so it's easier to
    wait on RB2/RB3 and load WRs; a receiving RB is a legit RB1/2, not just a flex.
- **Half PPR (`rec` = 0.5):** receptions still help, but yardage and TDs matter
  more, and workhorse RBs gain relative value. Prioritize target/carry *volume*
  and goal-line/red-zone role over pure catch count.
- **Standard (`rec` = 0):** RBs and TD-dependent players rise further;
  de-emphasize catches; pure slot WRs drop.

## Core shape of a good draft

1. **Rounds 1–7: RB and WR only.** This is where startable backs and receivers
   are available. Build your 2 RB / 2 RB + FLEX and 2–3 WR core here. Don't spend
   these picks on QB/TE/K/DEF unless an elite one falls to a real discount.
2. **QB:** either (a) land one elite target *at a discount* — a QB with a rushing
   floor is worth a small reach because the floor is real points — or (b) stream:
   draft two mid/late QBs on **offset bye weeks** and start the better matchup each
   week. Never pay a mid-round price for a pocket passer with no rushing upside.
3. **TE:** take one from your tier before the tier empties, then stop. If you miss
   the elite tier, wait and take two dart throws late — don't reach a round early.
4. **Rounds 8–12: upside and value.** Every pick now is a bench slot, and a bench
   player only helps if he breaks into your lineup or becomes a trade chip. **Floor
   does neither — draft upside, and value only when the room hands it to you.**
5. **Handcuff:** at most one, late, and only insurance for *your own* early RB
   stud. Don't draft other managers' handcuffs. If your stud has no viable
   handcuff (backup is a special-teamer or on IR), spend the pick on a ceiling RB
   instead.
6. **K and DEF: last two picks.** Stream both in-season off free agency.

## Byes

Ignore bye weeks until the middle rounds. From then on, use bye only as a
**tiebreaker** between close options — never to jump tiers. Watch for a **bye
cluster** (several starters off the same week) and avoid stacking a third.

## VALUE / REACH flags

- **VALUE:** a player whose expert-consensus rank is meaningfully better than his
  ADP in this room. Wins ties inside a tier. Veterans with secure roles are often
  VALUEs in the rounds where the room chases rookies.
- **REACH:** a player going well ahead of his ECR in this room. Never take him at
  the room's price — let someone else.

## Reading the room

If you have a prior-season draft from the same league, pull it and note:
- Which positions this room takes early vs. late (many rooms take TE and QB a
  round or two earlier than ADP; some ignore QB entirely for 30+ picks).
- Who the active managers are and which ones actually trade.

Order the two picks in a back-to-back "turn" by what the managers picking between
them are likely to grab: take the position they're *more* likely to steal first.

## In-season routine template (save after the draft)

The draft is a fraction of the season. Activity wins leagues. Save a per-league
in-season file with:

- **Waiver strategy.** Know the format: **rolling priority** (a one-shot resource —
  spend it only on a true difference-maker, then you drop to the back) vs **FAAB**
  (budget your bids). Most weekly moves should come from the **free-agent pool**
  (no priority/budget cost) the day after waivers clear.
- **Weekly routine:**
  - *Tuesday AM:* check every starter's status + next week's byes; submit only
    high-value waiver claims.
  - *Wednesday:* confirm claims; work the free-agent pool for streamers and
    upside; drop your worst bench player (never a handcuff to your own stud).
  - *Saturday night:* set the lineup by projection — no gut starts.
  - *Sunday ~90 min before kickoff:* check inactives for every questionable
    starter; never leave an OUT player in the lineup.
- **Sell-high window (weeks 3–6):** trade breakouts to the managers who actually
  trade, before regression. Cut obvious busts by ~week 5.
- **Watch list:** injuries to monitor, committee backfields, IR stashes to claim
  on activation, boom-bust players who are trade-chip candidates if they pop.
