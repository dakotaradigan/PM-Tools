---
name: solution-work:datamodel
description: Define canonical data models with governance, ownership, validation rules, and domain-specific identifiers
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Define Canonical Data Model

Create governed, traceable canonical data definitions.

## Steps

1. **Load references** — Read `references/domain-knowledge-base.md` for the data model completeness checklist. Read `references/domain-knowledge.md` for domain-specific identifiers and validation flags.

2. **Check for existing context** — Look for `discovery/entity-map.md` (from the `discover` command) and `synthesis/problem-statements.md` (from `synthesize-research`). These provide starting context. If neither exists, ask the user to describe the data entities.

3. **For each entity, define:**
   - Entity name and description
   - All attributes with data types, required/optional, defaults
   - Primary key and unique identifiers (cross-reference domain-specific identifiers from domain knowledge)
   - Relationships to other entities (type, cardinality, FK)
   - Enumerated value sets with governance (who can add values?)
   - Validation rules and constraints
   - Versioning / history tracking strategy
   - Data ownership: steward, source system, update frequency
   - Example values

4. **Validate against checklist** — Run through every item in the data model completeness checklist from `references/domain-knowledge-base.md`. Flag any gaps.

5. **Apply domain flags** — Check domain-specific validation flags from `references/domain-knowledge.md` (e.g., multi-asset coverage, identifier cross-referencing, corporate actions handling).

6. **Write outputs** — Write to `data-model/`:
   - `data-model/canonical-entities.md` — Full entity definitions
   - `data-model/relationships.md` — Entity relationship documentation
   - `data-model/governance.md` — Ownership, stewardship, change process

7. **Update solution state** — If `solution_state.md` exists, update the `canonical_data_model` artifact status.

8. **Suggest next steps** — Recommend `apicontract` to define APIs that expose these entities, or `nfr` to define quality attributes.

## Important

- Every entity needs an owner. "TBD" is acceptable temporarily but must be flagged.
- Cross-reference identifiers against domain knowledge. Flag entities with only local IDs.
- Validate against the checklist — don't skip items because they seem obvious.
- Enumerated values need governance — an ungoverned enum will grow uncontrollably.
- History/versioning is not optional in regulated domains.
