# Ring Structure Specification

Ontology terms are organized into concentric rings, from most universal to most domain-specific.

## Rings

### Ring 0: Kernel
- **Scope:** Existential — universally applicable across all domains
- **Loading:** Always loaded in every context
- **Count:** 14 terms
- **Criteria:** A term belongs in Ring 0 if it describes the fundamental structure of existence itself

### Ring 1: Software
- **Scope:** Software engineering — the DDD bridge
- **Loading:** Loaded for software projects
- **Count:** ~17 terms
- **Criteria:** A term belongs in Ring 1 if it's essential for software domain modeling and derives from Ring 0 concepts

### Ring 2+: Extended
- **Scope:** Full philosophical breadth
- **Loading:** On demand
- **Count:** ~80 terms (from btakita/philosophy) and growing
- **Criteria:** Any concept that can be defined using the SPEC.md template

## Ring Metadata

Rings are declared in `exkernel.toml` at the ontology repo root:

```toml
[meta]
name = "existential-kernel/ontology"
description = "Reference existential ontology — Ring 0 kernel + Ring 1 software terms"

[rings.0]
name = "kernel"
description = "14 universal terms, always loaded. The existential scope."
terms = ["existence", "entity", ...]

[rings.1]
name = "software"
description = "The DDD bridge — immediately useful for software projects."
terms = ["project", "model", ...]
```

## Domain Overlays

Projects extend the base ontology by adding a `## Domain Ontology` section to their `CLAUDE.md`:

```markdown
## Domain Ontology

| Term | Derives From | Description |
|------|-------------|-------------|
| Session | project + story | A bounded interaction with temporal arc |
| Document | entity + context | The unit of conversation |
```

Overlay terms reference upstream kernel terms they derive from. The `exkernel` CLI resolves the full chain: Ring 0 → Ring 1 → Domain Overlay.
