---
name: artifact-pyramids
description: >-
  Progressive disclosure for what AI agents produce. Structure research outputs
  across three fidelity layers — Raw Sources & Atoms, Molecules & Syntheses,
  and Published Artifacts — so downstream agents and humans consume only as
  deeply as they need. Load this skill when organizing research outputs,
  building agentic research pipelines, or designing agent collaboration
  protocols.
license: MIT
compatibility: Agent-agnostic — concepts apply to any AI agent workflow. Scripts require Python 3.9+ and a POSIX shell.
metadata:
  spec-version: "1.0"
  source: https://github.com/groktopus/artifact-pyramids
---

# Artifact Pyramids for Agentic AI Research

Progressive disclosure governs how we feed agents context. **The Artifact Pyramid extends the same principle to what agents produce.** Three layers, from atom to artifact, each consumable at its own depth.

## The Pyramid

```
          ┌─────────┐
          │ Layer 3 │  Published Artifacts
          │   🎯    │  Articles, presentations, specs, decisions
          └────┬────┘
          ┌────┴────┐
          │ Layer 2 │  Molecules & Syntheses
          │   🧩    │  Connected narratives, cross-referenced knowledge
          └────┬────┘
    ┌──────────┴──────────┐
    │     Layer 1          │  Raw Sources & Atoms
    │      📦              │  Captured pages, PDFs, transcripts, atomic facts
    └─────────────────────┘
```

The pyramid is consumed top-down (human reads the article, drills to molecules for claims, atoms for sources) but produced bottom-up (collect sources, extract atoms, synthesize molecules, polish into artifacts).

## Reference Files

| Reference | Load when | File |
|-----------|-----------|------|
| Framework & Philosophy | You need the full conceptual foundation — why this exists and what problems it solves | `references/artifact-pyramid-framework.md` |
| Pipeline Stages | You're building or running a research pipeline — detailed transformation rules per layer | `references/pipeline-stages.md` |
| Quality Gates | You need to verify that an artifact meets the standard for its layer | `references/quality-gates.md` |
| Worked Example | You want to see a complete synthetic walkthrough of all three layers | `references/synthetic-example.md` |

## Scripts

| Script | Load when | File |
|--------|-----------|------|
| pyramid-status | You want to audit an existing research directory for pyramid coverage and gaps | `scripts/pyramid-status.sh` |
| extract-atoms | You have raw source text and need to split it into atomic claims | `scripts/extract-atoms.py` |

## Templates

| Template | Load when | File |
|----------|-----------|------|
| Project Scaffold | You're starting a new research project and need the directory skeleton | `assets/pyramid-template.md` |
| Artifact Inventory | You need to track what exists at each layer across a research project | `assets/artifact-inventory.md` |

## Quick Start

```bash
# Scaffold a new research project
cp -r assets/pyramid-template.md ./my-project/00-index.md

# Check pyramid health of an existing project
scripts/pyramid-status.sh ./my-project

# Extract atoms from source text
scripts/extract-atoms.py ./my-project/01-sources/paper-1.txt
```

## Key Principles

1. **Progressive disclosure is symmetric.** The same principle that governs context injection governs artifact structure.
2. **Each layer is independently consumable.** An article (Layer 3) should make sense on its own; a molecule (Layer 2) should be useful without the published artifact.
3. **Atoms are recombination primitives.** They are true without their source context — their value is in being recombined into novel syntheses.
4. **Quality gates are directional.** Material moves up the pyramid only when it meets the gate for the target layer.
5. **Downward navigation is explicit.** Every Layer 3 artifact should trace back to the Layer 2 molecules and Layer 1 atoms that support it.

## When NOT to use

- Single-turn Q&A with no research artifacts to preserve
- Tasks producing only ephemeral output (one-off calculations, quick lookups)
- Workflows where the output IS the source (e.g., you're just collecting data, not synthesizing)
