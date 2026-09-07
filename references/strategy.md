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
3. **TE — two valid paths, pick one and commit:**
   - **(a) Elite TE early — take him when ALL FOUR are true.** This overrides a
     "WR/RB here" row in the plan. Take an elite TE in the early-middle rounds
     only when:
     1. **Elite tier** — a genuine top-1/2 TE with a wide positional-scoring
        edge (a weekly advantage at the league's thinnest starting slot), *and*
     2. **He fell to ~his ADP or below** — you are paying market price, not
        reaching. (Within a pick or two of his Sleeper ADP counts; a real
        discount is a green light.) *and*
     3. **A scarcity cliff sits right behind him** — the next TE tier is many
        picks away, so passing means a big drop in quality, *and*
     4. **Your premium anchors are already secured** — you have your RB1 and
        WR1 (or equivalent core), so the depth cost is affordable.
     When all four line up, take the TE even though the row says a different
     position — an elite TE at a cliff is a season-long structural edge.
     *(Worked example: a manager took McBride at pick 26 — his ADP was ~28, the
     next TE went at 52, and he already had his R1 RB + R2 WR. Textbook (a).)*
   - **(b) Wait and stream.** If any of the four is missing, don't force it: take
     one from your TE tier before that tier empties, then stop — or punt and grab
     two dart throws late.
   - **What to actually avoid** is reaching for a *middling* TE in the dead zone
     (a name with no positional edge, a round early, just to "have your TE").
     That's the trap — not taking an elite one early.
4. **Rounds 8–12: upside and value.** Every pick now is a bench slot, and a bench
   player only helps if he breaks into your lineup or becomes a trade chip. **Floor
   does neither — draft upside, and value only when the room hands it to you.**
5. **Late-round RBs: ceiling first.** Use these picks on backs with a path to a
   real role — upside that can break into your lineup or become a trade chip.
   Handcuffing is a minor, situational move: worth *one* pick only as insurance
   for your own early RB stud, and only if that backup would truly start if the
   stud went down. If he wouldn't (special-teamer, buried, on IR), take a ceiling
   RB instead. Never draft another manager's handcuff.
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
