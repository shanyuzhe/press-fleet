# Source radar

The radar is how the fleet discovers topics before they are re-heated by aggregators, and how it keeps "latest" claims honest. Method here; a real maintained instance is in [source-radar-example.zh.md](source-radar-example.zh.md).

## Principles

- Discovery may rely on aggregators; a filed story must return to the primary material.
- Entry points migrate. Re-verify the radar instance quarterly.
- The radar proves where information *can* come from; it never substitutes for per-task verification at `as_of`.

## Source tiers

| Tier | What it is | What it can prove |
|---|---|---|
| **P0** | Primary fact sources: company newsrooms, release pages, docs and changelogs, papers, model/system cards, official repos and weights, pricing/quota/status pages, first-party posts and filings, regulator originals | What someone published or claimed — not that it works |
| **P1** | Independent verification: evaluations and research bodies with public method, version, and limitations | Calibration against vendor claims; never quote a leaderboard rank alone |
| **P2** | Credible reporting and analysis | People, funding, org, supply-chain background; keep media attribution for exclusives and seek second confirmation |
| **P3** | Lead radar: X, Reddit, HN, Xiaohongshu, Bilibili, Product Hunt, GitHub Trending | That someone posted or is discussing — not motive, truth, or prevalence |

## Freshness discipline

Every candidate records three timestamps, converted to one declared timezone:

| Field | Meaning | May enter the "latest" window? |
|---|---|---|
| `source_created_at` | When the paper, code, file, or event actually appeared | Yes |
| `official_announced_at` | First official announcement | Yes |
| `rediscovered_at` | When media or a community re-heated it | Only as "re-surfaced", never as news |

Rules:

- Priority windows: last 4h -> 12h -> 24h -> 72h. A page showing only a date, not a time, cannot claim an hour-level window.
- Batch-refreshed listings (e.g. arXiv after a weekend) date from the item's own submission history, not the listing refresh.
- When old material re-enters discussion, the article states both the original time and the current wave.

## Maintaining an instance

Build your own instance as a table per beat: institution, stable entry URLs, what to watch, sweep cadence (daily / weekly / release-window). Review quarterly: dead links out, migrated entries updated, new beats added. The example instance covers the AI/model beat in Chinese; fork it for your own domain.
