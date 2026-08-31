# AI Robotics Paper to Research Notion

一套给 Codex 使用的 AI Robotics / Embodied AI / Robot Learning 论文精读工作流。它会把论文 PDF、project page、GitHub 与关键视觉证据整理成中文 Research Memo；在用户要求入库时，还会生成按原文章节组织的中文结构化详译，并同步到个人 Notion 研究库。

核心笔记方法来自 `paper2notion-cn-v1.2.0`。这个公开版本只做了可移植化：不包含作者个人 Notion 页面 ID，也不会把内容写进作者的工作区。

## 一键安装

前提：已经安装 Codex，并在 Codex 中安装、连接且授权 Notion 插件。

```bash
curl -fsSL https://raw.githubusercontent.com/ZhangJiayi24/ai-robotics-paper-to-research-notion/main/install.sh | bash
```

安装器会把 skill 放到 Codex 当前使用的个人 skill 目录：

```text
~/.agents/skills/ai-robotics-paper-to-research-notion
```

它不会读取 Notion，也不会保存 token。重复执行同一条命令即可升级。Codex 通常会自动发现更新；如果 skill 没有出现，重启 Codex。

也可以先 clone 再本地安装：

```bash
git clone https://github.com/ZhangJiayi24/ai-robotics-paper-to-research-notion.git
cd ai-robotics-paper-to-research-notion
bash install.sh
```

官方说明：[Codex Skills](https://developers.openai.com/codex/skills) · [Codex Plugins](https://developers.openai.com/codex/plugins)

## 第一次使用：复建 Notion 工作区

安装后，在 Codex 中发送：

```text
paper2notion 初始化
```

Codex 会在你当前连接的 Notion 工作区中创建或复用：

- `AI Robotics Research Hub`
- `AI Robotics 论文库`
- `AI Robotics 想法库`
- `Current Research Lens`
- `Research Map`

如果已存在同名 Hub，它会优先复用并只补齐缺失组件，不会使用任何写死的页面或数据库 ID。初始化属于 Notion 外部写入，因此只会在你明确发送初始化指令后执行。

## 触发指令：`paper2notion`

日常使用直接输入 `paper2notion` 即可。最短写法：

```text
paper2notion <PDF / arXiv / project page URL>
```

默认含义是：中文精读 → 中文结构化详译 → 写入 Notion。

完整的 `$ai-robotics-paper-to-research-notion` 是显式调用形式；当你想明确指定 skill 时使用，效果相同。

## 常用方式

只做中文精读，不写 Notion：

```text
paper2notion 只精读不入库：<PDF / arXiv / project page URL>
```

精读、结构化详译并入库：

```text
paper2notion <PDF / arXiv / project page URL>
```

带着自己的研究问题读：

```text
paper2notion <论文 URL>
我关注的问题：这篇工作如何表示 action、是否闭环、wrist camera 是否真正建模了 view correspondence？
```

首次初始化 Notion 研究库：

```text
paper2notion 初始化
```

查看版本：

```text
paper2notion 当前版本
```

## 这套流程会产出什么

- 中文 Research Memo：问题、主论点、method story、实验依据、failure、hidden assumptions 与研究连接。
- 图随文走的视觉证据：优先使用 paper 和 project page 原图，并说明它支持与不能支持的 claim。
- 中文结构化详译：入库或明确要求翻译时，按论文原文章节覆盖摘要、方法、实验、限制与关键附录。
- Notion 论文条目：结构化 metadata、阅读优先级、实验价值、一句话结论和可复现点。
- 少量高质量 Actionable Ideas，以及是否值得更新 Research Map 的判断。

## 仓库结构

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── chinese-structured-translation.md
│   ├── notion-paper-records.md
│   ├── notion-workspace-setup.md
│   ├── quality-and-completion.md
│   ├── research-map-and-ideas.md
│   ├── research-memo-writing.md
│   └── source-and-visual-evidence.md
├── install.sh
├── LICENSE
└── README.md
```

`SKILL.md` 只保留触发、模式选择、关键不变量和渐进式路由。来源与视觉证据、Research Memo 写法、Research Map、Notion 字段、详译和完成检查分别在需要时加载；笔记方法和判断标准没有因拆分而删减。

## 环境覆盖

默认安装到 `~/.agents/skills`。如需安装到另一个 Codex skills 目录：

```bash
CODEX_SKILLS_DIR=/your/skills/path bash install.sh
```

如 fork 了仓库，可在远程安装时覆盖来源：

```bash
curl -fsSL https://raw.githubusercontent.com/your-name/your-repo/main/install.sh | \
  AI_ROBOTICS_SKILL_REPO=your-name/your-repo bash
```

## 隐私与边界

- 仓库不包含个人 Notion URL、页面 ID、数据库 ID 或访问 token。
- 普通论文精读不会写入 Notion。
- Notion 初始化和论文入库只在用户明确要求时执行。
- 公开发布包含论文原图的笔记前，仍需由发布者确认相应图片与内容的再分发权限。

## License

[MIT](LICENSE)
