# Sleeper Draft Co-Pilot

A [Claude Code](https://claude.com/claude-code) **skill** that turns Claude into a
live fantasy football draft co-pilot for drafts run on [Sleeper](https://sleeper.com).

When you're on the clock, it reads the live draft board over Sleeper's **public,
read-only API** (no login, no password, no browser automation), tracks who's
gone, and recommends your pick in seconds against a tier sheet built for your
league. It also helps you prep before the draft and set up an in-season routine
after it.

Works for **any Sleeper league, any draft slot, any season, any scoring** — you
plug in your own league; nothing is hard-coded.

## What it does

- **Setup:** give it your Sleeper league URL and username. It finds your draft,
  reads your roster settings and scoring, confirms your draft slot, and works out
  your snake-turn pick numbers.
- **Build a plan:** pulls live ADP, projections, and injury status from free
  sources and builds a turn-by-turn tier sheet ("Round 2: take one of these RBs,
  in this order").
- **On the clock:** say *"my pick"* and it crosses off drafted players, checks
  your roster needs, and gives one fast recommendation with backups and a queue.
- **Live monitoring:** ask it to watch the board and it flags position runs and
  when players in your plan get taken.
- **After the draft:** saves your roster plus a waiver / weekly-lineup routine.

## Install

Copy the skill into your Claude Code skills directory:

```bash
git clone https://github.com/brandonchastain/sleeper-draft-copilot.git
mkdir -p ~/.claude/skills/sleeper-draft-copilot
cp -r sleeper-draft-copilot/SKILL.md sleeper-draft-copilot/references ~/.claude/skills/sleeper-draft-copilot/
```

On Windows (PowerShell):

```powershell
git clone https://github.com/brandonchastain/sleeper-draft-copilot.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills\sleeper-draft-copilot"
Copy-Item sleeper-draft-copilot\SKILL.md,sleeper-draft-copilot\references -Destination "$env:USERPROFILE\.claude\skills\sleeper-draft-copilot\" -Recurse
```

Then restart Claude Code (or start a new session) so it picks up the skill.

## Use

**A day or two before your draft:**

> Set up my Sleeper draft. League: https://sleeper.com/leagues/XXXXXXXX  — my username is yourname.

It walks setup and builds your plan file. Review the pre-made decisions
(elite QB target, when to take TE, handcuff plan) and tweak to taste.

**On draft day, when you're on the clock:**

> my pick

You'll get something like:

> **Take: Player Name (RB, TEAM)** — best back left in your tier, fills RB2.
> Then at your next pick: Other Player (backup: Third Player).
> Queue for the next turn: Name, Name, Name, Name.

## How it works

Everything runs off Sleeper's public API (`api.sleeper.app` / `api.sleeper.com`)
plus a few free ADP/projection/ranking sources — see
[`references/data-sources.md`](references/data-sources.md). No authentication is
ever required, and the skill only *reads* the draft; it never makes your picks
for you (you stay in control in the Sleeper app).

- [`SKILL.md`](SKILL.md) — the skill itself (the board-reading loop + how it talks).
- [`references/strategy.md`](references/strategy.md) — the half-PPR strategy playbook.
- [`references/data-sources.md`](references/data-sources.md) — the free data endpoints.
- [`references/plan-template.md`](references/plan-template.md) — the blank tier sheet.

## License

MIT — see [LICENSE](LICENSE).

---

*Not affiliated with Sleeper. Uses only Sleeper's public, read-only API.*
