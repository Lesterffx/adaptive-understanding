# Adaptive Understanding

> An adaptive understanding skill that diagnoses **why a reader is confused** and chooses the minimum sufficient representation instead of generating more content by default.
>
> Core path: **Text → Table → Diagram Type → Interactive → Animation/Video**

[中文 README](README.md)

## Why this skill exists

AI can generate more text, diagrams, webpages, animations, and videos than a person can reasonably consume. The harder problem is increasingly not only **generation**, but **understanding**: how to present the same source material in a form that lowers cognitive load without changing the facts.

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

This is an expression capability ladder, not a mandatory pipeline. The skill may skip levels, stay at one level, or downgrade to a simpler representation when that is clearer.

## Core principles

1. **Source Fidelity** — preserve numbers, units, attribution, negation, scope, prerequisites, uncertainty, and the difference between correlation and causation.
2. **Minimum Sufficient Representation** — use the simplest form that solves the current comprehension problem.
3. **Representation Fit** — choose the medium based on the information structure, not visual novelty.
4. **Progressive Escalation** — if the reader still does not understand, change the explanation path instead of merely adding more words.

```text
Understanding
= Source Fidelity
× Representation Fit
× Explanation Quality
```

## Representation decision tree

| Comprehension need | Default representation |
| --- | --- |
| Concept, claim, mechanism, evidence boundary | **Text** |
| A/B/C comparison with shared dimensions | **Table** |
| Components and modules | **Architecture / Block Diagram** |
| Sequence, branching, retry, AND/OR | **Flowchart** |
| Cross-role handoffs and responsibility | **Swimlane** |
| Classification and hierarchy | **Tree / Hierarchy** |
| Supported causal chains and feedback loops | **Causal Diagram** |
| Data movement | **Data-flow Diagram** |
| Events or version evolution over time | **Timeline** |
| Many-to-many relationships | **Network Graph** |
| Trends, distributions, numeric relationships | **Chart** |
| Changing parameters or scenarios | **Interactive** |
| Time evolution and step-by-step execution | **Animation / Video** |

See [`references/representation-decision-tree.md`](references/representation-decision-tree.md) for the full routing rules.

## What makes it different from a normal explain prompt

Adaptive Understanding does not assume that simpler wording is always the answer:

- unfamiliar term → **Text**
- alternatives buried in paragraphs → **Table**
- invisible sequence or branching logic → **Flowchart**
- unclear ownership across humans and agents → **Swimlane**
- parameter-dependent behavior → **Interactive**
- a process that only makes sense over time → **Animation / Video**

If the source itself does not contain the answer, the skill stops escalating and states the evidence gap instead of hiding it behind a more polished visualization.

## Epistemic safety

Clarity is not the same as truth. A polished diagram, slider, animation, or video can make unsupported claims feel more credible. Therefore:

- important relationships should be traceable to the source;
- unknown information stays unknown;
- missing information is not silently converted into assumptions;
- causal arrows require causal support;
- interactive formulas require a source, rule, code path, or an explicit teaching-assumption label;
- animation must represent real state changes rather than decorative motion.

## ASD-STE100 inspiration

The skill borrows selected clarity principles from **ASD-STE100 Simplified Technical English**, including stable terminology, reduced syntactic ambiguity, and concise procedural writing. It does **not** claim formal ASD-STE100 compliance or certification.

Chinese explanations adapt the intent of STE instead of mechanically translating English word-count limits into Chinese character-count limits.

See [`references/ste-and-chinese.md`](references/ste-and-chinese.md) and [`references/sources.md`](references/sources.md).

## Examples

- [`examples/flow.svg`](examples/flow.svg) — parallel checks, AND conditions, failure branches, loops, and human review.
- [`examples/parallel-demo.html`](examples/parallel-demo.html) — interactive teaching model with explicit formulas and assumptions.
- [`examples/process-animation.html`](examples/process-animation.html) — playable step-by-step process animation.
- [`examples/animation-storyboard.md`](examples/animation-storyboard.md) — storyboard fallback when video rendering is unavailable.
- [`examples/walkthrough.md`](examples/walkthrough.md) — walkthrough across Text, Table, Diagram, Interactive, and Animation.

## Acceptance tests

The repository includes acceptance cases covering evidence scope, overgeneralization, routing decisions, diagram selection, parallel-vs-sequential semantics, unsupported causality, invented formulas, animation semantics, over-generation, and downgrade behavior.

See [`references/acceptance-cases.md`](references/acceptance-cases.md).

## Inspiration and references

The main product inspiration is Andrej Karpathy's post about using different output modalities to make LLM-generated information easier for humans to understand:

- **Andrej Karpathy — X post:** https://x.com/karpathy/status/2105819303471976479

Adaptive Understanding extends that idea into **Text → Table → Diagram Type → Interactive → Animation/Video**, with Source Fidelity, Epistemic Safety, Minimum Sufficient Representation, Progressive Escalation, Diagram Type Routing, and Acceptance Tests added as first-class requirements.

Additional references:

- ASD-STE100 Simplified Technical English: https://www.asd-ste100.org/
- ASD-STE100 Issue 9: https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf

## License

This project is released under the **MIT License**. See [`LICENSE`](LICENSE).

## Status

This repository contains the **Adaptive Understanding V2** skill specification and examples. It is designed to be host-agnostic and should degrade gracefully when a host lacks a modality rather than pretending an artifact was generated or verified.
