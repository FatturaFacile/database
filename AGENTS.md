# Agent Working Guidelines & Standards

This document serves as the canonical reference for all AI coding agents working on this repository (`FatturaFacile/database`).

---

## 1. Project & Stack Overview

- **Repository Role**: Enterprise Database Schema, Architectural Documentation, Topological ER Models, and Reference SQLite Database for the Fattura Facile ERP suite.
- **Source of Truth**: The live schema is defined by migrations in `web-api` (Laravel). All schemas, dictionaries, diagrams, and queries in this repository must mirror and strictly conform to the `web-api` migrations.
- **Architectural Style**:
  - **Multi-Tenancy**: Single Database Multi-Tenancy with Discriminator Column (`tenant_id`).
    - *System / Global Tables (29 tables)*: No `tenant_id` (infrastructural tables and dependent child items scoped transitively via parent FK).
    - *Tenant-Scoped Tables (274 tables)*: High-volume transactional master and operational entities with `tenant_id VARCHAR(36) NOT NULL` (`FOREIGN KEY (tenant_id) REFERENCES tenants(id) ON DELETE CASCADE`).
    - *Shared Reference Lookup & Config Tables (113 tables)*: Baseline presets with `tenant_id VARCHAR(36) NULL` (system baseline when `NULL`, tenant override when populated).
  - **Primary Keys**: UUIDv7 / standard UUID string format across models (`VARCHAR(36)`).
  - **Audit & Outbox**: Transactional Outbox pattern (`transactional_outbox`, `transactional_inbox`) and immutable event streaming.
- **Repository Structure**:
  - `fattura-facile.sqlite`: Reference SQLite database containing schema and lookup baseline data.
  - `main.md`: Authoritative Mermaid Class Diagram defining all 416 tables and foreign key relationships.
  - `ARCHITECTURE.md`: Multi-tenancy isolation models, UUIDv7 conventions, CQRS read/write splitting, and event streaming.
  - `MIGRATIONS.md`: Up/down workflow, zero-downtime expand/contract patterns, and deployment checklists.
  - `docs/SCHEMA_INDEX.md`: Master directory linking all 416 database tables across 17 modular architectural domains.
  - `docs/modules/`: Field-level data dictionaries, nullability, defaults, and foreign keys per module (`01` to `17`).
  - `.dbeaver/`: DBeaver ER modeling configurations.

---

## 2. Coding & Quality Standards

- **Language & Naming**:
  - All documentation, SQL DDL, comments, commit messages, and identifiers must be in English.
  - Table and column names must strictly follow snake_case conventions.
  - Foreign key naming pattern: `<singular_referenced_table>_id` (e.g. `tenant_id`, `contact_id`, `invoice_id`).
- **Schema Modification Policy**:
  - Migrations are additive: never drop or rename existing columns/tables without backward-compatible expand/contract phases.
  - Never invent non-existent tables or columns. Verify against `web-api` migrations or existing documentation before making changes.
  - Maintain strict alignment across `ARCHITECTURE.md`, `README.md`, `main.md`, `docs/SCHEMA_INDEX.md`, and `docs/modules/*.md`.

---

## 3. Database & Testing Policy

- **Dual-Driver Compatibility (SQLite & PostgreSQL)**:
  - Local inspection, automated verification, and reference queries must run on SQLite (`fattura-facile.sqlite`).
  - PostgreSQL is strictly reserved for CI pipelines and Production.
  - All SQL DDL, migrations, and queries must be 100% compatible with both SQLite and PostgreSQL. Avoid driver-locked SQL (e.g. no PostgreSQL-specific `ILIKE`, `::jsonb`, `DISTINCT ON`, or SQLite-incompatible constraints).
  - Always enforce foreign key integrity (`PRAGMA foreign_keys = ON;` in SQLite).

---

## 4. Verification & Quality Commands

- **Repository Build Step**:
  - No compilation or build toolchain is present (documentation and SQL schema repository).
- **SQLite Database Integrity Verification**:
  ```bash
  # Check integrity of the reference SQLite database
  sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"
  sqlite3 fattura-facile.sqlite "PRAGMA foreign_key_check;"
  ```
- **Markdown & Schema Documentation Verification**:
  - Ensure all markdown links in `README.md`, `main.md`, `docs/SCHEMA_INDEX.md`, and `docs/modules/` resolve to existing files.
  - Ensure Mermaid diagram blocks in `main.md` and module docs maintain valid syntax.
