---
name: solution-work:nfr
description: Define non-functional requirements with measurable targets using domain-specific templates and defaults
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Define Non-Functional Requirements

Guided NFR definition with domain-specific defaults.

## Steps

1. **Load domain defaults** — Read `references/domain-knowledge.md` for domain-specific NFR starting points. Read `references/domain-knowledge-base.md` for the NFR format template.

2. **Identify capabilities** — Check for existing artifacts: `discovery/api-inventory.md`, `requirements/user-stories.md`, or any API contracts. List the capabilities that need NFRs. If no artifacts exist, ask the user to describe the capabilities.

3. **For each capability, prompt for NFRs** — Present the domain defaults as starting points and ask the user to confirm or adjust:
   - **Latency** — p50, p99, under what conditions
   - **Availability** — uptime target, during what hours
   - **Throughput** — requests/sec or events/sec at peak
   - **Data quality** — accuracy, freshness, completeness targets
   - **Security** — authentication, authorization, encryption requirements
   - **Compliance** — regulatory requirements that apply (flag from domain knowledge)
   - **Scalability** — growth expectations over 1-3 years

4. **Format each NFR** using the template from domain-knowledge-base.md:
   ```
   Quality: [attribute]
   Target: [measurable value]
   Conditions: [when this applies]
   Measurement: [how to verify]
   Priority: [MoSCoW]
   Source: [origin]
   ```

5. **Write outputs** — Write to `requirements/nfrs.md` (or update if it exists). Group NFRs by capability.

6. **Cross-reference** — Flag any capabilities from existing artifacts that have no NFRs. Flag any NFRs without a clear measurement method.

7. **Update solution state** — If `solution_state.md` exists, update the `nfrs` artifact status.

## Important

- NFRs without measurable targets are opinions, not requirements. Push for specificity.
- Domain defaults are starting points, not mandates. The user owns the final values.
- Every capability needs at least latency, availability, and data quality NFRs.
- Check `references/domain-knowledge.md` for regulatory requirements that may mandate specific NFRs.
- Suggest `/solution-work:review` after NFR definition to check completeness.
