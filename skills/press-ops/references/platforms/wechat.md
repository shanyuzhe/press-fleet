# WeChat preview and draft workflow

Use the pinned open-source [Wenyan CLI](https://github.com/caol64/wenyan-cli) for Markdown rendering, inline image uploads, permanent cover upload, and WeChat `draft/add`. Do not maintain a separate renderer or WeChat API client.

The adapter at `tools/wechat_publish.py` only:

- maps `draft.md` plus `publish.yml` to Wenyan frontmatter;
- removes the editorial-only leading H1 so the platform title is not duplicated;
- runs the content-package validator and release gates (title/author/digest length, cover rights, state flags);
- produces a phone-width local preview;
- keeps the default draft command as a no-network dry-run.

## One-time setup

At your **platform root** — the directory that contains your content packages, typically created by `/press-init`:

```bash
npm install @wenyan-md/cli@2.0.11
pip install pyyaml
cp <press-fleet>/.env.example .env   # then fill WECHAT_APP_ID / WECHAT_APP_SECRET locally
```

Never paste the secret into chat, a draft, logs, or committed files. Add `.env`, `dist/`, and `.wenyan-runtime/` to your workspace `.gitignore` before anything else.

The tool locates the platform root by walking up from the content package until it finds the Wenyan install; set the `PRESS_PLATFORM_ROOT` environment variable to override. The validator must sit next to the adapter in the same `tools/` directory.

The WeChat account must expose the required material and draft APIs. The machine's public egress IP must be allowed in the Official Account developer configuration, unless a separately reviewed fixed-egress deployment is used.

## Per-article configuration

Create `publish.yml` in the content package:

```yaml
title: "API title, at most 32 characters"
author: ""
digest: "Feed summary"
cover: "assets/cover.png"
source_url: ""
theme: "default"
highlight: "solarized-light"
mac_style: false
footnote: true
need_open_comment: false
only_fans_can_comment: false
```

The cover must exist inside the package, be registered in `asset-manifest.yml`, allow `wechat`, and have a resolved rights status. Do not use an unresolved screenshot as the cover merely to satisfy the API.

## Commands

Local preview; no network or external write:

```bash
python tools/wechat_publish.py preview <content-package> --open
```

Draft preflight; still no network or external write:

```bash
python tools/wechat_publish.py draft <content-package>
```

Create exactly one draft after explicit current-task authorization:

```bash
python tools/wechat_publish.py draft <content-package> --execute
```

`--execute` delegates rendering, image uploads, cover material upload, and draft creation to `@wenyan-md/cli`. It does not publish or mass-send. After success, a human still checks the actual draft in the Official Account backend.

Pinned-version notes:

- Wenyan CLI 2.0.11 does not forward a custom `digest` field to `draft/add`; WeChat derives an excerpt. Treat `publish.yml`'s `digest` as the desired backend check/edit value.
- Wenyan CLI 2.0.11 uploads body images as permanent image materials and reuses its local upload cache for duplicate assets. Review material-library growth during normal operations.

## Generated files

`dist/` contains `wenyan-source.md`, `wechat-content.html`, `wechat-preview.html`, and `publish-plan.json`. These files can be regenerated and must not be edited as canonical content.

Wenyan's local token and upload cache live under `<platform-root>/.wenyan-runtime/`; the directory is private and must stay Git-ignored.
