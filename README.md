# press-fleet

**An open-book AI editorial fleet for solo media operators.** The entire SOP that runs the account is public, versioned, and iterated on reader feedback.

[中文说明（主文档）](README.zh-CN.md) · [Architecture](docs/architecture.md) · [Philosophy](docs/philosophy.md) · [Lessons](docs/lessons.md) · [Changelog](CHANGELOG.md)

Sibling project of [research-fleet](https://github.com/shanyuzhe/research-fleet): research-fleet staffs a research project with an AI team that doesn't cut corners; press-fleet staffs a media operation with an AI newsroom that doesn't cut corners on readers.

## What it does

Signals in (tiered source radar + reader feedback) → topic desk → platform-agnostic evidence base → a six-role editorial pipeline → deterministic quality gates → user-authorized publishing → retro → a versioned SOP revision. Every published article cites the SOP version that produced it.

Mechanisms worth stealing even if you never install it:

- **Roles with red lines** — the auditor can't rewrite, the writer can't invent facts, the copy editor can't restyle. Eight roles, one handoff contract.
- **Hash-bound copyedit gate** — the sentence-level pass binds to a SHA-256 of the exact body; any later edit voids it. A zero-dependency validator enforces agreement between the draft, the copyedit record, and the actual bytes.
- **Chinese-adapted AI-pattern diagnostic** — English word lists and stylometric thresholds are explicitly *not* gates for Chinese copy; the diagnostic targets real symptoms (repeated verdict-reframe constructions, stacked rhetorical questions, condescending register).
- **Feedback as versioned changes** — comments, metrics, and issues become CHANGELOG entries with cited signals. See [lessons.md](docs/lessons.md) for the real failures that produced the current rules — the list grows with every retro.

Start with [`examples/demo-package/`](examples/demo-package/) — a minimal complete content package that passes the validator. Edit one character of its body, re-run the validator, and watch the hash gate fail.

## Runtimes

- **Claude Code**: install as a plugin — 8 subagents (`agents/`), a `/press-init` workspace scaffold, and the `press-ops` skill.
- **Codex**: `skills/press-ops/` is self-contained; copy it into `.agents/skills/` and one session role-plays the team.

Platform support in v0.1: WeChat Official Accounts end-to-end (Wenyan-based render/preview/draft tool, dry-run by default); X methodology (tooling in v0.2); Xiaohongshu design contract (v0.3).

## License

MIT
