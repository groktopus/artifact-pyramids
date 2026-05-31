# The Artifact Pyramid: Framework & Philosophy

## The Idea

Progressive disclosure governs how we feed AI agents context: start with metadata, expand to instructions on activation, and load resources on demand. **The Artifact Pyramid extends the same principle to what agents produce.**

Just as an agent should never be flooded with irrelevant context, a downstream consumer — whether human or agent — should never have to wade through raw source dumps to find the synthesized insight. The Artifact Pyramid structures research outputs into three layers, each independently consumable:

```
            ┌─────────────┐
            │  Layer 3     │  Published Artifacts
            │  🎯          │  (articles, presentations, specs)
            └──────┬──────┘
              ┌────┴────┐
              │ Layer 2 │  Molecules & Syntheses
              │  🧩     │  (connected narratives, domain syntheses)
              └────┬────┘
        ┌──────────┴──────────┐
        │     Layer 1          │  Raw Sources & Atoms
        │      📦              │  (captured pages, PDFs, extracts, atomic facts)
        └─────────────────────┘
```

## Why This Exists

### The asymmetry problem

In current AI agent workflows, instructions use progressive disclosure but outputs don't. An agent receives:

1. **Metadata** (~100 tokens): `name` and `description` of available skills
2. **Instructions** (<5000 tokens): The full skill body when activated
3. **Resources** (on demand): Reference files loaded when needed

But it *produces* a single flat response — a monolithic artifact containing everything from raw data to final conclusion. The consumer (human or downstream agent) has no way to access intermediate knowledge without re-processing everything.

The Artifact Pyramid fixes this by applying the same layered structure to outputs. A downstream agent consuming an artifact pyramid can:

1. **Read the Layer 3 artifact** (quick scan — is this relevant?)
2. **Drill to Layer 2 molecules** (deeper — what claims support this?)
3. **Drill to Layer 1 atoms and sources** (deepest — where does this claim come from?)

### The multi-agent problem

When multiple agents collaborate in a research pipeline, each agent produces artifacts at a different layer:
- A **researcher agent** collects sources and extracts atoms (Layer 1)
- A **synthesizer agent** connects atoms into narratives (Layer 2)
- A **writer agent** polishes narratives into published output (Layer 3)

Without the pyramid, each agent's output is a flat document that the next agent must re-parse. With the pyramid, the handoff is structured: the researcher deposits atoms with source attribution, the synthesizer reads atoms and produces molecules, the writer reads molecules and produces articles. Each layer is the *contract* between agents.

### The traceability problem

In research-driven decision-making, every claim in a final artifact needs to trace back to its source. The pyramid makes this explicit:

```
Published Article
  → claims in article reference Molecule-IDs
    → Molecules reference Atom-IDs
      → Atoms reference Source-IDs (URLs, PDF paths, timestamps)
```

This creates an auditable chain from conclusion back to evidence — essential for fact-checking, peer review, and accountable AI research.

## Symmetry with Progressive Disclosure

| Input Side (how agents learn) | Output Side (how agents produce) |
|---|---|
| **Metadata:** skill names and descriptions | **Layer 3:** published artifacts (headline-level) |
| **Instructions:** full skill body on activation | **Layer 2:** molecules and syntheses (detail-level) |
| **Resources:** reference files loaded on demand | **Layer 1:** raw sources and atoms (source-level) |

The symmetry is deliberate: the same architect
ural principle governs both directions of information flow.

## Relationship to Other Frameworks

### DIKW Pyramid (Ackoff 1989)

The Artifact Pyramid is inspired by the Data → Information → Knowledge → Wisdom hierarchy, but adapted for agentic AI research:

| DIKW | Artifact Pyramid |
|---|---|
| Data | Raw sources (captured pages, PDFs, transcripts) |
| Information | Extracted atoms (individual claims, facts, quotes) |
| Knowledge | Molecules (connected narratives, domain syntheses) |
| Wisdom | Published artifacts (actionable insights, decisions) |

The key difference: the Artifact Pyramid is not a philosophy of knowledge — it's a **pipeline architecture** with explicit handoffs, quality gates, and bidirectional navigation.

### Zettelkasten / Atomic Notes

The Artifact Pyramid's atom layer shares principles with the Zettelkasten method (Luhmann, Ahrens, Matuschak):
- Atoms are atomic — one claim per unit
- Atoms are recombination primitives — their value is in novel connections
- Connections between atoms create molecules

But the pyramid adds:
- Explicit quality gates between layers
- Bidirectional traceability (top-down consumption, bottom-up production)
- An agent-aware structure (not just human-readable)

### Software Build Pipelines

Source → compiled → linked → packaged → deployed mirrors the pyramid's Raw Sources → Atoms → Molecules → Published Artifacts. Each stage transforms the artifact and adds quality guarantees. The pyramid borrows the concept of:
- **Build stages** with clear inputs and outputs
- **Artifact registries** (the inventory tracker)
- **Dependency chains** (molecules depend on atoms, articles depend on molecules)

## When the Pyramid Breaks

The pyramid is a tool, not a dogma. It breaks when:

1. **The output is ephemeral.** A one-off calculation or quick lookup doesn't need layered artifact structure — the cost of extraction exceeds the value.
2. **The source IS the output.** When you're collecting data without synthesizing (e.g., a dataset of sensor readings), the pyramid collapses to a single layer.
3. **The consumer is always the same agent.** If the same agent consumes and produces, the overhead of structured handoffs may not justify itself.
4. **The output is tiny.** A three-sentence answer doesn't need three layers.

Use the pyramid when: research depth > 5 sources, multi-agent handoffs are involved, or outputs need to be auditable and reusable.
