---
name: solution-work:status
description: Generate a status report summarizing solution progress, artifact completeness, open questions, and next steps
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Status Report

Generate a comprehensive status report from solution state and existing artifacts.

## Steps

1. **Check for solution state** — Read `solution_state.md` if it exists. If not, scan for artifacts manually.

2. **Inventory artifacts** — Glob for all artifacts across known directories: `synthesis/`, `data-model/`, `api-contracts/`, `event-specs/`, `requirements/`, `pi-planning/`, `discovery/`, `architecture/`, `review/`. Note which exist and their last modified dates.

3. **Assess progress** — For each artifact category, determine status:
   - **Complete** — Artifact exists and has been reviewed
   - **In progress** — Artifact exists but hasn't been reviewed
   - **Not started** — No artifact exists

4. **Summarize open items** — Pull from `solution_state.md` if available:
   - Open questions
   - Unresolved risks
   - Review findings not yet addressed
   - Missing NFRs or data model gaps

5. **Generate status report:**
   ```markdown
   # Solution Status Report
   ## Date: [today]
   ## Project: [from solution_state or directory name]

   ## Progress Summary
   | Artifact | Status | Last Updated | Notes |
   |----------|--------|-------------|-------|

   ## Key Decisions Made
   - [from architecture ADRs and solution_state]

   ## Open Questions
   - [from solution_state]

   ## Risks
   - [from solution_state and review findings]

   ## Recommended Next Steps
   1. [Most impactful next command to run]
   2. [Second priority]
   3. [Third priority]
   ```

6. **Write output** — Write to `status-report.md` in the project root.

7. **Present summary** — Show the user the key metrics: X of Y artifact categories complete, Z open questions, top 3 next steps.

## Important

- Status is descriptive, not prescriptive. Report the state, recommend next steps, but don't make decisions.
- Always recommend the next command to run based on what's missing.
- If no `solution_state.md` exists, suggest creating one from the template.
- Flag stale artifacts (not updated in > 2 weeks) as needing refresh.
