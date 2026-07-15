# The master loop

press-fleet runs one loop, open-book and versioned. Every published article states which SOP version produced it; every reader signal can change the next version.

```text
          ┌────────────── signals in ──────────────┐
          │  source radar (P0-P3 tiers, freshness) │
          │  reader comments / platform metrics    │
          │  GitHub issues on the public SOP       │
          └───────────────────┬─────────────────────┘
                              ▼
                      1. topic desk
              candidates -> selection record
                              ▼
                      2. evidence base
        platform-agnostic sources.md + fact sheet
                              ▼
              3. per-platform production
     ┌──────────────────┬──────────────────┬───────────────┐
     │ WeChat long-form │ X posts/threads  │ XHS cards     │
     │ six-role pipeline│ rewrite from the │ (roadmap)     │
     │                  │ fact base, never │               │
     │                  │ compress the     │               │
     │                  │ article          │               │
     └────────┬─────────┴────────┬─────────┴───────┬───────┘
              ▼                  ▼                 ▼
                      4. gates (per platform)
        facts / rights / voice / AI-pattern / copyedit-hash
                              ▼
                      5. publish (user-authorized)
                              ▼
                      6. retro
        metrics + comments + defects -> change proposals
                              ▼
                      7. SOP revision
        CHANGELOG + version bump -> next article runs on it
```

## Stage contracts

1. **Topic desk.** Every candidate records its three timestamps (`source_created_at`, `official_announced_at`, `rediscovered_at`) and its radar tier. Selection is a written judgment: reader, promise, and why now. Rejected candidates stay on file — they are cheap future leads.
2. **Evidence base.** One research effort feeds all platforms. Claims are atomic and labeled (fact / vendor self-report / third-party / inference / commentary). See [writing-research.md](writing-research.md).
3. **Per-platform production.** Each platform is a rewrite from the evidence base with its own reader contract, not a compression of another platform's output. Platform specifics live in [platforms/](platforms/).
4. **Gates.** Fixed gates in [editorial-gates.md](editorial-gates.md); the sentence-level gate binds a SHA-256 of the exact final body ([copyedit-pass.md](copyedit-pass.md)); the deterministic validator (`tools/validate_content_package.py`) must report zero errors. Model judgment is advisory; recorded evidence decides.
5. **Publish.** Always a user-controlled external action, per platform adapter.
6. **Retro.** Within a week of publication the retro coach fills `templates/retro.md`: what the signals said, what defects escaped, what the SOP should change.
7. **SOP revision.** Accepted changes land in the CHANGELOG with a semver bump and rationale. The article footer convention `本篇由 press-fleet SOP vX.Y 生产` makes the version reader-visible.

## State machine

Content package states: `idea -> research -> draft -> fact_checked -> editorial_review -> ready -> published -> archived`. Transition rules live in [content-package.md](content-package.md). `ready` requires `fact_checked`, `rights_checked`, `copyedit_checked` all true and a current body hash; `published` requires a real URL or explicit user confirmation.

## What is public, what is private

Open-book applies to the system, not to unfinished work or credentials:

- **Public**: the SOP, roles, gates, templates, tools, radar method, retro summaries, CHANGELOG.
- **Private**: unpublished drafts and research notes, platform credentials (`.env`), personal commercial strategy, raw reader data. Publish aggregates, never individual reader information.
