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
2. **Ontology** section is required — this is the definition
3. **Axiology** section is required — why it matters
4. **Epistemology** section is required — how we know it
5. **Ethics** section is optional — include when the concept has ethical dimensions
6. **Links** use relative markdown: `[term](./term.md)`
7. **External refs** use HTML anchors with `target="_blank"`
8. **Definitions** from external sources are blockquoted (`>`)
9. **Pattern Expression** grounds the abstract in concrete examples
10. **Scope**: definitions are relative to Existence (broadest scope); narrower applications are noted

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
- The `Pattern Expression` subsection bridges theory to practice

## Ring Metadata

Each node belongs to a **ring** — a concentric layer from universal to domain-specific. Ring assignment is declared in `ring.toml` at the ontology repo root, not in the node file itself.

The `ring.toml` format:

```toml
[rings]
[rings.0]
name = "kernel"
description = "Universal terms, always loaded"
terms = ["existence", "entity", "system", "domain", "scope", "context", "resolution", "focus", "abstraction", "perspective", "consciousness", "evolution", "story", "pattern"]

[rings.1]
name = "software"
description = "Software engineering bridge"
terms = ["project", "model", "component", "interface", "state", "event", "command", "query", "aggregate", "repository", "service", "factory", "value-object", "specification", "policy", "module", "bounded-context"]
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

The `exkernel` CLI resolves domain overlays by reading the project's `CLAUDE.md` and merging overlay terms into the active ontology graph. Overlay terms inherit the Ontology/Axiology/Epistemology structure but are defined inline rather than as separate node files.
