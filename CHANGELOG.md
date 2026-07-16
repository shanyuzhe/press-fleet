# Changelog

All SOP and framework changes land here with rationale. Articles cite the version that produced them (`本篇由 press-fleet SOP vX.Y 生产`).

## v0.1.1 — 2026-07-16

Two SOP changes, each triggered by a real editorial round; plus onboarding and CI.

- **ai-pattern-pass, group 3: verdict-reframe reuse.** Signal: a filed article passed all gates, then user review found the construction "比 X 更要紧的是 Y" used four times across one piece (2026-07-15, Apple filing article, defects HUMAN-AI-005~009). One reframe is a stance; four is a tic. Now an explicit symptom.
- **ai-pattern-pass, group 3: the argument treadmill.** Signal: a second article restated its core thesis five times — opening, section endings, an image caption, and the closing — with near-identical wording (2026-07-16, GPT-Red article, defects HUMAN-AI-006~008). Neither the cold read nor the sentence gate catches cross-position repetition. New rule: every return to the thesis must carry a new fact, boundary, or consequence; captions must add information the prose does not state. Recorded as lesson 8 in docs/lessons.md.
- **examples/demo-package**: a minimal complete content package that passes the validator, with a hands-on "edit one character, watch the hash gate fail" experiment. Doubles as the CI fixture.
- **CI**: GitHub Actions runs the validator against the demo package on every push and PR — the spec, the validator, and the hash gate must always agree.

## v0.1.0 — 2026-07-15

Initial open-book release. Extracted from a private WeChat operation that ran this system through 8 content packages in July 2026.

- Six production roles + two operation roles (radar scout, retro coach) with red lines and a handoff contract.
- Fixed editorial gates; Chinese-adapted AI-pattern diagnostic; human-voice cold read; sentence-level copyedit gate bound to a body SHA-256.
- Content package spec with a deterministic validator.
- Source radar method (P0-P3 tiers, three-timestamp freshness) with a maintained Chinese AI-beat example.
- WeChat publishing adapter (Wenyan-based; dry-run by default, `--execute` user-gated).
- Dual runtime: Claude Code plugin (agents + `/press-init` + skill) and Codex (self-contained skill folder).
- Docs: architecture with a three-stage roadmap (traffic -> tooling/multi-platform -> gated fleet-network community), philosophy, eight lessons from live operation.
- Honest boundaries: X tooling and Xiaohongshu pipeline are roadmap, not features.
