# press-fleet · 明牌编辑部

**一支跑自媒体的 AI 编辑舰队，SOP 全部开源，明牌运营。**

[English](README.md) · [架构](docs/architecture.md) · [为什么明牌](docs/philosophy.md) · [实战教训](docs/lessons.md) · [CHANGELOG](CHANGELOG.md)

[research-fleet](https://github.com/shanyuzhe/research-fleet) 的姊妹项目：research-fleet 给科研配一支不偷工减料的 AI 团队，press-fleet 给自媒体配一支不糊弄读者的 AI 编辑部。

## 为什么需要它

2026 年 4 月起，微信等平台严打 AI 低质内容：限流、删除、封号，AI 内容农场一夜死亡。市场的主流应对是"降 AI 率"灰产——花 4.8 元/千字把 AI 味藏过检测器。press-fleet 走相反的路：**别人把 AI 味藏起来，我们把生产过程亮出来**。平台打的从来是低质，不是 AI；质量可证明，比 AI 率可伪装更能穿越治理周期。

现有自媒体 SOP 有三个病（完整证据和来源见 [docs/why.md](docs/why.md)）：

1. **SOP 是给人读的文档，不是能强制执行的机制**——81% 的记者在用 AI，只有 13% 的编辑部有政策；有政策的照样连发更正。
2. **火力全在流量上限，质量下限裸奔**——事实翻车行政拘留、图片钓鱼维权 17 万的账单已经到账，而来源核查和权利登记不在任何一张模板里。
3. **平台严打后全行业在骗检测器**，没人修内容本身。

press-fleet 对着这三个病打，把新闻编辑部的纪律拆成可执行的机制：**信号进（信息源雷达 + 读者反馈）→ 选题台 → 证据层 → 六角色生产流水线 → 确定性门禁 → 用户授权发布 → 复盘 → SOP 改版**。

## 关键机制

- **八个角色，各带红线**：主编、证据编辑、主笔、终校、视觉与权利编辑、发布审计，加上雷达侦察和复盘教练。审计员不许改稿，写手不许造事实，终校不许当二号文风师。
- **门禁是确定性的**：逐句终校与正文 SHA-256 绑定，改一个字就作废重跑；包校验器零依赖、可进 CI；模型判断只做参考，记录在案的证据才作数。
- **中文适配的 AI 痕迹诊断**：不用英文词表和统计阈值糊弄中文，抓的是真实症状——改判句式复用、反问连发、否定式标题、俯视语气。
- **明牌迭代**：每篇文章脚注标注生产它的 SOP 版本；读者评论、平台数据、GitHub issue 都是信号，采纳的变更进 CHANGELOG。你现在看到的每一条规则，都写着它是被哪次失败教出来的（见 [lessons](docs/lessons.md)）。

## 快速开始

主战场是 **Claude Code 和 Codex**：press-fleet 服务 AI-native 创作者，不做网页工具版。门禁的完整度优先于上手的轻量度——事实、权利、终校三道门不为速度让路。

### Claude Code（插件）

```bash
# 克隆后在 Claude Code 中作为本地插件加载，或安装到插件目录
git clone https://github.com/shanyuzhe/press-fleet
```

然后在你的工作目录运行 `/press-init`，按提示选平台（微信公众号 / X / 小红书），舰队会搭好工作区。八个角色以子代理形式可用。

### Codex

```bash
# skills/press-ops 目录自包含，拷进你的项目即可
cp -r press-fleet/skills/press-ops <your-project>/.agents/skills/press-ops
```

单会话按 `references/team.md` 的流程依次扮演各角色——本项目最初就是这样跑起来的。

### 微信发布

`tools/wechat_publish.py` 基于 [Wenyan CLI](https://github.com/caol64/wenyan-cli)：渲染、传图、建草稿一条龙。默认 dry-run 不碰网络；`--execute` 才创建草稿，且永远不代替你按发布键。凭据放本地 `.env`，模板见 `/press-init` 生成的 `.env.example`。

## 仓库结构

```text
agents/            # 8 个角色（Claude Code 子代理）
commands/          # /press-init 工作区脚手架
skills/press-ops/  # 协议核心：SOP、团队、门禁、雷达、平台适配（双运行时共用）
tools/             # 包校验器 + 微信发布适配器
docs/              # 架构、明牌哲学、实战教训
templates/         # 复盘模板
examples/          # demo-package：能通过校验器的最小完整内容包（也是 CI 的校验对象）
```

想快速理解内容包机制，从 `examples/demo-package/` 开始：改动正文任意一个字再跑校验器，亲眼看哈希门失效。

## 路线图

| 阶段 | 内容 | 状态 |
|---|---|---|
| v0.1 | 微信全流程 + 双运行时 + 雷达 + 复盘闭环 | ✅ 当前 |
| v0.2 | X 发布适配器 + 指标回拉 | 计划 |
| v0.3 | 小红书卡片管线（导出待发包，不做非官方自动发布） | 计划 |
| 阶段三 | 舰队网络：多家用同一缺陷分类法互相审稿 | 有触发条件，见[架构](docs/architecture.md) |

## 参与

评论区、issue、PR 都是信号，怎么发才有效见 [CONTRIBUTING](CONTRIBUTING.md)。如果你用这套 SOP 跑起了自己的号——你就是路线图第三阶段的触发条件，来 issue 里报个到。

## License

MIT
