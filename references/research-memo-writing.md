# 中文 Research Memo 写作规范

在撰写任何论文精读笔记或 Research Memo 前完整阅读本文件。这里保留正文结构、Method Story、Evidence、Failure、Quick Recall、可选附录和写作风格规则。

研究兴趣连接、Research Map Check 和 Actionable Ideas 的细则位于 `research-map-and-ideas.md`；所有 paper 任务还必须读取该文件。

## 目录

1. 中文 Research Memo 正文结构
2. 小节写法：Main Thesis、Method、Evidence、Failure
3. Quick Recall 与可选附录
4. 写作风格

## 7. 中文 Research Memo 正文结构

不要在正文中重复数据库元数据。如果 Title / Author / Year / URL / Code 已经是数据库属性，不要再放完整“论文基本信息”。

默认正文结构：

```markdown
# 中文 Research Memo

## 0. TL;DR
## 1. Main Thesis：这篇到底在证明什么？
## 2. Key Concepts / Keywords
## 3. Method Story：从输入到输出
## 4. Evidence：实验真正说明什么？
## 5. Failure & Hidden Assumptions
## 6. 和我当前研究兴趣的连接
## 7. Research Map Check
## 8. Actionable Ideas
## 9. Quick Recall
```

如果只是聊天中讲解，也使用同一套结构，但可以把标题改得更自然：

```markdown
# 论文中文精读笔记

## 1. 一句话总结
## 2. 这篇文章到底在解决什么问题？
## 3. 之前的方法为什么不够？
## 4. 方法总览：从输入到输出
## 5. 核心机制细讲
## 6. 实验结果和 ablation：到底证明了什么？
## 7. 我的判断：这篇真正有价值的点
## 8. 局限性
## 9. 和我当前研究兴趣的连接
## 10. 是否值得更新到 research map？
```

注意：不要出现单独的“关键图表总表”小节。所有图都应该嵌入到对应解释位置。

如果论文很短或不重要，压缩小节。如果论文和当前 research lens 高度相关，扩展 Method Story、Evidence、Failure、Research Connection 和 Actionable Ideas。

---

## 8. 小节写法要求

### 8.1 TL;DR / 一句话总结

开头必须直接说明核心贡献：

> 这篇文章的核心是：……

这个句子应说明真实贡献，而不是复述标题。

好的示例：

> 这篇文章的核心是：把连续 robot action chunk 编码成短的、总能解码的、从粗到细有顺序的离散 token 序列，让 autoregressive policy 可以像 LLM 一样逐 token 生成动作。

随后用 1–2 段说明：这篇 paper 本质上是什么；它不是什么；为什么重要；最大限制是什么。

### 8.2 Main Thesis：这篇到底在证明什么？

使用 3–5 个大论点，不要碎成太多小 bullet points。

聚焦：central claim、paradigm position、它挑战了哪些既有假设、为什么对 robotics 重要、不能从中推出什么。

示例：

```markdown
TiPToP 的核心不是提出一个新 policy，而是在证明一个系统级判断：当 foundation perception 足够强之后，传统 TAMP 最大的瓶颈不再一定是 planner 本身，而是 pixels-to-symbolic/geometric world state 的接口。

它把 VLA 隐式压在 latent 里的东西拆出来：object identity、3D geometry、grasp candidates、symbolic goal、collision constraints 和 robot trajectory。这个拆解让它在 semantic distractor 和 multi-step tabletop tasks 上很强，但也暴露出另一个问题：一旦显式 world state 错了，planner 会非常自信地计划一个错误世界。
```

### 8.3 先讲问题，再讲方法

始终先解释问题，再解释方法。

回答：

- 输入是什么？
- 输出是什么？
- 现有范式哪里不够？
- 为什么这个问题在 robotics / embodied AI 中重要？
- 这篇论文把问题重新定义成了什么？

### 8.4 Baseline 对比

只比较理解动机所必需的 baselines。

对每个 baseline 说明：它怎么做、优点是什么、致命问题是什么、本文针对它补了什么。有帮助时使用紧凑表格。

### 8.5 Key Concepts / Keywords

用紧凑关键词表作为概念索引。

格式：

| Keyword | 这篇里的含义 | 为什么重要 |
|---|---|---|

不要过度解释每个术语。关键词示例：Ordered Action Tokenization、Coarse-to-fine Action Representation、Prefix-decodable Robot Policy、Action Token Budget、Pixels-to-TAMP Interface、Object-centric World State、VLM Grounding、Plan Skeleton、Action Chunking、Open-loop Execution、Closed-loop Recovery、Multi-view Correspondence、Wrist Camera、Belief-space Planning、VLA as Reactive Skill Primitive。

### 8.6 Method Story：从输入到输出

把方法讲成一个故事，而不是 checklist。

始终包含一个 ASCII pipeline，并在讲到对应模块时嵌入关键方法图。

示例：

```text
Stereo RGB + language instruction
        ↓
VLM grounding + object detection
        ↓
segmentation + depth + grasp proposals
        ↓
object-centric 3D symbolic-geometric state
        ↓
TAMP plan skeleton + continuous optimization
        ↓
motion planning
        ↓
joint trajectory + gripper execution
```

然后用连贯段落解释流程。每个阶段要讲清：input、operation、output、design motivation，以及可能的 failure 或 hidden assumption。

对于 robotics papers，始终覆盖：

1. observation representation；
2. state / world representation；
3. action representation；
4. policy / planner / controller；
5. training 或 inference-time optimization；
6. open-loop vs closed-loop；
7. embodiment assumptions。

除非必要，不要创建过多子小节。

### 如果论文是 VLA / policy learning

讨论 vision encoder、language encoder、proprioception、action representation、action chunking、action tokenizer / detokenizer、action tokens 是否 ordered / causal / prefix-decodable、diffusion / flow matching / autoregressive decoding、training data、loss、control frequency、closed-loop inference、cross-embodiment assumptions。

### 如果论文是 TAMP / planning / neuro-symbolic

讨论 predicates、symbolic state、operator schema、preconditions / effects、continuous variables、grasp / placement / IK / trajectory、motion planner、perception-to-planning interface、replanning 或 execution monitoring。

### 如果论文是 world model

讨论 world state、latent vs explicit representation、object-centric structure、transition / dynamics、memory、rollout、planning space、compounding error。

### 如果论文和 multi-view / wrist-camera 有关

讨论 camera setup、pixel-level concat vs token-level fusion、late fusion vs cross-attention、3D lifting、camera-aware positional encoding、是否真的建模了 view correspondence、wrist camera 是帮助 local refinement 还是引入噪声。

### 8.7 Evidence：实验真正说明什么？

不要只汇报数字。围绕大结论组织实验，并在讲到结果时嵌入结果表、曲线、ablation 图或真实机器人图。

分析：

- benchmark relevance；
- baseline fairness；
- metrics；
- task categories；
- ablations；
- failure breakdown；
- real-robot results 是否有说服力；
- 结果证明了什么；
- 结果没有证明什么。

有帮助时使用表格：

| Task Category | Paper method 强在哪里 | Baseline 强在哪里 | 真正说明什么 |
|---|---|---|---|
| Simple pick-place | 轨迹快、几何明确 | 闭环反应好 | 两者差距不大 |
| Distractor | 显式 grounding 强 | 容易被 distractor 干扰 | 结构化 grounding 有优势 |
| Semantic | VLM → predicate 明确 | policy 隐式理解不稳 | symbolic goal 有价值 |
| Multi-step | TAMP plan skeleton | 长程结构隐式学 | planning 优势明显 |
| Small/slippery objects | 容易失败 | 可 retry | closed-loop recovery 很关键 |

使用 source anchors，例如 Paper Table I、Paper Fig. 2、Paper Fig. 5、Appendix A、Project Page Demo、GitHub README。

### 8.8 Failure & Hidden Assumptions

这一节要写得尖锐一点，聚焦最重要的少数 failure modes。

对每个 failure mode 使用：

```text
failure source → why it happens → whether paper solves it → possible fix
```

常见 hidden assumptions：objects visible、scene static、camera calibration accurate、controller tracking accurate、object geometry easy enough、grasp predictor reliable、VLM grounding reliable、predicates expressive enough、action primitives cover the task、benchmark is pick-place-friendly、no serious deformable objects、no complex contact、no strong bimanual coordination、no online correction、reset protocol is fair。

如果论文有 failure figure 或 failure table，要直接嵌入这一节，而不是放到单独图表清单里。

---

### 8.12 Quick Recall

每篇 memo 最后用一个短 recall block 收尾。用户只读这一节，也应该能记住这篇 paper。

格式：

```markdown
## Quick Recall

- 这篇一句话：
- 最重要 keyword：
- 方法主线：
- 实验结论：
- 最大硬伤：
- 和我当前方向的关系：
- 值不值得继续深挖：
```

保持紧凑。

---

## 9. 可选附录

对于重要论文，只有在有用时，才在 Quick Recall 后添加 appendix。

可选 appendix：

```markdown
## Appendix A. Reproduction Checklist
## Appendix B. Source Anchors
## Appendix C. Code Notes
## Appendix D. Detailed Experiment Table
```

不要把所有详细 checklist 内容塞进 main memo。用 appendix 避免正文碎片化。

---

---

## 13. 写作风格

主要语言：中文。

风格要求：

- 像研究合作者，而不是营销总结；
- 直接、技术上认真；
- 少用碎小节，多用连贯论证；
- 用关键词作为概念锚点；
- 图必须服务解释，并嵌入对应段落；
- 避免在正文里重复数据库 metadata；
- 避免很长的泛泛 related-work 总结；
- 诚实指出 novelty 弱点和 hidden assumptions；
- 不过度吹捧；
- 不无理由地过度批评；
- 不确定时就说不确定；
- 中文解释要占绝大多数，英文只作为必要术语。

对于 robotics papers，始终分析 observation representation、world/state representation、action representation、embodiment assumptions、controller / execution loop、failure modes。

对于 planning papers，始终分析 predicates、operators、plan skeletons、continuous constraints、perception-to-planning interface。

对于 VLA papers，始终分析 data scale、action chunking、action representation、closed-loop behavior、cross-embodiment assumptions、它是否真的在 reasoning，还是主要在 imitation。

对于 multi-view / wrist-camera papers，始终分析 view fusion mechanism、camera correspondence、wrist view 是否被区别于 third-person view 处理、是否有 ablation 证明 wrist view 有用。

---
