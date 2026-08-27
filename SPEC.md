# Ontology Node Specification

Layout and structure for concept definitions in `src/`.

## Node Template

```markdown
# {Term}

## [Ontology](./ontology.md)

{What the term IS. Core definition. Links to related terms via `[term](./term.md)`.}

## [Axiology](./axiology.md)

{Why it MATTERS. Value, significance, implications for practice.}

## [Ethics](./ethics.md)

{Optional. Ethical considerations when applying this concept.}

## [Epistemology](./epistemology.md)

### [Cultural](./culture.md) Definition

{External references — Wiktionary, Wikipedia, etymonline, academic sources.
Use `<a href="..." target="_blank">` format for links.
Quote definitions using `>` blockquotes.}

### [Pattern](./pattern.md) Expression

{How this concept manifests universally in Existence.
Concrete examples showing the pattern at different scales.}
```

## Rules

1. **Title** = the term name, capitalized
2. **Ontology** section is required — this is the definition. Open it with a single plain-language sentence — the **lay definition** — before any depth: tooling (`search`, `scope`, future glossary exports) surfaces that first line as the term's one-line definition, which is what teammates meet first
3. **Axiology** section is required — why it matters
4. **Epistemology** section is required — how we know it
5. **Ethics** section is optional — include when the concept has ethical dimensions
6. **Links** use relative markdown: `[term](./term.md)`
7. **External refs** use HTML anchors with `target="_blank"`
8. **Definitions** from external sources are blockquoted (`>`)
9. **Pattern Expression** grounds the abstract in concrete examples. Epistemology subsection headings are non-normative — lint binds only the required `##` sections — so a domain ontology may prefer plainer headings. The recognized subsection vocabulary is `Cultural Definition` | `Sources` and `Pattern Expression` | `Examples` (kernel spelling | plain spelling); `existence lint` warns on any other Epistemology subsection heading without failing. The plain names trade some meaning for readability, so keep the intent: Examples should show the pattern at more than one scale or resolution (not a flat list of instances), and Sources should first quote how the term is already used around you (the domain's cultural definition) before listing references
10. **Pattern nodes** hold a word that recurs with a different meaning at each scale as *one* node carrying a pattern — a named, recurring resolution of the same forces (the kernel term Pattern) — not one node per meaning (which fragments the vocabulary) and not one vague definition (which explains nothing). Such a node adds two subsections under `## Ontology`, after the lay definition, and this is the recognized Ontology subsection vocabulary: `### Pattern` — **Context** (where the pattern recurs), **Forces** (the tension every occurrence has to resolve), **Resolution** (the shape this domain uses to resolve it), **Related patterns** (links); this is the invariant, what stays true of the word at every scale — and `### Senses` — a table with one row per meaning, ordered **domain (product) meaning first**: the scale it lives at, what it means there in the domain's own words, and how the implementation spells it (route, schema field, table, enum, or code type). `Examples` under Epistemology then maps each sense to concrete implementation evidence, so a reader can go from the domain meaning to the field that carries it. Nodes without a pattern keep the plain form; `existence lint` warns on any other Ontology subsection heading without failing, the same advisory policy as rule 9. Rule of thumb for a new node versus a new sense: a **new node** when the thing has its own lifecycle and identity; a **new sense** when the same word names the same resolution at another scale
11. **Scope**: definitions are relative to Existence (broadest scope); narrower applications are noted
12. **Typed links** (optional): a link title names the SKOS relation the link asserts — `[information](./information.md "broader")`, `[system](./system.md "narrower")`; an untitled link is `related`. Recognized values: `broader` | `narrower` | `related`. `existence export` emits `skos:broader` / `skos:narrower` / `skos:related` and adds the inverse hierarchy link on the target; `existence lint` warns on any other title and on a target typed both broader and narrower. Type a link only where the hierarchy holds at the term's own scope — a passing mention stays untitled

## Section Purposes

| Section | Question | Maps To |
|---------|----------|---------|
| Ontology | What IS it? | Definition, identity |
| Axiology | Why does it MATTER? | Value, purpose, significance |
| Ethics | What SHOULD we consider? | Moral implications |
| Epistemology | How do we KNOW it? | Evidence, sources, patterns |

## Conventions

- Each file = one concept = one node in the ontology graph
- Nodes link to related nodes — the graph IS the ontology
- Definitions start broad (Existence scope) and can be narrowed by context
- The `Pattern Expression` subsection bridges theory to practice (domain ontologies may title it `Examples`)
- A word with several meanings is one pattern node (`### Pattern` + `### Senses` under Ontology), its senses linked in place rather than split into nodes

## Ring Metadata

Each node belongs to a **ring** — a concentric layer from universal to domain-specific. Ring assignment is declared in `existence.toml` at the ontology repo root, not in the node file itself.

The `existence.toml` format:

```toml
[meta]
name = "existence-lang/ontology"
description = "Reference existential ontology — Ring 0 kernel + Ring 1 software terms"

[rings.0]
name = "kernel"
description = "14 universal terms, always loaded. The existential scope."
terms = [
  "existence", "entity", "abstraction", "scope", "context", "resolution",
  "pattern", "system", "domain", "focus", "perspective", "consciousness",
  "evolution", "story"
]

[rings.1]
name = "software"
description = "The DDD bridge — immediately useful for software projects."
terms = [
  "project", "model", "algorithm", "state", "type", "definition",
  "information", "signal", "language", "tool", "environment", "coherence",
  "communication", "collective", "integrity", "qualitative", "quantitative"
]
```

Ring 0 terms are always loaded. Higher rings are loaded on demand based on project context. See [RINGS.md](./RINGS.md) for the full ring structure specification.

## Domain Overlays

Projects extend the base ontology by adding a `## Domain Ontology` section to their `CLAUDE.md`. This section defines project-specific terms that derive from upstream kernel terms:

```markdown
## Domain Ontology

| Term | Derives From | Description |
|------|-------------|-------------|
| Session | project + story | A bounded interaction with temporal arc |
| Document | entity + context | The unit of conversation |
```

Overlay terms reference the upstream kernel terms they extend. This creates a resolution chain: Ring 0 (kernel) -> Ring 1 (software) -> Domain Overlay (project-specific).

The `existence` CLI resolves domain overlays by reading the project's `CLAUDE.md` and merging overlay terms into the active ontology graph. Overlay terms inherit the Ontology/Axiology/Epistemology structure but are defined inline rather than as separate node files.
