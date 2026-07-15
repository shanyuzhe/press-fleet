# Changelog

All SOP and framework changes land here with rationale. Articles cite the version that produced them (`本篇由 press-fleet SOP vX.Y 生产`).

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
