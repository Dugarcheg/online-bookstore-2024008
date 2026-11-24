# Online Bookstore Constitution

## Core Principles

### I. Spec-Anchored Development (Source of Truth)
`specs/<feature>/spec.md` is the single approved source of truth for all functional and non-functional requirements. No implementation, database migration, or API route may be written before the corresponding specification is reviewed and explicitly approved. Any discrepancy discovered during implementation or testing must trigger a formal specification update (`CHG-xxx` in `docs/changes.md`) prior to code changes.

### II. Technology Stack & Architecture Constraints
The system is built strictly on the Cloudflare edge stack:
- **Runtime:** Cloudflare Workers (`src/index.ts`) written in strict TypeScript.
- **Database:** Cloudflare D1 (SQLite) managed via versioned SQL migrations in `migrations/` and seed data in `sql/seed.sql`.
- **Testing:** Automated unit and integration tests using Vitest (`npx vitest run`).
- External heavy frameworks or non-Cloudflare runtime dependencies are prohibited unless explicitly approved in a feature specification.

### III. Test-First & Real Evidence Verification
Every feature and bug fix must be backed by automated Vitest tests covering both happy paths and edge/error cases. All database changes must be verified against local D1 (`wrangler d1 execute --local`). Fabricated, mocked-out core database logic, or unverified test outputs are strictly forbidden—completion requires real command execution logs and passing test suites.

### IV. Incremental Small-Batch Delivery
Work progresses one small, self-contained feature slice at a time following the Spec Kit pipeline: `specify` -> `clarify` -> `plan` -> `tasks` -> `implement` -> `converge`. Each stage requires explicit student approval before advancing to the next stage.

### V. Security, Safety & Secret Hygiene
Secrets, API tokens, and local environment files (`.dev.vars`) must never be committed to Git or printed in logs. Destructive operations, remote D1 migrations, and production deployments (`wrangler deploy`) must never be executed automatically without explicit student confirmation.

## Governance
- This constitution supersedes ad-hoc coding conventions across the repository.
- Amendments require updating `.specify/memory/constitution.md`, incrementing the version below, and committing the change with a clear rationale.
- All code reviews and `/speckit-converge` checks must verify compliance with these five principles.

**Version**: 1.0.0 | **Ratified**: 2026-11-24 | **Last Amended**: 2026-11-24
