---
title: "示例：一个通过全部门禁的内容包长什么样"
platform: wechat
status: ready
created: 2026-07-16
updated: 2026-07-16
as_of: 2026-07-16
fact_checked: true
rights_checked: true
copyedit_checked: true
copyedit_body_sha256: "f8dd6d532feeae53fa52c1a6818295d2f485cbd120ed6bf8c3b70e466de429a0"
published_url: ""
---

# 示例：一个通过全部门禁的内容包长什么样

这个目录是一个最小但完整的 press-fleet 内容包。它的正文（就是你正在读的这篇）刻意写得很短，但七个档案文件齐全，且能通过校验器：

```bash
python tools/validate_content_package.py examples/demo-package
```

每个文件各管一件事：`brief.md` 记录选题判断和读者承诺；`sources.md` 记录每条事实的来源和访问日期；`copyedit.md` 是逐句终校的记录，绑定正文哈希；`review.md` 是发布审计员的门禁打分；`asset-manifest.yml` 登记每张图的来源与权利；`publish-record.md` 记录发布状态。

想直观感受哈希门，做一个实验：把正文里任意一个字改掉，再跑一遍上面的命令。校验器会报错，因为正文的 SHA-256 已经和 `copyedit.md` 里记录的不一致——这就是"改一个字也要重跑终校"的机制在工作。

真实稿件和这个示例的区别只在体量：来源更多、审校轮次更多、配图有真实的权利登记。结构完全相同。
