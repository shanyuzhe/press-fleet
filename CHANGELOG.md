# Changelog

All SOP and framework changes land here with rationale. Articles cite the version that produced them (`本篇由 press-fleet SOP vX.Y 生产`).

## v0.1.3 — 2026-07-16

Adoption blockers and the peer-review MVP.

- **tools/wechat_publish.py is now workspace-independent.** Signal: the tool was extracted from a private workspace and still resolved the validator via a hardcoded `.agents/skills/...` path, assumed a `微信公众号/` directory layout, and shelled a Windows-only `wenyan.cmd` — a fresh clone could not run it at all. Now: validator resolves next to the tool; the platform root (Wenyan install, `.env`, runtime cache) is discovered by walking up from the content package, with a `PRESS_PLATFORM_ROOT` override; the Wenyan binary name is cross-platform. Both the missing-install error path and a full preview render were tested against the demo package from a clean clone layout.
- **.env.example** shipped at the repo root; the WeChat platform reference rewritten for the generic setup (npm + PyYAML + platform-root layout).
- **references/guest-audit.md**: the cross-model guest audit protocol — the single-fleet version of stage-3 cross-fleet peer review. A cold reviewer from a different model family gets the draft only (no notes, no tools — untrusted-content discipline), reports `GUEST-*` defects in the shared taxonomy, and every finding gets a recorded in-house triage. Same exchange shape as the future fleet network, debuggable today.

## v0.1.2 — 2026-07-16

Positioning grounded in a sourced investigation of the existing self-media SOP ecosystem (signal: operator-directed competitive research, 2026-07-16).

- **docs/why.md**: the problem statement, fully sourced — SOPs as unenforceable documents (81% adoption / 13% policy), the bare quality floor (real penalty cases: administrative detention, a 2.6M CNY defamation judgment, copyright troll settlements), and the post-crackdown "AI-score laundering" gray industry that fights detectors instead of fixing content.
- **README repositioned**: leads with the April 2026 platform crackdown and the anti-score-laundering stance ("instead of hiding the AI, make the production process auditable"); states the deliberate battleground — Claude Code and Codex, AI-native creators, no web-tool version.
- **Boundaries made explicit**: no virality guarantees, no score laundering ever, full pipeline is intentionally heavier than "just post it".

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
