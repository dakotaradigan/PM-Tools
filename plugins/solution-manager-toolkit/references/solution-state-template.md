# Solution State Template

Copy this file to `solution_state.md` in your project root to enable persistent state tracking across commands.

Commands that create artifacts will update `solution_state.md` if it exists.

---

```yaml
project: [Project Name]
status: discovery
last_updated: [today's date]

artifacts:
  research_synthesis:
    status: not started
    path: null
    last_command: null
  canonical_data_model:
    status: not started
    path: null
    last_command: null
  api_contracts:
    status: not started
    path: null
    last_command: null
  event_specs:
    status: not started
    path: null
    last_command: null
  nfrs:
    status: not started
    path: null
    last_command: null
  architecture_decisions:
    status: not started
    path: null
    last_command: null
  pi_plan:
    status: not started
    path: null
    last_command: null

codebase:
  discovered: false
  discovery_path: null
  models: []
  apis: []
  dependencies: []

open_questions: []

decisions:
  # - decision: [What was decided]
  #   date: [When]
  #   rationale: [Why]
  #   alternatives_considered: [What else was considered]

risks:
  # - risk: [Description]
  #   likelihood: [high | medium | low]
  #   impact: [high | medium | low]
  #   mitigation: [Plan]

review_findings:
  completeness: []
  cross_reference: []
```

## Usage

```bash
# Initialize state tracking in your project
cp references/solution-state-template.md solution_state.md
# Edit the project name and date, then run commands as usual
```
