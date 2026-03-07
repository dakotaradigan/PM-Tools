---
name: canonical-data
description: This skill should be used when defining canonical data models with governance, ownership, validation rules, and cross-system traceability for solution management.
---

# Canonical Data

Domain knowledge for defining governed, traceable canonical data models.

## When to Use

- User asks to define a data model, entity, or schema
- Building a canonical or "golden source" data definition
- Reviewing data models for completeness and governance

## Data Model Components

For each entity: name, description, attributes with types, keys, relationships, ownership, validation rules, enumerated values, versioning strategy, and example values.

## Key Principles

- Every entity needs an owner (data steward) and a source system.
- Cross-reference against `references/domain-knowledge.md` for domain-specific identifiers.
- Validate against the data model checklist in `references/domain-knowledge-base.md`.
- Flag attributes without validation rules — they will accept garbage.
- Enumerated values need governance — who adds new values?
- History/versioning strategy is not optional for regulated domains.
