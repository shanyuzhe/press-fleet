# Xiaohongshu adaptation (roadmap)

Status in v0.1: **design only.** Nothing here is battle-tested yet; this file states the contract the v0.3 implementation must satisfy, so early adopters know what is coming and what is deliberately excluded.

## Reader contract

Xiaohongshu is card-first: the cover card decides whether anyone reads, and cards carry the argument while the caption carries the voice. Long prose does not transfer.

## Planned pipeline

1. **Card generation from the evidence base.** Each card is one claim from the fact sheet rendered as a phone-readable graphic (deterministic templates, not per-card freehand design). Card text follows the same fact labels as prose.
2. **Caption** is a fresh rewrite (voice contract applies), not the WeChat opening pasted in.
3. **Gates**: rights manifest covers every card asset (`allowed_platforms` includes `xiaohongshu`); the copyedit gate applies to card text and caption; phone-width readability is a blocking check.
4. **Publishing is manual by design.** Xiaohongshu offers no official posting API for this use case; the adapter will stop at "export a ready-to-post bundle" (cards + caption + tags) and never automate login or posting through unofficial means.

## Explicitly out of scope

- Unofficial automation of posting, login, or engagement — account-risk and ToS-risk are not worth it.
- Engagement-bait card formulas. The radar's freshness discipline and the voice contract apply on every platform, including this one.
