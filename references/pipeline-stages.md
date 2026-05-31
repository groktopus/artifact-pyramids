# Pipeline Stages: The Three Layers in Detail

## Overview

The Artifact Pyramid has three layers. Material flows **bottom-up** during production (collect → extract → synthesize → polish). Consumers navigate **top-down** during consumption (read → drill → verify).

```
PRODUCTION FLOW (bottom-up)

  Layer 3 ┌───────────────────────────────────────────┐
          │  Polish: molecules → publishable artifacts  │
          └───────────────────────┬───────────────────┘
  Layer 2 ┌───────────────────────┴───────────────────┐
          │  Synthesize: atoms → connected narratives   │
          └───────────────────────┬───────────────────┘
  Layer 1 ┌───────────────────────┴───────────────────┐
          │  Collect + Extract: sources → atoms         │
          └───────────────────────────────────────────┘


CONSUMPTION FLOW (top-down)

  Layer 3 ┌───────────────────────────────────────────┐
          │  Scan: does this artifact answer my         │
          │  question?                                  │
          └───────────────────────┬───────────────────┘
  Layer 2 ┌───────────────────────┴───────────────────┐
          │  Study: what claims support this?           │
          │  Are they well-supported?                   │
          └───────────────────────┬───────────────────┘
  Layer 1 ┌───────────────────────┴───────────────────┐
          │  Verify: where does this claim come from?   │
          │  Is the source reliable?                    │
          └───────────────────────────────────────────┘
```

---

## Layer 1: Raw Sources & Atoms

### Purpose
Establish the evidentiary foundation. Every claim in the upper layers must trace back to a specific atom and source.

### Inputs
- Web pages, PDFs, academic papers, transcripts, logs, datasets
- Any raw material from which knowledge can be extracted

### Transformations

| Transformation | Description | Example |
|---|---|---|
| **Capture** | Fetch and preserve source material with metadata | `get paper.pdf → paper.pdf + paper-metadata.json` |
| **Extract** | Pull atomic claims, facts, quotes, and data points | `paper.pdf → atom-001: "Model X achieves 94.2% accuracy on benchmark Y"` |
| **Classify** | Tag atoms with domain, type (fact/quote/claim/data), source reference | `atom-001 → {domain: "nlp", type: "claim", source: "paper.pdf", tags: ["accuracy", "benchmark"]}` |
| **Deduplicate** | Merge identical claims from different sources, flag contradictions | `source-A says X, source-B says not-X → flag contradiction` |

### Outputs
- **Sources**: Captured files with metadata (URL, timestamp, title, author)
- **Atoms**: Individual knowledge units, each a single context-independent claim
- **Atom Registry**: A directory or inventory file mapping atom IDs to sources

### Atom Format

```yaml
atom-001:
  content: "Model X achieves 94.2% accuracy on benchmark Y"
  type: claim
  domain: natural-language-processing
  source: paper-001
  source_location: "Section 4.2, Table 1"
  tags: [accuracy, benchmark, model-x]
  contradictions: []
  extracted_at: 2026-05-31
```

### Quality Gate (to pass to Layer 2)

- [ ] Each atom contains exactly one claim or fact
- [ ] Each atom is context-independent (makes sense without its source)
- [ ] Each atom has a source reference
- [ ] Atoms are deduplicated (no identical claims from different sources)
- [ ] Known contradictions are flagged
- [ ] Atoms are classified by domain

### Common Pitfalls

- **Composite atoms**: "Model X is fast, accurate, and energy-efficient" is three atoms, not one
- **Context-dependent atoms**: "This finding was significant" — significant according to whom, in what context?
- **Missing source attribution**: An atom without a source cannot be verified
- **Premature synthesis**: Extracting interpretations instead of observations ("The data suggests..." rather than "The data shows X=0.94")

---

## Layer 2: Molecules & Syntheses

### Purpose
Transform atoms into connected, interpretive narratives. A molecule is a structured synthesis that produces understanding a single atom cannot provide.

### Inputs
- Atoms from Layer 1 (the raw material)
- Existing molecules (for cross-domain alloys)
- Domain knowledge and analytical frameworks

### Transformations

| Transformation | Description | Example |
|---|---|---|
| **Cluster** | Group related atoms by domain, theme, or argument | Collect all atoms about "attention mechanisms" |
| **Connect** | Link atoms causally, contrastively, or hierarchically | "Atom A (attention improves recall) → Atom B (attention is expensive) → trade-off" |
| **Interpret** | Add analytical context — what these atoms mean together | "The attention-efficiency trade-off suggests a Pareto frontier" |
| **Cross-link** | Connect to molecules from other domains | "This same trade-off appears in neuromorphic computing" |

### Outputs
- **Molecules**: Structured documents that synthesize atoms into arguments
- **Cross-domain Alloys**: Molecules that bridge two or more domains
- **Synthesis Map**: A graph showing how atoms connect within and across molecules

### Molecule Format

Each molecule is a markdown document with:

```markdown
# Molecule: The Attention-Efficiency Trade-off

**Domains:** natural-language-processing, hardware-optimization

## Thesis
Transformer attention improves recall but the quadratic cost
creates a fundamental efficiency ceiling.

## Supporting Evidence
- [atom-023]: Attention mechanism recall improvement (83→94%)
- [atom-047]: Self-attention is O(n²) in sequence length
- [atom-089]: Sparse attention reduces cost to O(n log n)

## Synthesis
The attention literature reveals a consistent pattern: architectural
improvements that boost recall consistently increase computational
cost. This is not a bug to be fixed but a fundamental trade-off
governed by the information-theoretic limits of the attention
mechanism. Sparse and linear attention variants don't eliminate the
trade-off; they shift where on the Pareto frontier you operate.

## Cross-references
- [[Molecule: Efficient Transformer Architectures]]
- [[Molecule: Information Theory in Deep Learning]]

## Source Atoms
atom-023, atom-047, atom-089, atom-112, atom-143
```

### Quality Gate (to pass to Layer 3)

- [ ] Molecule makes at least one claim no constituent atom makes individually
- [ ] Every claim in the molecule traces to specific atoms
- [ ] No leaps unsupported by atoms (if you're guessing, say so)
- [ ] Cross-references to related molecules are explicit
- [ ] Conflicting evidence is surfaced, not buried
- [ ] The synthesis adds value beyond its atoms (re-formatting isn't synthesis)

### Common Pitfalls

- **Atom restatement**: A molecule that just paraphrases its atoms in paragraph form isn't synthesis — it's formatting
- **Unsupported claims**: "This proves that..." when the atoms only suggest correlation
- **Domain isolation**: Failing to cross-reference related molecules leaves insight on the table
- **Synthesis by omission**: Cherry-picking only supporting atoms and ignoring contradicting ones

---

## Layer 3: Published Artifacts

### Purpose
Deliver the synthesized knowledge to an audience. Articles, presentations, reports, documentation, and decisions that are complete, polished, and actionable.

### Inputs
- Molecules from Layer 2
- Cross-domain alloys
- Audience requirements (who will consume this, and in what format)

### Transformations

| Transformation | Description | Example |
|---|---|---|
| **Synthesize** | Select and order molecules for narrative flow | Pick 3 molecules that tell a coherent story |
| **Polish** | Write in the target voice, add examples, adjust for audience | Convert research notes → blog post tone |
| **Review** | Fact-check claims against source atoms, copy-edit | Every claim traces back through molecule → atom → source |
| **Format** | Render in the output medium | Markdown → HTML → Ghost CMS, or slides → presentation |
| **Publish** | Version, release, and announce | Git tag + GitHub release + social media |

### Outputs
- **Articles**: Blog posts, papers, essays (one artifact = one coherent argument)
- **Presentations**: Slides, talks, demos
- **Specifications**: Design docs, architecture decisions, technical RFCs
- **Reports**: Analysis documents, findings briefs, decision memos
- **Code**: Libraries, tools, implementations derived from research

### Quality Gate (for delivery)

- [ ] Artifact is appropriate for its intended audience
- [ ] Every factual claim traces back to a Layer 2 molecule (which traces to Layer 1 atoms)
- [ ] Conflicting evidence is addressed (not hidden)
- [ ] The artifact is self-consistent and internally coherent
- [ ] Format meets the target platform's standards
- [ ] The artifact is versioned and discoverable

### Common Pitfalls

- **Missing traceability**: Claims in the article that can't be traced to molecules or atoms
- **Audience mismatch**: Writing for domain experts when the audience is general (or vice versa)
- **Over-condensation**: Removing so much context that the artifact becomes misleading
- **Silver bullet syndrome**: One study doesn't prove a rule — the pyramid should prevent this by requiring cross-referenced molecules

---

## Cross-layer Navigation

### Top-Down (Consumption)

```
Article: "Attention mechanisms are approaching fundamental limits"
  ↓ reads
Molecule: The Attention-Efficiency Trade-off
  ↓ follows trace
Atom-047: "Self-attention is O(n²) in sequence length"
  ↓ verifies source
Source: "Efficient Transformers: A Survey" (Tay et al., 2022)
```

### Bottom-Up (Production)

```
Source: "Efficient Transformers" paper
  ↓ extract
Atom-047: "Self-attention is O(n²)"
Atom-089: "Sparse attention reduces to O(n log n)"
  ↓ synthesize
Molecule: The Attention-Efficiency Trade-off
  ↓ polish + format
Article: "Attention mechanisms are approaching fundamental limits"
```

### The Auditing Loop

The pyramid supports auditing in both directions:

1. **Forward audit**: Start from sources → every atom is valid → every molecule is sound → the article is trustworthy
2. **Backward audit**: Start from the article → for each claim, find the molecule → for each claim in the molecule, find the atom → for each atom, verify the source

Either direction should produce a complete, documented chain.
