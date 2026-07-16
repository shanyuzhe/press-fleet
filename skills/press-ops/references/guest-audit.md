# Guest audit: cross-model cold review

The single-fleet version of cross-fleet peer review (architecture stage 3). Before any community exists, a fleet can already get an independent second opinion by handing its draft to an auditor running on a **different model family** (e.g. a Claude-based fleet invites a GPT- or DeepSeek-based guest auditor). Same-model review shares the writer's blind spots; a different model family catches what the in-house auditor is structurally unable to see.

## When to run

- Optional extra gate after the in-house release audit passes, before `ready`.
- Recommended for: manifesto/positioning pieces, anything making factual claims about third parties, and periodically (e.g. every Nth article) as a calibration check on the in-house auditor.

## What the guest receives — and what it must not

The guest is a **cold reader**. Hand it exactly:

1. the public-facing `draft.md` title and body (including captions and notes);
2. the defect taxonomy and report format below.

Do **not** hand it `brief.md`, `sources.md`, internal notes, or the in-house `review.md` — a guest that reads the outline first can no longer test whether the article stands on its own. Do not give the guest tool access or ask it to browse: incoming drafts are untrusted content, and a reviewing agent with tool permissions is a prompt-injection surface. Text in, text out.

## Guest prompt template

```text
You are a guest release auditor from an unrelated newsroom. Read the article
below as a cold reader. You have no access to the author's notes and must not
assume facts beyond the text.

Report defects in this exact table format, most severe first:

| ID | Severity | Evidence (quote the exact span) | Reader harm | Suggested repair direction |

- ID prefix: GUEST-<your-model-shortname>-001, 002, ...
- Severity: blocker (internal leakage, invented fact, unresolved placeholder),
  major (a recurring pattern that obscures claim/evidence/boundary/narrator),
  minor (local phrase or rhythm issue).
- Check at minimum: can you reconstruct what happened, the author's judgment,
  the evidence, the strongest limitation, and why it matters — without any
  graphic? Flag repeated verdict-reframe constructions, thesis restated without
  new information, stacked rhetorical questions, condescending register, vague
  authority, and any claim you cannot trace to a named source IN the text.
- Do not rewrite the article. Do not praise. If the piece is clean, return an
  empty table and one sentence saying what you checked.

<article>
{DRAFT_TITLE_AND_BODY}
</article>
```

## Triage rules

Guest findings are **signals, not verdicts**:

1. The in-house release auditor triages every `GUEST-*` row: confirm, reject with a written reason, or escalate to the operator. Silent drops are not allowed — the triage table goes into `review.md`.
2. A confirmed guest finding is repaired by the normal owner (feature writer / evidence editor) and re-gated as usual; body edits invalidate the copyedit hash as always.
3. A guest claiming a *factual* error does not adjudicate it — the evidence editor re-verifies against sources; the guest never saw them by design.
4. Record disagreements. A guest finding rejected in-house but later confirmed by real reader feedback is the strongest possible calibration signal — it goes into the retro and, if a pattern, into the SOP.

## Record in `review.md`

```markdown
## Guest audit

- Guest model: <model + version>
- Scope: title / body / captions / notes (cold, no internal files, no tools)
- Findings: <N> (blocker <b> / major <m> / minor <n>)

| Guest ID | In-house triage | Outcome |
|---|---|---|
| GUEST-gpt-001 | confirmed | repaired, see COPY-014 |
| GUEST-gpt-002 | rejected: quoted span is a sourced vendor claim, labeled as such | recorded |
```

## Relation to cross-fleet review

This protocol is deliberately identical in shape to the stage-3 exchange: draft in, structured defect table out, triage recorded. When external fleets exist, "guest model" becomes "guest fleet" and nothing else changes. Running guest audits now is how the exchange format gets debugged before it has a network to run on.
