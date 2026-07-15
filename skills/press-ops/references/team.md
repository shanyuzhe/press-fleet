# The editorial fleet

A manager-led workflow with eight roles. Keep the team small: specialization is useful only when roles own different decisions or verification surfaces. Six roles produce one article; two roles run the operation around it.

## Production roles

### Managing editor
Own the reader promise, single hook, argument architecture, assignments, and state decisions. Owns `brief.md`, `research/argument-map.md`, frontmatter state after audit, and `publish-record.md` after explicit publication confirmation. Expresses the central claim as a causal chain, maps every major section to `judgment -> evidence -> limitation -> reader consequence`, and keeps `copyedit_checked: false` until the copy editor passes the exact final body. Red line: never edits `draft.md` while the feature writer owns it.

### Evidence editor
Own sources, claim decomposition, factual labels, and the release fact card. Owns `sources.md` and `research/fact-sheet.md`. Converts background and argument evidence into atomic claims labeled fact / vendor self-report / third-party result / inference / commentary; records URL, source type, access date, supported wording, and limitation for each. Starts discovery from the source radar ([source-radar.md](source-radar.md)), then re-verifies each entry for the task date. Red line: reports over-broad wording as `FACT-*` defects; never silently rewrites prose.

### Feature writer
Own the only editable body draft, title candidates, plain-language translation, rhythm, and ending. Sole writer of `draft.md`; other roles report defects without touching the body. Opens with a concrete scene, places the minimum fact card before analysis, translates jargon at first use, and runs the writer self-pass in [human-voice-pass.md](human-voice-pass.md) before handoff. Red line: never introduces unsourced facts and never forks parallel drafts.

### Copy editor
Own sentence-level grammar, syntax, reference, punctuation, terminology, and the exact final body hash. Owns `copyedit.md` and `COPY-*` defects. Runs [copyedit-pass.md](copyedit-pass.md) sentence by sentence on the exact final body only after AI-pattern and cold-read repairs are complete. Red line: a narrow correctness gate, not a second stylist; never marks a partial spot-check as a pass.

### Visual and rights editor
Own publication assets, captions, mobile readability, privacy, and rights status. Owns `asset-manifest.yml` and `assets/`. Registers source, rightsholder, acquisition date, modifications, allowed platforms, and attribution for every asset; previews wide charts at phone width. Red line: never implies commercial authorization, fabricates screenshots, or replaces a factual image with an AI-generated fake of a real event.

### Release auditor
Independently grade the package: run [ai-pattern-pass.md](ai-pattern-pass.md) in detect mode, perform the cold read in [human-voice-pass.md](human-voice-pass.md) without reading the outline first, grade every gate in [editorial-gates.md](editorial-gates.md), run the validator, and recommend pass or repair. Red line: identifies defects but never rewrites the body; a detector score is advisory, never a gate.

## Operation roles

### Radar scout
Own topic discovery and freshness discipline. Maintains the workspace instance of the source radar, sweeps tiered sources on cadence, and files topic candidates with `source_created_at` / `official_announced_at` / `rediscovered_at` explicitly separated. Red line: aggregators may surface a lead, but a candidate is not actionable until the primary source is located; never lets a re-heated old story pose as breaking news.

### Retro coach
Own the feedback loop. After each publication (and monthly), collects reader comments, platform metrics, defect statistics, and GitHub issues; proposes SOP changes with evidence; records accepted changes in the CHANGELOG with a version bump. Red line: every proposal cites signals; no change lands without a written rationale.

## Modes

- **Standard**: all six production roles for a new article or structural rewrite.
- **Research only**: managing editor + evidence editor; stop at `research`.
- **Rewrite**: managing editor + evidence editor for changed claims + feature writer + copy editor + release auditor; add the visual editor when images or captions change.
- **Fast edit**: feature writer + copy editor + release auditor only when structure, claims, sources, and assets are unchanged.

If uncertain, use Standard. Never use Fast to bypass fact, rights, or state gates.

## Workflow

1. The managing editor writes or refreshes `brief.md`: reader blind spot, one-sentence promise, one primary hook, required background, argument map, counterpoint, ending job.
2. The evidence editor and visual editor work in parallel on `sources.md` / fact sheet and the asset inventory.
3. The managing editor locks the brief only after the evidence for the opening fact card and core argument is usable.
4. The feature writer becomes the sole writer of `draft.md`.
5. The evidence editor verifies changed claims; the visual editor verifies final image use. Neither rewrites prose.
6. The release auditor runs the AI-pattern diagnostic in detect mode, reads the package cold, and records `HUMAN-AI-*` and other defects in `review.md`.
7. The feature writer repairs; the evidence editor rechecks changed meaning; the auditor re-runs until no blocking or major defect remains.
8. Only then the copy editor runs the sentence-level gate on the complete exact body and reports `COPY-*` defects; the feature writer repairs; the copy editor re-reads the whole body.
9. The managing editor records the same body hash in `copyedit.md` and draft frontmatter. Any later body edit invalidates this gate.
10. The release auditor confirms hash agreement, runs the validator, and recommends state. At most two targeted repair rounds per gate; repeated material defects become blockers.
11. Publication remains a user-controlled external action.

## File ownership

| File or area | Primary writer | Other roles |
|---|---|---|
| `brief.md`, `research/argument-map.md` | Managing editor | Comment through handoff |
| `sources.md`, `research/fact-sheet.md` | Evidence editor | Read only |
| `draft.md`, `research/title-lab.md` | Feature writer | Defect reports only |
| `copyedit.md` | Copy editor | Feature writer resolves listed defects in `draft.md` |
| `asset-manifest.yml`, `assets/` | Visual and rights editor | Read only |
| `review.md` | Release auditor | Repair owners resolve listed defects |
| frontmatter state, `publish-record.md` | Managing editor | Auditor recommends; user authorizes publication |
| topic candidates, radar instance | Radar scout | Managing editor selects |
| retro records, CHANGELOG proposals | Retro coach | User accepts SOP changes |

Never maintain parallel `draft-v2-agent-name.md` files. One source of truth; defect history lives in `review.md`.

## Handoff contract

End every role run with:

```text
STATUS: pass | needs_fix | blocked
OWNED_FILES:
BLOCKERS:
CHANGED_CLAIMS:
DEFECT_IDS:
HANDOFF_TO:
NEXT_ACTION:
```

Defect prefixes: `LEAD`, `FACT`, `WRITE`, `HUMAN`, `HUMAN-AI`, `COPY`, `VISUAL`, `RELEASE`, `RETRO`. A handoff is not a pass when unknowns are merely omitted.
