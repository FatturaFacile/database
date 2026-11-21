# Agent Guidelines — FatturaFacile/database

## Stack & Repository
- Role: Enterprise ERP database schema docs, topological ER models, and reference SQLite DB (`fattura-facile.sqlite`, 416 tables / 17 domains).
- Source of truth: live schema lives in `web-api` Laravel migrations; mirror strictly—never invent tables or columns.
- No compile/build toolchain (schema + docs repository).
- Key files: `fattura-facile.sqlite`, [main.md](./main.md) (Mermaid ER, 416 tables / 1,062 FKs), [ARCHITECTURE.md](./ARCHITECTURE.md), [MIGRATIONS.md](./MIGRATIONS.md), [docs/SCHEMA_INDEX.md](./docs/SCHEMA_INDEX.md), `docs/modules/01..17_*.md`, `.dbeaver/`.

## Multi-Tenancy & Data Architecture
- Single-database multi-tenancy via `tenant_id` discriminator across 416 tables:
  - System / Global (29): no `tenant_id` (14 infrastructural + 15 parent-FK child tables scoped transitively).
  - Tenant-Scoped (274): `tenant_id VARCHAR(36) NOT NULL`, `FOREIGN KEY (tenant_id) REFERENCES tenants(id) ON DELETE CASCADE`, fail-closed (`WHERE 1 = 0` without tenant context).
  - Shared Reference Lookup / Config (113): `tenant_id VARCHAR(36) NULL` (`NULL` = system baseline; populated = tenant override).
- Primary keys: UUIDv7 (`VARCHAR(36)`), except `cache`/`cache_locks` (`key VARCHAR(255)`), `password_reset_tokens` (`email VARCHAR(255)`), and `enterprise_audit_ledger` (composite `(id, event_timestamp)`).
- Indexing & uniqueness: always index `tenant_id` (or lead compound indexes with `tenant_id`); scope business-key `UNIQUE` constraints with `tenant_id` (never single-column business-ID `UNIQUE` on tenant tables).
- Audit & events: Transactional Outbox/Inbox (`transactional_outbox`, `transactional_inbox`) and append-only `enterprise_audit_ledger`.

## Coding, Schema & Localization Standards
- Language & naming: English only for docs, SQL DDL, comments, commit messages, and identifiers; `snake_case` tables/columns; FKs `<singular_referenced_table>_id`.
- Additive migrations only: reversible `up()`/`down()`; use zero-downtime expand/contract phases (never drop or rename columns/tables in place; add `NOT NULL` columns as nullable first, backfill, then constrain).
- Localization (4 locales mandatory): preserve and support `it`, `de`, `fr`, `en` across all `*_translations` tables (`UNIQUE(<entity>_id, locale)` / `UNIQUE(tenant_id, lookup_item_id, locale)`) and seeded baseline lookups.
- Cross-doc sync: keep [ARCHITECTURE.md](./ARCHITECTURE.md), [README.md](./README.md), [main.md](./main.md), [docs/SCHEMA_INDEX.md](./docs/SCHEMA_INDEX.md), and `docs/modules/*.md` aligned on any schema change.
- Token efficiency: read targeted files/line ranges only (avoid loading full multi-thousand-line diagrams unless needed); emit concise contextual diffs.

## Dual-Driver SQL Policy (SQLite & PostgreSQL)
- SQLite (`fattura-facile.sqlite`, 3.45+) for local inspection, verification, and reference queries; PostgreSQL 16+ strictly for CI and Production.
- 100% SQLite + PostgreSQL compatible DDL/queries: forbid driver-locked syntax (`ILIKE`, `::jsonb`, `DISTINCT ON`, SQLite-incompatible constraints); guard PostgreSQL `CREATE INDEX CONCURRENTLY` behind a driver check.
- Always enforce `PRAGMA foreign_keys = ON;` in SQLite sessions.

## Quality Gate (Mandatory Before Push)
- Never push to `origin/dev` unless every gate passes with zero warnings/errors:
  - `sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"` (must return `ok`)
  - `sqlite3 fattura-facile.sqlite "PRAGMA foreign_key_check;"` (must return empty)
  - Verify all relative Markdown links in modified docs resolve to existing paths and Mermaid blocks remain valid.

## Strict Git Workflow (`dev` Only, Zero PRs, Zero Leftovers)
- Integrate directly into `dev` via local merge: `git checkout dev && git pull --rebase origin dev && git merge --no-ff <branch>` (or direct commit on `dev` for scoped governance/doc changes).
- **FORBIDDEN**: NEVER commit, merge, or push to `main`. NEVER create Pull Requests (`gh pr create` / `gh pr`).
- Autonomous conflict resolution: resolve merge conflicts autonomously preserving Clean Architecture, strict schema/type integrity, multi-tenancy invariants, and all 4 locales (`it`, `de`, `fr`, `en`).
- Mandatory end-of-task cleanup: after pushing `dev`, delete merged local & remote feature branches (`git branch -D <branch>`, `git push origin --delete <branch>`), remove linked worktrees (`git worktree remove --force <path> && git worktree prune`), and remove any temporary/debug files so `git status` is clean.
