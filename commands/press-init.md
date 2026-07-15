---
description: Scaffold a press-fleet media workspace (context contracts, radar instance, platform dirs, content-package layout)
---

Initialize a press-fleet workspace in the current directory (or the directory the user names). Load the `press-ops` skill first.

Create this layout, asking the user for platform selection (WeChat / X / Xiaohongshu, multi-select) and workspace language before writing:

```text
<workspace>/
├─ 上下文/                         # long-lived contracts (rename to context/ for non-Chinese workspaces)
│  ├─ 品牌定位.md                  # positioning: theme, default reader, long-term beats
│  ├─ 作者声音.md                  # voice contract: how the account sounds, banned phrasing
│  ├─ 事实与引用规范.md            # facts & citation norms
│  ├─ 视觉与版权规范.md            # visual & rights norms
│  └─ 当前重点.md                  # rolling current focus
├─ 知识库/
│  └─ 信息源/
│     └─ 信息源雷达.md             # radar instance — seed from skill reference source-radar-example.zh.md
├─ <platform>/                     # one dir per selected platform, e.g. 微信公众号/
│  ├─ 内容/YYYY/MM/<slug>/         # content packages per references/content-package.md
│  ├─ 选题/                        # topic desk: candidates + selection records
│  ├─ 复盘/                        # retro records per templates/retro.md
│  └─ tools/                       # platform adapters (copy wechat_publish.py for WeChat)
└─ .gitignore                      # must cover .env, dist/, runtime caches
```

Rules:

1. Fill each context file with a skeleton of questions to answer, not invented content — positioning and voice belong to the operator.
2. Seed the radar instance from the packaged example, then tell the user to prune beats they do not cover.
3. For WeChat, copy `tools/wechat_publish.py` and `tools/validate_content_package.py` into the workspace, create `.env.example` (WECHAT_APP_ID / WECHAT_APP_SECRET placeholders), and add `.env` plus `dist/` and runtime caches to `.gitignore` before anything else.
4. Record the press-fleet SOP version (from CHANGELOG) in `上下文/当前重点.md` so articles can cite it.
5. Do not create a git repo, push, or publish anything without the user's say-so.

Finish by listing what was created and the first three suggested actions: fill the voice contract, prune the radar, run one topic through the Standard mode pipeline.
