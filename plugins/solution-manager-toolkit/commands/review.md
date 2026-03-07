---
name: solution-work:review
description: Run completeness and cross-reference checks across all solution artifacts using parallel review agents
allowed-tools: Read, Glob, Grep, Write, Agent, Bash
user-invocable: true
---

# Review Solution Artifacts

Orchestrate a comprehensive review of all solution artifacts using the completeness-checker and cross-reference-checker agents.

## Steps

1. **Inventory artifacts** — Use Glob to find all solution artifacts across known directories: `synthesis/`, `data-model/`, `api-contracts/`, `event-specs/`, `requirements/`, `pi-planning/`, `discovery/`. Present the list to the user and confirm which artifacts to review.

2. **Launch completeness checks in parallel** — For each artifact found, launch a `completeness-checker` agent using the Agent tool. Each agent reviews one artifact against the structural checklist from `references/domain-knowledge-base.md` and domain flags from `references/domain-knowledge.md`. Run all agents in parallel.

3. **Launch cross-reference check** — Launch a `cross-reference-checker` agent to check consistency across all artifacts simultaneously. This agent looks for naming mismatches, orphan references, CRUD gaps, NFR gaps, and contradictions.

4. **Collect results** — Wait for all agents to complete. Merge the findings into a single review report.

5. **Write review report** — Write to `review/`:
   - `review/completeness-report.md` — Per-artifact completeness scores and gaps
   - `review/cross-reference-report.md` — Cross-artifact consistency findings
   - `review/action-items.md` — Prioritized list of gaps to address, sorted by severity

6. **Update solution state** — If `solution_state.md` exists, update the `review_findings` section.

7. **Present summary** — Show the user: overall completeness scores, critical cross-reference issues, and top 5 action items.

## Important

- Review is non-destructive — it reports findings but does not modify artifacts.
- Run completeness and cross-reference checks in parallel for speed.
- Contradictions (from cross-reference) are higher severity than gaps (from completeness).
- The review should make the author say "good catch" — flag non-obvious issues.
- Suggest specific commands to address gaps (e.g., "run `/solution-work:nfr` to add missing NFRs").
