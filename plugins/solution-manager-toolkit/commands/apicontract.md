---
name: solution-work:apicontract
description: Define contract-first API specifications with schemas, error handling, versioning, and consumer alignment
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Define API Contracts

Create contract-first API specifications aligned with the canonical data model.

## Steps

1. **Load references** — Read `references/domain-knowledge-base.md` for the API contract completeness checklist. Read `references/domain-knowledge.md` for domain-specific requirements.

2. **Check for existing context** — Look for `data-model/canonical-entities.md`, `discovery/api-inventory.md`, and `requirements/user-stories.md`. These inform what APIs are needed.

3. **For each API endpoint, define:**
   - HTTP method and path (RESTful conventions)
   - Request schema: body, query parameters, path parameters, headers
   - Response schema for success (200/201/204)
   - Error response schemas with specific error codes and messages
   - Authentication and authorization requirements
   - Rate limiting and throttling policy
   - Versioning strategy (URL path recommended)
   - Pagination approach (cursor-based recommended for large datasets)
   - Idempotency requirements for POST/PUT/DELETE
   - Content negotiation (Accept/Content-Type headers)
   - Example request/response pairs

4. **Validate against checklist** — Run through every item in the API contract completeness checklist. Flag gaps.

5. **Cross-reference with data model** — Verify that every entity referenced in API schemas exists in the canonical data model. Flag mismatches in naming or structure.

6. **Write outputs** — Write to `api-contracts/`:
   - `api-contracts/endpoints.md` — Full endpoint specifications
   - `api-contracts/error-catalog.md` — All error codes and responses
   - `api-contracts/versioning-policy.md` — API versioning and deprecation rules

7. **Update solution state** — If `solution_state.md` exists, update the `api_contracts` artifact status.

8. **Suggest next steps** — Recommend `eventspec` for async integrations, or `nfr` for quality targets, or `review` if multiple artifacts exist.

## Important

- Contract-first: define specs before writing implementation code.
- Consumers should review contracts before implementation — ask who the consumers are.
- Error responses need as much detail as success responses. Don't hand-wave errors.
- Check domain knowledge for domain-specific headers, auth patterns, or compliance requirements.
- If an existing API inventory was discovered, note deviations from current patterns.
