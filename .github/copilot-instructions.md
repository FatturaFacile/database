# Copilot instructions

Project: Schema documentation, SQL DDL and a SQLite sample (the live schema is defined by the web-api migrations).

## Essentials

- Write all code, comments, commit messages and documentation in English.
- Fix every error you meet, also outside the request.
- Never add dependencies or secrets; follow the sibling files of the area you change.
- The web-api migrations are the source of truth: never invent tables or columns that do not exist there.
- Migrations are additive (no drop or rename of existing columns or tables); document expand/contract steps in `MIGRATIONS.md`.
- Keep `ARCHITECTURE.md`, `README.md` and `docs/` consistent with each other.

## Commands

- No build step: documents and SQL files are reviewed by hand.
