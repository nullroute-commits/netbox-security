# NetBox Security Agent Source of Truth

This repository adopts the upstream `agency-agents` approach as a project-level AI operating model.

- Upstream reference: https://github.com/nullroute-commits/agency-agents
- Local skill: `/agent.md`
- Copilot workspace entrypoint: `/.github/copilot-instructions.md`

If AI guidance files disagree, use this precedence order:

1. `AGENTS.md`
2. `.github/copilot-instructions.md`
3. `agent.md`
4. `CONTRIBUTING.md`
5. `README.md`

## Project overview

`netbox-security` is a NetBox plugin for tracking security and NAT-related objects.

Core plugin areas:

- Django/NetBox models in `/netbox_security/models`
- REST API serializers and viewsets in `/netbox_security/api`
- GraphQL types in `/netbox_security/graphql`
- Forms, filtersets, tables, and views in their matching package directories
- Tests in `/netbox_security/tests`

## Repository conventions

- Target Python is 3.12+.
- Format Python code with Black.
- Keep changes NetBox-plugin-native; avoid generic Django patterns when a NetBox pattern already exists.
- Preserve plugin UI namespace `plugins:netbox_security`.
- Preserve plugin API namespace `plugins-api:netbox_security`.
- Add or update tests for behavior changes whenever practical.

## Operational guidance

- Prefer small, reviewable changes.
- Treat model choices, serializer fields, GraphQL types, and filtersets as coupled surfaces.
- When changing persisted choice values, plan a data migration.
- When changing model validation, account for API, forms, GraphQL, and direct ORM usage.
- Do not mutate related objects from validation methods.

## Validation guidance

Primary checks used by this repository:

- Black formatting
- NetBox plugin test suite via `python netbox/manage.py test netbox_security.tests --parallel -v2`

The CI workflow currently provisions PostgreSQL, Redis, and a NetBox checkout before running tests.

## Delivery expectations

When working in this repository, AI agents should:

- summarize concrete findings with file citations
- call out data-migration risk explicitly
- separate verified bugs from suspected gaps
- produce NetBox-aware implementation plans
