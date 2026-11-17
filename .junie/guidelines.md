# JetBrains AI / Junie Guidelines

Refer to [AGENTS.md](../AGENTS.md) as the single source of truth for architectural standards, multi-tenancy rules, and documentation conventions.

## Core Directives
- **Architecture**: Single database multi-tenancy with `tenant_id` column discrimination across 416 tables divided into System, Tenant-Scoped, and Shared Reference categories.
- **SQL Compatibility**: Dual-driver compatibility (SQLite and PostgreSQL). No driver-locked SQL features.
- **Verification Commands**:
  - `sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"`
  - `sqlite3 fattura-facile.sqlite "PRAGMA foreign_key_check;"`
