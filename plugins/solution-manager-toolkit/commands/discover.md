---
name: solution-work:discover
description: Analyze an existing codebase to extract data models, API endpoints, dependencies, and architectural patterns
allowed-tools: Read, Glob, Grep, Write, Bash, Agent
user-invocable: true
---

# Discover Codebase

Comprehend an existing codebase and produce a structured discovery report for solution management context.

## Steps

1. **Load team context** — Read `references/team-context.md` for team-specific systems, codebase conventions, and vendor integrations if available. Use this to guide where to look and what patterns to expect.

2. **Identify project type** — Use Glob and Read to determine the tech stack: language, framework, build tools, package manager. Check for files like `package.json`, `Gemfile`, `pom.xml`, `go.mod`, `requirements.txt`, `Cargo.toml`, etc.

3. **Extract data models** — Search for ORM definitions, database schemas, migration files, entity classes, or type definitions. For each entity found, capture: name, attributes, relationships, and source file.

4. **Map API endpoints** — Search for route definitions, controller files, OpenAPI specs, or GraphQL schemas. For each endpoint: method, path, request/response shape, and authentication requirements.

5. **Catalog dependencies** — Read dependency files and identify external services, vendor integrations, shared libraries, and internal service calls. Flag any undocumented service-to-service communication.

6. **Detect event patterns** — Search for message queue producers/consumers, pub/sub patterns, webhook handlers, or event bus usage. Capture event names, payloads, and flow direction.

7. **Identify configuration** — Scan for environment variables, feature flags, config files, and deployment manifests. Categorize as: secrets, environment-specific, or static config.

8. **Write discovery report** — Write the following to `discovery/`:
   - `discovery/codebase-report.md` — Full discovery findings organized by category
   - `discovery/entity-map.md` — All data entities with attributes and relationships
   - `discovery/api-inventory.md` — All API endpoints with methods and schemas
   - `discovery/dependency-graph.md` — External and internal dependencies

9. **Update solution state** — If `solution_state.md` exists, update the `codebase` section with discovery findings.

10. **Suggest next steps** — Recommend the logical next command based on findings (typically `datamodel` or `apicontract`).

## Important

- Discovery is observation, not inference. Report what the code says, not what you think it should say.
- Flag undocumented dependencies as high-risk items.
- If the codebase is very large, ask the user to scope discovery to specific directories or modules.
- Reference the codebase-discovery skill for domain knowledge.
- Check `references/domain-knowledge.md` for domain-specific patterns to look for.
