# Solution Manager Toolkit

A Claude Code plugin for AI-assisted solution management — accelerating user research synthesis, requirements generation, and workshop preparation.

## What This Does

This plugin automates the repetitive parts of the solution management workflow while keeping human judgment at the center:

| Command | What It Does |
|---------|-------------|
| `/synthesize-research` | Takes raw interview notes, survey responses, and workshop transcripts → outputs structured problem statements, persona cards, and theme matrices |
| `/generate-requirements` | Takes synthesized problem statements → outputs user stories, acceptance criteria, and NFRs |
| `/workshop-prep` | Takes a workshop goal and participant list → outputs timed agenda, discussion prompts, and pre-read materials |

## Components

- **3 Commands** — User-invocable slash commands for each workflow step
- **3 Skills** — Domain knowledge for research synthesis, requirements, and workshop design
- **2 Agents** — Theme extractor for parallel processing + institutional knowledge reviewer for gap analysis

## Installation

### As a Claude Code Plugin

Copy this directory to your Claude Code plugins path:

```bash
cp -r solution-manager-toolkit ~/.claude/plugins/local/solution-manager-toolkit
```

Or clone from GitHub and symlink:

```bash
git clone https://github.com/dakotaradigan/solution-manager-toolkit.git
ln -s $(pwd)/solution-manager-toolkit ~/.claude/plugins/local/solution-manager-toolkit
```

### As Individual Skills

Copy any skill's `SKILL.md` to `~/.claude/skills/<skill-name>/SKILL.md`.

## Usage

### Synthesize Research

Place your research files (markdown) in a directory, then:

```
/synthesize-research
```

The command will find your files, extract themes in parallel, and generate:
- `synthesis/research-summary.md`
- `synthesis/personas.md`
- `synthesis/problem-statements.md`
- `synthesis/theme-matrix.md`

### Generate Requirements

After synthesis, run:

```
/generate-requirements
```

Generates:
- `requirements/user-stories.md`
- `requirements/acceptance-criteria.md`
- `requirements/nfrs.md`

### Workshop Prep

```
/workshop-prep
```

Generates:
- `workshop/agenda.md`
- `workshop/discussion-prompts.md`
- `workshop/pre-read.md`

## MCP Server Integrations (Optional)

This plugin works standalone with local files. For pushing artifacts to external tools, configure these MCP servers:

| Tool | MCP Server | What It Enables |
|------|-----------|----------------|
| Miro | [miroapp/miro-ai](https://github.com/miroapp/miro-ai) | Push workshop structures, persona boards, theme clusters to Miro |
| Confluence | [atlassian/atlassian-mcp-server](https://github.com/atlassian/atlassian-mcp-server) | Publish requirements docs, research summaries to Confluence |
| Jira | [atlassian/atlassian-mcp-server](https://github.com/atlassian/atlassian-mcp-server) | Create epics and stories from generated requirements |

## Sample Data

See `sample-data/` for synthetic market data platform research that demonstrates the full workflow.

## License

MIT
