---
name: press-ops
description: "Run a solo media operation with newsroom discipline: source radar for topic discovery, a six-role editorial pipeline with hard quality gates (facts, rights, sentence-level copyedit bound to a body hash), deterministic package validation, and a per-article retro that feeds SOP revisions. Use when producing, auditing, or publishing long-form or short-form content for WeChat Official Accounts, X, or Xiaohongshu."
---

# press-ops

You are operating a small newsroom, not writing a one-off post. Everything runs on two rules:

1. **Discipline is deterministic.** Facts, rights, and sentence-level quality are gates with recorded evidence, not vibes. A package ships only when the validator agrees.
2. **The SOP is open-book and versioned.** Reader comments, platform metrics, and GitHub issues are input signals; every accepted change lands in the CHANGELOG and the next article runs on the new version.

## The loop

Read [references/sop.md](references/sop.md) for the master loop:

signals in (radar + reader feedback) -> topic desk -> evidence base -> per-platform production -> gates -> publish -> retro -> SOP revision.

## Key references

| Concern | File |
|---|---|
| Master loop and state machine | [references/sop.md](references/sop.md) |
| Team roles, workflow, handoff contract | [references/team.md](references/team.md) |
| Source radar method | [references/source-radar.md](references/source-radar.md) (worked example: [source-radar-example.zh.md](references/source-radar-example.zh.md)) |
| Content package spec | [references/content-package.md](references/content-package.md) |
| Fixed editorial gates | [references/editorial-gates.md](references/editorial-gates.md) |
| Human-voice cold read | [references/human-voice-pass.md](references/human-voice-pass.md) |
| AI-pattern diagnostic (Chinese-adapted) | [references/ai-pattern-pass.md](references/ai-pattern-pass.md) |
| Sentence-level copyedit gate (hash-bound) | [references/copyedit-pass.md](references/copyedit-pass.md) |
| Guest audit: cross-model cold review | [references/guest-audit.md](references/guest-audit.md) |
| Research method for writing | [references/writing-research.md](references/writing-research.md) |
| WeChat publishing | [references/platforms/wechat.md](references/platforms/wechat.md) |
| X adaptation | [references/platforms/x.md](references/platforms/x.md) |
| Xiaohongshu adaptation (roadmap) | [references/platforms/xiaohongshu.md](references/platforms/xiaohongshu.md) |

## Tools

- `tools/validate_content_package.py <package>` — deterministic package validation; `--print-copyedit-hash` prints the exact body hash the copyedit gate binds to.
- `tools/wechat_publish.py preview|draft <package> [--execute]` — Wenyan-based render, preview, and WeChat draft creation. Default is a no-network dry run; `--execute` requires explicit per-task user authorization.

## Runtimes

- **Claude Code**: install as a plugin; the roles in `agents/` become subagents and `/press-init` scaffolds a workspace.
- **Codex**: copy `skills/press-ops/` into your project's `.agents/skills/press-ops/`. The skill folder is self-contained; one session role-plays the team per [references/team.md](references/team.md).

## Non-negotiables

- Publication is always a user-controlled external action. Never mark `published` without a real URL or explicit user confirmation.
- Any body edit after a copyedit pass invalidates the hash; re-run the full gate.
- Never fabricate sources, screenshots, or rights status. When in doubt, block and say so.
