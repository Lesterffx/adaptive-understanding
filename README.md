# Adaptive Understanding

> An adaptive understanding skill that routes complex information into the **minimum sufficient representation**: **Text → Table → Diagram Type → Interactive → Animation/Video**.
>
> 自适应理解引擎：先判断“为什么没看懂”，再选择最合适的表达形式，而不是默认生成更多内容。

## Why this skill exists

AI can generate more text, diagrams, webpages, and videos than a person can reasonably consume. The harder problem is therefore not only **generation**, but **understanding**: how to present the same source material in a form that lowers cognitive load without changing the facts.

Adaptive Understanding treats explanation as a routing problem:

```text
Source material
      ↓
Preserve facts, scope, uncertainty, and relationships
      ↓
Diagnose the comprehension bottleneck
      ↓
Choose the minimum sufficient representation
      ↓
Text → Table → Diagram Type → Interactive → Animation/Video
      ↓
Verify semantic fidelity
      ↓
If the reader is still confused, change the explanation path
```

The sequence above is an **expression capability ladder**, not a mandatory pipeline. The skill may skip levels, stay at one level, or downgrade to a simpler representation when that is clearer.

## Core idea

The skill follows four principles:

1. **Source Fidelity** — preserve numbers, units, attribution, negation, scope, prerequisites, uncertainty, and the difference between correlation and causation.
2. **Minimum Sufficient Representation** — use the simplest form that solves the current comprehension problem; do not generate every format by default.
3. **Representation Fit** — choose the medium based on the information structure, not on visual novelty.
4. **Progressive Escalation** — if the reader still does not understand, change the explanation path instead of merely adding more words.

A useful mental model is:

```text
Understanding
= Source Fidelity
× Representation Fit
× Explanation Quality
```

If any factor is close to zero, the explanation fails even if the output looks polished.

## Representation decision tree

| Comprehension need | Default representation |
| --- | --- |
| A concept, claim, mechanism, evidence boundary | **Text** |
| A/B/C comparison using shared dimensions | **Table** |
| Components and modules | **Architecture / Block diagram** |
| Sequence, branching, retry, AND/OR conditions | **Flowchart** |
| Cross-role handoffs and responsibility | **Swimlane** |
| Classification and hierarchy | **Tree / Hierarchy** |
| Supported causal chains and feedback loops | **Causal diagram** |
| Data movement through a system | **Data-flow diagram** |
| Events or version evolution over time | **Timeline** |
| Many-to-many relationships | **Network graph** |
| Trends, distributions, or numeric relationships | **Chart** |
| Changing parameters or scenarios | **Interactive** |
| Time evolution, state transitions, step-by-step execution | **Animation / Video** |

For the full routing rules, see [`references/representation-decision-tree.md`](references/representation-decision-tree.md).

## What makes it different from a normal “explain this” prompt

Adaptive Understanding does not assume that simpler wording is always the answer. A reader may be blocked by different problems:

- an unfamiliar term → explain with Text;
- too many alternatives mixed in paragraphs → use a Table;
- invisible sequence or branching logic → use a Flowchart;
- unclear ownership across human and AI agents → use a Swimlane;
- a parameter-dependent relationship → build an Interactive explanation;
- a process that only makes sense over time → use Animation/Video.

It also stops escalating when the source itself does not contain the answer. A more sophisticated visualization must not hide missing evidence.

## Epistemic safety

This skill separates **clarity** from **truth**.

A polished diagram, slider, animation, or video can make unsupported claims feel more credible. Therefore:

- every important relationship should be traceable to the source;
- unknown information stays unknown;
- missing information is not converted into a neat assumption silently;
- causal arrows require causal support;
- interactive formulas require a source, rule, code path, or an explicit “teaching assumption” label;
- animation must represent real state changes, not decorative motion.

## Simplified Technical English inspiration

The skill borrows selected clarity principles from **ASD-STE100 Simplified Technical English**, especially stable terminology, reduced syntactic ambiguity, and concise procedural writing. It does **not** claim formal ASD-STE100 compliance or certification.

Chinese explanations adapt the intent of STE instead of mechanically translating English word-count limits into Chinese character-count limits.

See [`references/ste-and-chinese.md`](references/ste-and-chinese.md) and [`references/sources.md`](references/sources.md).

## Examples

The repository includes examples that demonstrate the routing approach:

- [`examples/flow.svg`](examples/flow.svg) — preserves parallel checks, AND conditions, failure branches, loops, and human review.
- [`examples/parallel-demo.html`](examples/parallel-demo.html) — interactive teaching model for parallel processing using an explicit formula and assumptions.
- [`examples/process-animation.html`](examples/process-animation.html) — playable step-by-step process animation with play, pause, previous, next, and restart controls.
- [`examples/animation-storyboard.md`](examples/animation-storyboard.md) — storyboard fallback for environments that cannot render video directly.
- [`examples/walkthrough.md`](examples/walkthrough.md) — walkthrough of multiple output forms.

## Acceptance tests

The skill includes acceptance cases covering:

- evidence scope and overgeneralization;
- table-vs-diagram routing;
- diagram type selection;
- parallel vs sequential semantics;
- unsupported causality;
- invented formulas;
- animation semantics;
- over-generation;
- downgrade behavior when a complex visual makes understanding worse.

See [`references/acceptance-cases.md`](references/acceptance-cases.md).

## Repository structure

```text
adaptive-understanding/
├── README.md
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

## Inspiration and references

The main product inspiration for this skill is Andrej Karpathy's post about using different output modalities to make LLM-generated information easier for humans to understand:

- **Andrej Karpathy — X post:** https://x.com/karpathy/status/2105819303471976479

Adaptive Understanding extends that idea into a routing system: **Text → Table → Diagram Type → Interactive → Animation/Video**, with source fidelity, epistemic boundaries, progressive escalation, and acceptance tests added as first-class requirements.

Additional references include:

- ASD-STE100 Simplified Technical English: https://www.asd-ste100.org/
- ASD-STE100 Issue 9: https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf

For detailed provenance and boundaries, see [`references/sources.md`](references/sources.md).

## License

This project is released under the **MIT License**. See [`LICENSE`](LICENSE) for details.

## Status

This repository contains the **Adaptive Understanding V2** skill specification and examples. It is designed to be host-agnostic: different AI environments may provide different capabilities for file reading, diagram rendering, HTML generation, animation, and video generation.

The skill should degrade gracefully when a host lacks a modality rather than pretending an artifact was generated or verified.
