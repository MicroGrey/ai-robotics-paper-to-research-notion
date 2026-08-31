# 质量检查与完成汇报

完成任何 paper memo 前完整阅读本文件；Notion 入库任务还需执行其中的入库汇报要求。

## 14. 质量检查清单

最终完成任何 paper memo 前，检查：

- 如果是 paper2notion / 精读入库 / 明确翻译任务，是否已阅读并执行 `references/chinese-structured-translation.md`？
- 是否按顺序提供了“中文 Research Memo → 中文结构化详译”，而不是把两者混成一层？
- 详译是否覆盖原文 Abstract、Introduction、Method、Experiments、Limitations / Conclusion 和关键 Appendix？
- 详译是否保持原文章节编号，并保留重要图号、表号、公式、数字、单位和限定词？
- 作者 claim、项目页/代码页补充、译者注和个人判断是否清楚分开？
- PDF 抽取损坏的公式、变量或表格是否回看了原页，而不是输出残缺文本？
- 是否先讲清楚了问题，而不是直接讲方法？
- 是否先检索并优先使用了 paper 原文与 project webpage 的原始视觉材料？
- Method Story 是否至少有一张方法、系统或核心机制图；若原文确实没有，是否明确说明？
- Evidence 是否优先使用了结果表、result plot、ablation、qualitative result 或真实 demo sequence？
- 如果存在 failure figure / failure table，是否放进了 Failure & Hidden Assumptions？
- 图是否嵌入到对应讲解段落，而不是单独堆图？
- 是否解释了核心图，而不是把图当装饰？
- 每张图是否标注了来源、source anchor、对应 claim，以及它能证明和不能证明什么？
- 是否只在原始来源缺少合适视觉材料或需要跨来源整合时才使用自绘/生成图，并明确标注“非论文原图”？
- 如果关键视觉材料少于 2 个，是否在完成汇报中说明具体原因？
- 是否讲清楚输入、输出、observation、state、action、policy / planner / controller？
- 是否解释了 baseline 为什么不够？
- 是否给出了主要实验趋势，而不是堆数字？
- 是否说明了 ablation 到底证明了什么？
- 是否区分了作者 claim 和自己的判断？
- 是否指出了具体局限，而不是泛泛而谈？
- 是否和当前 research lens 建立了必要但不牵强的连接？
- 是否只在必要时建议更新 mindmap？
- 是否避免了正文开头重复数据库 metadata？
- 是否中文为主，英文只保留必要技术词？
- 是否能让用户读完后记住“大论点”和“关键词”，而不是只记住一堆细节？

---

## 15. 默认完成汇报

工作流完成后，面向用户的回复保持简洁。

如果只是聊天精读，说明已经整理了中文笔记，并简要说明覆盖了哪些重点。

如果写入 Notion，报告：

1. 论文条目是创建还是更新；
2. 是否写入中文 Research Memo；
3. 是否写入中文结构化详译，以及覆盖到哪些正文和附录章节；
4. 哪些关键图被嵌入到了哪些段落；
5. 是否向 AI Robotics 想法库添加 ideas；
6. 是否建议更新 research map；
7. 哪些来源缺失或细节不确定；
8. 是否优先使用了 paper / project webpage 原始视觉材料；若少于 2 个或未使用原始图，具体原因是什么。

示例：

```text
已更新论文库条目，并写入中文 Research Memo 与按论文原文章节组织的中文结构化详译。详译覆盖摘要、引言、方法、实验、讨论/局限和与复现相关的关键附录；作者内容与个人判断保持分离。正文没有重复 metadata，图没有单独堆成清单，而是放进 Method Story / Evidence / Failure 和详译对应章节里。

这次嵌入了 5 个关键视觉材料：
1. Paper Fig. 1 teaser：放在问题设定里
2. Paper Fig. 2 system overview：放在 Method Story 里
3. Paper Fig. 3 perception module：放在 perception-to-planning 讲解里
4. Project page failure demo：放在 Failure & Hidden Assumptions 里
5. 自绘 closed-loop extension schematic：放在 Research Map Check 里

想法库新增 1 条：Closed-loop TiPToP with Predicate Effect Monitor。
Research Map 建议小更新：在 Current Research Lens / Planning 下加入 Perception-to-Planning Interface。
```
