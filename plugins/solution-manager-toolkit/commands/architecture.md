---
name: solution-work:architecture
description: Facilitate architecture decisions with structured tradeoff matrices and decision records
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Architecture Facilitation

Guide architecture decisions using structured tradeoff analysis and decision records.

## Steps

1. **Load references** — Read `references/domain-knowledge-base.md` for the architecture tradeoff framework. Read `references/domain-knowledge.md` for domain-specific architectural concerns. Read `references/team-context.md` for team-specific systems, vendor constraints, and stakeholder context if available.

2. **Identify the decision** — Ask the user what architecture decision needs to be made. Common types:
   - Build vs buy vs extend
   - Synchronous vs asynchronous communication
   - Monolith vs microservices decomposition
   - Data storage technology selection
   - Caching strategy
   - API gateway pattern
   - Event streaming platform

3. **Define options** — Work with the user to define 2-4 concrete options. Each must be specific enough to evaluate (not "Option A: do it right").

4. **Build tradeoff matrix** — For each option, evaluate against the tradeoff framework dimensions:
   - Pros / Cons
   - Latency impact
   - Complexity (implementation + operational)
   - Operational cost (infra + maintenance)
   - Team familiarity
   - Reversibility (how hard to change later)
   - Risk (what could go wrong)

5. **Rank decision criteria** — Ask the user to rank the dimensions by priority for this specific decision. The ranking determines the recommendation.

6. **Document the decision** — Write an Architecture Decision Record (ADR):
   ```
   # ADR-[number]: [Title]

   ## Status: [proposed | accepted | deprecated | superseded]
   ## Date: [date]
   ## Context: [Why this decision is needed]
   ## Options Considered: [List with tradeoff matrix]
   ## Decision: [What was chosen]
   ## Rationale: [Why, referencing ranked criteria]
   ## Consequences: [What changes as a result]
   ```

7. **Write outputs** — Write to `architecture/`:
   - `architecture/adr-[number]-[slug].md` — The ADR
   - Update `architecture/adr-index.md` — Index of all ADRs (create if first one)

8. **Update solution state** — If `solution_state.md` exists, add the decision to the `decisions` list.

## Important

- Present tradeoffs, don't make the decision. The user/team owns architecture decisions.
- Every option must have cons. If an option has no cons, you haven't analyzed it enough.
- Reversibility is often the most underweighted dimension — highlight it.
- Check domain knowledge for domain-specific architectural constraints (regulatory, vendor, latency).
- Reference existing artifacts — the tradeoff should account for the current data model, API contracts, and NFRs.
