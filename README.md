# Existence Lang — Specification

Formal specification for ontology nodes in the [Existence Lang](https://github.com/existence-lang) framework.

## Overview

Each concept in the ontology is a **node** — a markdown file following a structured template. Nodes answer three questions:

1. **Ontology** — What IS it? (definition, identity)
2. **Axiology** — Why does it MATTER? (value, purpose)
3. **Epistemology** — How do we KNOW it? (evidence, patterns)

## Documents

- [SPEC.md](./SPEC.md) — Node format specification and template
- [RINGS.md](./RINGS.md) — Ring structure specification

## Usage

Ontology repos (like [existence-lang/ontology](https://github.com/existence-lang/ontology)) follow this spec. The `existence` CLI validates nodes against it.

## License

Apache-2.0
