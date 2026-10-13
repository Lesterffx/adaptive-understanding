# Adaptive Understanding

> **自适应理解引擎**：先判断“为什么没看懂”，再选择最合适的表达形式，而不是默认生成更多内容。
>
> 核心路径：**Text → Table → Diagram Type → Interactive → Animation/Video**

[English README](README_EN.md)

## 为什么需要这个 Skill？

AI 已经可以快速生成大量文字、图表、网页、动画和视频。真正越来越稀缺的，不只是“生成能力”，而是：

> **如何让人更快、更准确地理解 AI 生成的内容。**

Adaptive Understanding 把“解释”看成一个**表达形式路由问题**：

```text
来源材料
   ↓
保留事实、范围、不确定性与关系
   ↓
诊断理解卡点
   ↓
选择最小充分表达
   ↓
Text → Table → Diagram Type → Interactive → Animation/Video
   ↓
验证是否改变原意
   ↓
如果仍没懂，就改变解释路径
```

这条路径不是固定流水线。Skill 可以跳过某些层级、停留在当前层级，或者在复杂表达反而增加负担时，主动降级到更简单的形式。

## 核心原则

1. **Source Fidelity（来源忠实）**：保留数字、单位、归因、否定、范围、前提、不确定性，以及“相关 ≠ 因果”的区别。
2. **Minimum Sufficient Representation（最小充分表达）**：用能解决当前理解问题的最简单形式，不默认一次生成全部格式。
3. **Representation Fit（表达形式匹配）**：根据“信息结构”选择表达形式，而不是为了视觉效果而增加图表或动画。
4. **Progressive Escalation（渐进升级）**：用户仍没懂时，改变解释路径，而不是单纯继续加字。

可以把它理解成：

```text
Understanding
= Source Fidelity
× Representation Fit
× Explanation Quality
```

只要其中一项接近 0，即使输出看起来很漂亮，解释仍然可能失败。

## 表达形式决策树

| 理解需求 | 默认表达形式 |
| --- | --- |
| 单个概念、论点、机制、证据边界 | **Text** |
| A / B / C 使用共同维度比较 | **Table** |
| 组成、模块、上下游 | **Architecture / Block Diagram** |
| 顺序、条件、失败返回、重试、AND/OR | **Flowchart** |
| 多角色协作、责任边界、交接 | **Swimlane** |
| 分类、从属、层级关系 | **Tree / Hierarchy** |
| 有证据支持的因果链、反馈回路 | **Causal Diagram** |
| 数据从哪里来、经过哪里、到哪里去 | **Data-flow Diagram** |
| 时间顺序、版本演进 | **Timeline** |
| 多对多关系 | **Network Graph** |
| 趋势、分布、数值关系 | **Chart** |
| 改参数、改条件、观察结果变化 | **Interactive** |
| 时间演化、状态转换、逐步执行 | **Animation / Video** |

完整路由规则请参阅：[`references/representation-decision-tree.md`](references/representation-decision-tree.md)

## 和普通“帮我解释一下”有什么不同？

普通 Prompt 往往默认“没看懂 → 再解释得简单一点”。Adaptive Understanding 会先判断**没懂的原因**：

- 不认识一个术语 → **Text**
- 多个方案混在长段落里 → **Table**
- 看不懂步骤和条件分支 → **Flowchart**
- 不知道人和 Agent 各自负责什么 → **Swimlane**
- 想知道参数改变后结果怎样变化 → **Interactive**
- 静态图看懂了，但脑中仍没有过程感 → **Animation / Video**

如果真正的问题是“来源材料本身没有答案”，Skill 不会继续用更漂亮的图或动画掩盖证据缺口，而会明确指出：**材料没有告诉我们。**

## Epistemic Safety：清楚不等于正确

一张漂亮的图、一个 Slider、一段动画或视频，可能让未经支持的内容显得更可信。因此本 Skill 特别强调：

- 重要关系应能追溯到来源；
- 未知信息继续保持未知；
- 不把缺失信息静默变成假设；
- 因果箭头必须有因果依据；
- 交互公式必须来自来源、规则、代码路径，或明确标记为“教学假设”；
- 动画中的移动、变色、连线和状态变化必须表达真实语义，而不是装饰效果。

## ASD-STE100 的启发

本 Skill 借鉴了 **ASD-STE100 Simplified Technical English** 的部分表达原则，例如术语稳定、减少句法歧义、操作步骤更直接，以及“简化语言但不删掉关键条件”。

但本项目**不声称正式符合 ASD-STE100，也不提供 STE 合规认证**。中文不会机械把英文 20 / 25 words 的限制换成中文字数限制。

中文适配说明：[`references/ste-and-chinese.md`](references/ste-and-chinese.md)

来源说明：[`references/sources.md`](references/sources.md)

## 示例

- [`examples/flow.svg`](examples/flow.svg)：并发检查、AND 条件、失败分支、补材料回路与人工核对。
- [`examples/parallel-demo.html`](examples/parallel-demo.html)：用明确公式与教学假设演示参数变化。
- [`examples/process-animation.html`](examples/process-animation.html)：可播放、暂停、上一步、下一步、重新开始的流程动画。
- [`examples/animation-storyboard.md`](examples/animation-storyboard.md)：宿主不能直接生成视频时的 storyboard / narration 降级方案。
- [`examples/walkthrough.md`](examples/walkthrough.md)：同一份材料如何分别使用 Text、Table、Diagram、Interactive、Animation。

## Acceptance Tests

本项目加入验收案例，覆盖证据范围、过度外推、Table / Diagram 路由、Diagram Type 选择、并发 vs 顺序、AND vs OR、未经支持的因果关系、编造公式、Animation 语义、过度生成，以及复杂视觉的降级行为。

完整案例：[`references/acceptance-cases.md`](references/acceptance-cases.md)

## 仓库结构

```text
adaptive-understanding/
├── README.md
├── README_EN.md
├── LICENSE
├── SKILL.md
├── examples/
│   ├── animation-storyboard.md
│   ├── flow.svg
│   ├── parallel-demo.html
│   ├── process-animation.html
│   ├── source.md
│   └── walkthrough.md
└── references/
    ├── acceptance-cases.md
    ├── representation-decision-tree.md
    ├── sources.md
    └── ste-and-chinese.md
```

## 灵感来源与参考资料

这个 Skill 的主要产品灵感来自 **Andrej Karpathy** 关于“如何让人更容易理解 LLM 输出”的帖子：

- **Andrej Karpathy — X 原帖**  
  https://x.com/karpathy/status/2105819303471976479

Karpathy 的帖子提出了使用不同输出形式来降低理解成本的思路，包括文字、图示、网页和视频。

**Adaptive Understanding 在此基础上进一步扩展为：**

> **Text → Table → Diagram Type → Interactive → Animation/Video**

并加入 Source Fidelity、Epistemic Safety、Minimum Sufficient Representation、Progressive Escalation、Diagram Type Routing 与 Acceptance Tests。

其他参考：

- ASD-STE100 Simplified Technical English: https://www.asd-ste100.org/
- ASD-STE100 Issue 9: https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf

详细出处与适用边界：[`references/sources.md`](references/sources.md)

## License

本项目采用 **MIT License**。请参阅 [`LICENSE`](LICENSE)。

## 当前状态

当前仓库包含 **Adaptive Understanding V2** 的 Skill 规范、表达形式决策树、验收案例与示例，并设计为 **host-agnostic**。

当宿主不具备某种能力时，Skill 应该优雅降级，例如 Video → Storyboard + Narration、Animation → HTML / Step-by-step storyboard、Diagram → Text relationship map，而不是假装已经生成或验证不存在的成果。

## 一句话总结

> **Adaptive Understanding 不是让 AI 生成更多内容，而是让 AI 判断：为了让人真正看懂，当前最应该生成什么。**
