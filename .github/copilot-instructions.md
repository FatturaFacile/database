# GitHub Copilot Instructions

Refer to [AGENTS.md](../AGENTS.md) for complete architectural standards, schema definitions, and quality gate commands.

## Key Constraints & Standards
- **Schema Alignment**: All schemas, data dictionaries, and ER models must conform strictly to `web-api` migrations. Never invent tables or columns.
- **Multi-Tenancy**: Single-database multi-tenancy enforced with discriminator `tenant_id` (System: no `tenant_id`, Tenant-Scoped: `tenant_id NOT NULL`, Shared Lookup: `tenant_id NULL`).
- **Dual-Driver SQL**: All SQL and queries must be compatible with both SQLite and PostgreSQL. Avoid driver-specific syntax.
- **Verification Commands**:
  - `sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"`
  - `sqlite3 fattura-facile.sqlite "PRAGMA foreign_key_check;"`
