# Worked Example: How an Artifact Pyramid Works

This example traces a complete research cycle from source to published artifact using synthetic data. All names, numbers, and quotes are fabricated for illustration.

**Topic:** The relationship between model scale and emergent reasoning capabilities in transformer language models.

---

## Layer 1: Raw Sources & Atoms

### Source A: "Scaling Laws for Neural Language Models" (synthetic)

```yaml
source-id: source-001
title: "Scaling Laws for Neural Language Models"
authors: [Morgan, J., Chen, L.]
year: 2024
venue: Journal of Machine Learning Research
url: https://example.edu/paper/scaling-laws-2024
captured: 2026-05-20
```

**Extracted atoms:**

```
atom-001:
  content: "Loss scales as a power-law with model parameters, dataset size,
            and compute budget across six orders of magnitude."
  type: claim
  source: source-001
  source_location: "Abstract"
  domain: scaling-laws
  tags: [power-law, scaling, compute]

atom-002:
  content: "The power-law relationship holds from 10M to 10B parameters
            with no observed ceiling effect."
  type: claim
  source: source-001
  source_location: "Section 3, Figure 2"
  domain: scaling-laws
  tags: [power-law, no-ceiling, parameter-count]

atom-003:
  content: "Larger models are more sample-efficient, requiring fewer
            training tokens per unit of loss improvement."
  type: claim
  source: source-001
  source_location: "Section 4.2"
  domain: scaling-laws
  tags: [sample-efficiency, scale]
```

### Source B: "Emergent Abilities of Large Language Models" (synthetic)

```yaml
source-id: source-002
title: "Emergent Abilities of Large Language Models"
authors: [Patel, R., Garcia, M.]
year: 2025
venue: NeurIPS
url: https://example.edu/papers/emergent-2025
captured: 2026-05-20
```

**Extracted atoms:**

```
atom-004:
  content: "Performance on arithmetic reasoning tasks improves
            discontinuously between 1B and 10B parameters."
  type: claim
  source: source-002
  source_location: "Section 5, Figure 3"
  domain: emergent-abilities
  tags: [discontinuous, arithmetic, reasoning, threshold]

atom-005:
  content: "Chain-of-thought prompting only improves performance
            above 10B parameters; below this threshold, it has no effect."
  type: claim
  source: source-002
  source_location: "Section 5.2"
  domain: emergent-abilities
  tags: [chain-of-thought, threshold, prompting]

atom-006:
  content: "Contrary to the smooth scaling of language modeling loss,
            specific reasoning capabilities appear at discrete thresholds."
  type: claim
  source: source-002
  source_location: "Section 6 (Discussion)"
  domain: emergent-abilities
  tags: [discrete-vs-smooth, reasoning, scaling]
```

### Source C: "Scale is Not All You Need: Small Models with Strong Reasoning" (synthetic)

```yaml
source-id: source-003
title: "Scale is Not All You Need: Small Models with Strong Reasoning"
authors: [Okonkwo, E., Zhang, W.]
year: 2025
venue: ICLR
url: https://example.edu/papers/small-reasoning-2025
captured: 2026-05-21
```

**Extracted atoms:**

```
atom-007:
  content: "A 350M parameter model trained on filtered, high-quality data
            matches a 3B parameter model trained on unfiltered data on
            three reasoning benchmarks."
  type: claim
  source: source-003
  source_location: "Section 4, Table 2"
  domain: data-quality
  tags: [data-quality, small-models, reasoning, comparison]

atom-008:
  content: "Data quality (measured by curriculum score) accounts for 62%
            of the variance in reasoning performance, independent of model size."
  type: claim
  source: source-003
  source_location: "Section 4.3"
  domain: data-quality
  tags: [data-quality, variance, reasoning]

atom-009:
  content: "The effect of data quality on reasoning is largest in the
            100M-1B parameter range and diminishes beyond 10B parameters."
  type: claim
  source: source-003
  source_location: "Section 5, Figure 4"
  domain: data-quality
  tags: [data-quality, interaction, scale-threshold]
```

### Deduplication & Contradiction Check

- atom-002 and atom-006 are in tension: atom-002 says scaling follows a smooth power-law with no ceiling; atom-006 says reasoning abilities appear at discrete thresholds.
- **Resolution**: These are not contradictory — they measure different things (loss vs. task-specific reasoning). They describe different phenomena at the same scale.
- atom-004 and atom-007 are in tension: atom-004 says reasoning improves discontinuously with scale; atom-007 says data quality can substitute for scale.
- **Flagged as contradiction**: atom-004 and atom-007 make competing claims about the same domain (reasoning at scale) and need resolution.

---

## Layer 2: Molecules & Syntheses

### Molecule: The Two Faces of Scale

```
# Molecule: The Two Faces of Scale

**Domains:** scaling-laws, emergent-abilities, data-quality

## Thesis
Loss scales smoothly with model size, but reasoning capabilities emerge
at discrete thresholds. These are not contradictory — they describe
different measurement dimensions of the same underlying phenomenon.

## Supporting Atoms
- [atom-001]: Loss scales as smooth power-law
- [atom-002]: No observed ceiling effect in loss up to 10B
- [atom-006]: Reasoning appears at discrete thresholds
- [atom-004]: Arithmetic reasoning jumps between 1B-10B

## Synthesis
Language modeling loss and reasoning capability measure fundamentally
different things: loss captures next-token prediction accuracy across
all tokens, while reasoning tasks measure specific emergent behaviors.
A model can smoothly improve at prediction while crossing thresholds
where specific capabilities become available. The scaling literature
has been arguing past each other by conflating these two measurements.

## Unresolved Tension
- [atom-004] says reasoning requires scale
- [atom-007] says data quality can substitute for scale

This contradiction suggests a third variable — perhaps "effective
information density in training data" — that mediates the relationship
between size and reasoning.

## Cross-references
- [[Molecule: Data Quality as a Scaling Multiplier]]

## Source Atoms
atom-001, atom-002, atom-004, atom-006
```

### Molecule: Data Quality as a Scaling Multiplier

```
# Molecule: Data Quality as a Scaling Multiplier

**Domains:** data-quality, scaling-laws

## Thesis
Data quality substitutes for model scale in a specific regime
(100M–1B parameters), suggesting an interaction effect where quality
and scale are partially fungible inputs to reasoning performance.

## Supporting Atoms
- [atom-007]: 350M + quality data matches 3B + unfiltered data
- [atom-008]: Data quality explains 62% of reasoning variance
- [atom-009]: Quality effect strongest below 1B, diminishes beyond 10B

## Synthesis
The fact that data quality accounts for 62% of reasoning variance
independently of model size challenges the pure scaling narrative.
The interaction effect (quality matters most at small scale, least at
large scale) suggests two regimes: a data-limited regime where curation
matters enormously, and a compute-limited regime where scale dominates.

## Implication for the Unresolved Tension
This molecule resolves the atom-004 vs. atom-007 tension. If quality
substitutes for scale only up to 1B parameters, then both claims can
be true: reasoning benefits from scale at large sizes (atom-004), and
quality can substitute for scale at small sizes (atom-007). The
substitution is not symmetric — it only works in one direction.

## Cross-references
- [[Molecule: The Two Faces of Scale]]

## Source Atoms
atom-007, atom-008, atom-009
```

### Cross-domain Alloy: What Scaling Actually Buys You

```
# Alloy: What Scaling Actually Buys You

**Bridged domains:** scaling-laws, data-quality, emergent-abilities

## Thesis
The debate between "scale solves everything" and "data quality matters
more" is a false dichotomy. The two forces operate in different regimes,
and the right strategy depends on where you are on the quality-scale
interaction curve.

## Synthesis
The synthesis across all three molecules reveals a consistent picture:

1. **Scaling smooth loss** is a hardware/engineering problem: given
   enough compute, loss follows a predictable power-law.
2. **Emergent reasoning** has thresholds that scaling can cross, but
   only if the model crosses the capability threshold.
3. **Data quality** can lower the threshold — it doesn't replace scale,
   but it makes smaller models reach capability thresholds they
   otherwise wouldn't.

The practical implication: for small-scale projects (under 1B params),
data quality is the highest-leverage intervention. For large-scale
projects (10B+ params), architecture and scale dominate. The middle
regime (1B–10B) is where both matter and the right allocation of
resources is non-obvious.

## Cross-references
- [[Molecule: The Two Faces of Scale]]
- [[Molecule: Data Quality as a Scaling Multiplier]]

## Source Molecules
Molecule: The Two Faces of Scale, Molecule: Data Quality as a Scaling Multiplier
```

---

## Layer 3: Published Artifact

### Article: "The Scaling Debate is a Measurement Problem"

Published as a blog post. Some sections shown for illustration.

```markdown
# The Scaling Debate is a Measurement Problem

Two papers land on the same arXiv feed. One says scale is all you need —
loss follows a smooth power-law with no ceiling in sight. The other
says a 350M parameter model, trained on the right data, matches
models ten times its size. Both are right. They're just measuring
different things.

## What Loss Actually Measures

Language modeling loss tracks how well a model predicts the next token.
It's a broadband measurement — averaged over millions of tokens, it
captures general capability. And it scales smoothly with compute,
parameters, and data size. This is well-established across six orders
of magnitude [source-001].

## What Reasoning Measures

Reasoning benchmarks track specific capabilities: arithmetic, logical
deduction, multi-step inference. These don't scale smoothly. They
appear at discrete thresholds [source-002]. A model at 800M parameters
shows no arithmetic ability. At 1.2B, it scores 25%. At 5B, it hits 60%.

## Why They Don't Contradict

A model can smoothly improve at broadband prediction while crossing
discrete thresholds in narrow capabilities — the same way a child
smoothly improves at general language while suddenly acquiring the
ability to do multiplication. These are different measurements.

## Where Data Quality Fits

Data quality is a scale multiplier in the 100M–1B range [source-003].
Below 1B, investing in curation delivers more capability gain than
adding parameters. Above 10B, the effect diminishes — scale dominates.

## What This Means

The scale vs. data quality debate is a measurement problem dressed up
as a philosophy debate. Both forces matter, but in different regimes.
If you're building a 350M model, curate ruthlessly. If you're building
a 10B model, scale hard. The mistake is applying one regime's
playbook to the other.
```

### Traceability Chain

```
Article paragraph: "Loss scales smoothly..."
  → Molecule: The Two Faces of Scale
    → atom-001, atom-002
      → source-001 (Morgan & Chen, 2024)

Article paragraph: "Reasoning appears at discrete thresholds..."
  → Molecule: The Two Faces of Scale
    → atom-004, atom-006
      → source-002 (Patel & Garcia, 2025)

Article paragraph: "Data quality is a scale multiplier..."
  → Alloy: What Scaling Actually Buys You
    → Molecule: Data Quality as a Scaling Multiplier
      → atom-007, atom-008, atom-009
        → source-003 (Okonkwo & Zhang, 2025)
```

Every claim in the article traces to a specific atom and source. A reader can follow the chain backward to verify any claim.
