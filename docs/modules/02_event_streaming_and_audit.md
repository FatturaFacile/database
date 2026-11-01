# Module Reference: Audit Logging & Event Streaming (Outbox/Inbox)

**Module ID**: `02_event_streaming_and_audit`  
**Tables Count**: `5`  
**Description**: Enterprise event distribution, transactional outbox/inbox guarantees, and immutable Merkle audit trails.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `audit_logs` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `audit_logs_tenant_id_created_at_index, audit_logs_event_index` |
| `enterprise_audit_ledger` | Tenant-Scoped | `id, event_timestamp` | None | `idx_audit_resource` |
| `transactional_inbox` | Tenant-Scoped | `id` | None | `transactional_inbox_tenant_id_index, idx_inbox_pending` |
| `transactional_outbox` | Tenant-Scoped | `id` | None | `transactional_outbox_tenant_id_index, transactional_outbox_retry_after_index` |
| `transactional_outbox_archive` | Tenant-Scoped | `id` | None | `transactional_outbox_archive_tenant_id_index, transactional_outbox_archive_company_id_index` |

---

## Detailed Entity Schema & Data Dictionary

### `audit_logs`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `audit_logs_tenant_id_created_at_index` (Unique: No)
  - `audit_logs_event_index` (Unique: No)
  - `audit_logs_auditable_type_index` (Unique: No)
  - `audit_logs_auditable_id_index` (Unique: No)
  - `sqlite_autoindex_audit_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `event` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `auditable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `auditable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for auditable |
| `old_values` | `TEXT` | Yes | NULL | Operational entity attribute |
| `new_values` | `TEXT` | Yes | NULL | Operational entity attribute |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `user_agent` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `enterprise_audit_ledger`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `idx_audit_resource` (Unique: No)
  - `sqlite_autoindex_enterprise_audit_ledger_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `event_timestamp` | `TIMESTAMP` | Yes | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `module_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `action` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `resource_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `resource_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for resource |
| `actor_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for actor_user |
| `actor_type` | `VARCHAR(255)` | No | `'user'` | Operational entity attribute |
| `payload_before` | `TEXT` | Yes | NULL | Operational entity attribute |
| `payload_after` | `TEXT` | Yes | NULL | Operational entity attribute |
| `diff_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `user_agent` | `TEXT` | Yes | NULL | Operational entity attribute |
| `record_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `previous_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |

---

### `transactional_inbox`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `transactional_inbox_tenant_id_index` (Unique: No)
  - `idx_inbox_pending` (Unique: No)
  - `sqlite_autoindex_transactional_inbox_2` (Unique: Yes)
  - `sqlite_autoindex_transactional_inbox_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `message_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for message |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `payload_json` | `TEXT` | No | NULL | Operational entity attribute |
| `received_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `processed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |

---

### `transactional_outbox`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `transactional_outbox_tenant_id_index` (Unique: No)
  - `transactional_outbox_retry_after_index` (Unique: No)
  - `transactional_outbox_company_id_index` (Unique: No)
  - `idx_outbox_pending` (Unique: No)
  - `sqlite_autoindex_transactional_outbox_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `aggregate_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `aggregate_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for aggregate |
| `payload_json` | `TEXT` | No | NULL | Operational entity attribute |
| `occurred_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `processed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `retry_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `error_message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `retry_after` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |

---

### `transactional_outbox_archive`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `transactional_outbox_archive_tenant_id_index` (Unique: No)
  - `transactional_outbox_archive_company_id_index` (Unique: No)
  - `idx_outbox_archive_date` (Unique: No)
  - `sqlite_autoindex_transactional_outbox_archive_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `aggregate_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `aggregate_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for aggregate |
| `payload_json` | `TEXT` | No | NULL | Operational entity attribute |
| `occurred_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `processed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `retry_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'processed'` | State machine status indicator |
| `error_message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `retry_after` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `archived_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |

---

