# X adaptation

Status in v0.1: **method stable, tooling partial.** The rewrite rules below are battle-tested; API posting tools are not yet bundled.

## Reader contract

X readers give you one screen and no patience. A post earns its length with one concrete fact, one judgment, or one artifact (chart, screenshot, table). Threads exist for evidence chains that genuinely need steps, not for chopping an article into slices.

## Rules

1. **Rewrite, never compress.** Posts are written fresh from the evidence base (`sources.md` + fact sheet), not condensed from the WeChat article. A compressed long-form article reads like a press release stump on X.
2. Default package: 3 independent single posts + 1 short thread per topic, each with its own hook and standalone value.
3. Facts keep their labels: a vendor claim is quoted as a claim; independent numbers cite the evaluator. The evidence editor verifies X copy against the same fact sheet as long-form.
4. Images follow the same rights manifest as the long-form package (`asset-manifest.yml`, `allowed_platforms` must include `x`).
5. Time claims follow radar freshness discipline — never present a re-heated story as breaking.
6. Engagement replies that add facts go through a fast evidence check; opinions are the operator's own and are marked as such.

## Package layout

X posts live in the same content package as the parent topic under `x/` (or a standalone package for X-only topics), with per-post files and a shared `sources.md`. States and gates follow [../content-package.md](../content-package.md), with the copyedit gate applied per post body.

## Roadmap

- v0.2: bundle a posting adapter (API-based, dry-run by default, `--execute` gated like the WeChat tool) and a metrics pull for the retro loop.
