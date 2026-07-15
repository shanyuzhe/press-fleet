# Contributing = sending signals

press-fleet runs on feedback signals. There are three ways in, all welcome:

## 1. Reader signals (no GitHub needed)

Comment on the articles produced by this SOP. Comments that name a concrete problem ("this read like AI", "the chart is unreadable on my phone", "you called a filing a launch") are treated as defect reports and enter the retro loop. The CHANGELOG records which comments changed the system.

## 2. Issues

Open an issue for anything in the SOP that is wrong, vague, or missing. Strong issues name:

- the file (e.g. `skills/press-ops/references/copyedit-pass.md`),
- the observed problem (with an example if you ran the SOP yourself),
- optionally a proposed fix.

If you run press-fleet on your own account, your escaped defects are the most valuable signal we can get — file them with the defect taxonomy (`FACT-*`, `HUMAN-AI-*`, `COPY-*`, `VISUAL-*`, `RELEASE-*`) if you can.

## 3. Pull requests

PRs to references, templates, tools, and docs are welcome. Rules:

- One concern per PR; state the signal that motivated it (an issue, a retro record, a real failure).
- Changes to gates must keep them deterministic where they are deterministic today — no replacing recorded evidence with model vibes.
- English or Chinese are both fine; keep each document in its existing language.
- Tool changes keep the two-step safety design: dry-run by default, external effects behind an explicit flag.

## What gets accepted

Every accepted change needs a cited signal and lands in the CHANGELOG with rationale and a version bump. "It feels better" is not a signal; "this gate blocked three false positives in a row" is.

## Roadmap participation

The three-stage roadmap is in [docs/architecture.md](docs/architecture.md). Stage 3 (cross-fleet peer review — fleets auditing each other's packages with the shared defect taxonomy) activates only when real external fleets exist. If you are running one, say hello in an issue: you are the trigger condition.
