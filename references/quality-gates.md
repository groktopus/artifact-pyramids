# Quality Gates: Verification at Each Layer

Each layer of the Artifact Pyramid has a quality gate — a set of checks that material must pass before it can flow to the next layer. These gates prevent premature synthesis, unsupported claims, and broken traceability.

## How to Use Quality Gates

Run the appropriate gate checklist when:
- Moving atoms into a molecule draft (use the Layer 1→2 gate)
- Moving a molecule into the publication pipeline (use the Layer 2→3 gate)
- Auditing a completed artifact pyramid (run all three)

Each gate has three categories:
- **Critical** — must pass or the artifact cannot proceed
- **Standard** — should pass; flag exceptions explicitly
- **Advisory** — aspirational; note gaps for future improvement

---

## Gate A: Layer 1 Completeness (Sources → Atoms)

Run this before atoms are used in molecule synthesis.

### Critical

- [ ] **Atomicity**: Every atom contains exactly one claim, fact, quote, or data point. No composite atoms.
- [ ] **Source binding**: Every atom references a specific source file and location (section, page, timestamp).
- [ ] **Context independence**: Every atom makes sense without its source document. No "this finding", "the results show", "as discussed above" — substitute the referent.

### Standard

- [ ] **Deduplication**: Identical claims from multiple sources are merged into one atom with multiple source references.
- [ ] **Contradiction flagging**: Atoms making contradictory claims are cross-referenced with a `contradictions:` field.
- [ ] **Classification**: Each atom has a domain tag and type label (fact, claim, quote, data, observation).
- [ ] **Extraction completeness**: The extraction covers the full source, not just confirmatory passages. Counter-evidence is extracted alongside supporting evidence.

### Advisory

- [ ] **Metadata completeness**: Source metadata includes publication date, author, and access timestamp.
- [ ] **Semantic tagging**: Atoms have descriptive tags that support cross-domain discovery (e.g., `trade-off`, `scaling-law`, `emergent`).

---

## Gate B: Layer 2 Integrity (Atoms → Molecules)

Run this before a molecule enters the publication pipeline or is passed to a downstream agent.

### Critical

- [ ] **Emergent claim**: The molecule makes at least one claim that no constituent atom makes individually. If every claim in the molecule can be found in an atom, this is reformatting, not synthesis.
- [ ] **Full traceability**: Every claim in the molecule body traces to specific atom IDs. No orphan claims.
- [ ] **No unsupported leaps**: All inferential steps are supported by atoms. When extrapolating beyond the evidence, the molecule explicitly flags it (e.g., "The atoms suggest X, but no atom directly confirms it.").

### Standard

- [ ] **Conflict transparency**: If atoms disagree on a point, the molecule surfaces the conflict rather than choosing one side. "Atom-012 says X, but atom-047 says not-X. Both are cited."
- [ ] **Cross-referencing**: The molecule links to related molecules in other domains when thematic overlap exists.
- [ ] **Narrative structure**: The molecule has a clear thesis, evidence section, and analytical synthesis — not just a list of atom summaries.

### Advisory

- [ ] **Quantitative precision**: If atoms contain numbers, the molecule preserves and contextualizes them (not "most models improved" but "7 of 12 models improved by ≥5%").
- [ ] **Source diversity**: The molecule draws from multiple sources within and across domains, not a single paper or viewpoint.

---

## Gate C: Layer 3 Readiness (Molecules → Published Artifacts)

Run this before publishing or delivering the artifact.

### Critical

- [ ] **Audience fit**: The artifact's language, depth, and format match the intended audience. (A blog post for practitioners ≠ a research brief for executives.)
- [ ] **End-to-end traceability**: Every factual claim in the artifact traces through a molecule to a source atom. No claim lacks an evidentiary chain.
- [ ] **Internal consistency**: The artifact does not contradict itself. If it presents conflicting views, it does so deliberately with framing (e.g., "Researchers disagree on this point...").

### Standard

- [ ] **Review completion**: The artifact has been reviewed for factual accuracy, clarity, and completeness.
- [ ] **Version tracking**: The artifact has a version identifier and, if significant, a changelog entry.
- [ ] **Format compliance**: The artifact meets the target platform's formatting standards (metadata, SEO fields, image specs, etc.).

### Advisory

- [ ] **Downstream discoverability**: The artifact links back to its source molecules and atoms, enabling consumers to drill deeper.
- [ ] **Measurable outcome**: For decision-oriented artifacts, the expected outcome or acceptance criteria are stated.

---

## Running Gates with the CLI

The `pyramid-status.sh` script performs a structural coverage audit — it checks how many files exist at each layer and whether cross-references between them resolve:

```bash
# Full structural audit of a research project directory
scripts/pyramid-status.sh ./my-research-project

# Machine-readable output
scripts/pyramid-status.sh --json ./my-research-project
```

The script reports:
- **Counts** by layer (sources, atoms, molecules, artifacts)
- **Quality warnings** for markdown files over 5 lines that lack YAML frontmatter
- **Broken cross-references** (`[[wikilinks]]` or `[atom-NNN]` patterns that don't resolve)

**Important: The script checks structural coverage, not gate-level quality.** A "Complete" verdict means files exist in the right naming pattern — it does NOT mean the content passes Gate A, B, or C criteria. Use the checklists above for gate-level verification. The script is a triage tool: run it first to find structural gaps, then apply the quality gate checklists for substantive review.

---

## Gate Failure Recovery

### Gate A failures (Layer 1)

| Failure | Recovery |
|---|---|
| Composite atom | Split into individual atoms |
| Missing source | Re-extract from source, add reference |
| Context-dependent atom | Rewrite to be self-standing |

### Gate B failures (Layer 2)

| Failure | Recovery |
|---|---|
| No emergent claim | Re-examine atoms for novel connections. If none exists, the material isn't ready for molecule status — keep at atom layer. |
| Orphan claim | Either add the supporting atom (re-extract from source) or remove the claim. |
| Conflict hidden | Surface the conflict with `contradictions:` references |

### Gate C failures (Layer 3)

| Failure | Recovery |
|---|---|
| Broken traceability | Trace the claim backward through the pyramid. If the chain is broken, add the missing molecule or atom. |
| Audience mismatch | Rewrite or re-format for the target audience |
| Internal inconsistency | Reconcile conflicting claims or add framing that explains the tension |
