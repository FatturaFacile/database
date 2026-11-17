# Antigravity Rules

Follow all guidelines defined in [AGENTS.md](../AGENTS.md).

- **Multi-Tenancy & Schema**: Strictly adhere to single database multi-tenancy rules (`tenant_id` discrimination) and dual-driver compatibility (SQLite & PostgreSQL).
- **Integrity**: Run SQLite integrity checks (`sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"`) after making database modifications.
- **Verification**: Ensure zero broken links across `docs/` and valid Mermaid diagram syntax in `main.md`.
