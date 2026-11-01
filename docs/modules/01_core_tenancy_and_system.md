# Module Reference: Core Tenancy, Authentication & System Infrastructure

**Module ID**: `01_core_tenancy_and_system`  
**Tables Count**: `15`  
**Description**: Foundation services managing multi-tenant isolation, user identity, access control, worker queues, caching, and backups.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `cache` | System / Global | `key` | None | `cache_expiration_index` |
| `cache_locks` | System / Global | `key` | None | `cache_locks_expiration_index` |
| `dashboard_layouts` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `PRIMARY` |
| `enterprise_feature_flags` | Shared Lookup | `id` | None | `idx_feature_user, idx_feature_tenant` |
| `failed_jobs` | System / Global | `id` | None | `failed_jobs_connection_queue_failed_at_index` |
| `job_batches` | System / Global | `id` | None | `PRIMARY` |
| `jobs` | System / Global | `id` | None | `jobs_queue_index` |
| `password_reset_tokens` | System / Global | `email` | None | `PRIMARY` |
| `personal_access_tokens` | System / Global | `id` | None | `personal_access_tokens_tokenable_type_tokenable_id_index, personal_access_tokens_expires_at_index` |
| `sessions` | System / Global | `id` | None | `sessions_user_id_index, sessions_last_activity_index` |
| `tenant_backups` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `tenant_backups_tenant_id_status_completed_at_index, tenant_backups_status_index` |
| `tenant_user` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `PRIMARY` |
| `tenants` | System / Global | `id` | None | `tenants_vat_number_index, tenants_uid_number_index` |
| `translations` | Shared Lookup | `id` | `undefined->tenants` | `PRIMARY` |
| `users` | System / Global | `id` | None | `PRIMARY` |

---

## Detailed Entity Schema & Data Dictionary

### `cache`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `cache_expiration_index` (Unique: No)
  - `sqlite_autoindex_cache_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `key` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `value` | `TEXT` | No | NULL | Operational entity attribute |
| `expiration` | `INTEGER` | No | NULL | Operational entity attribute |

---

### `cache_locks`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `cache_locks_expiration_index` (Unique: No)
  - `sqlite_autoindex_cache_locks_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `key` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `owner` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `expiration` | `INTEGER` | No | NULL | Operational entity attribute |

---

### `dashboard_layouts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_dashboard_layouts_2` (Unique: Yes)
  - `sqlite_autoindex_dashboard_layouts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `name` | `VARCHAR(255)` | No | `'Default Dashboard'` | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `widgets_layout` | `TEXT` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `enterprise_feature_flags`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `idx_feature_user` (Unique: No)
  - `idx_feature_tenant` (Unique: No)
  - `enterprise_feature_flags_user_id_index` (Unique: No)
  - `enterprise_feature_flags_tenant_id_index` (Unique: No)
  - `enterprise_feature_flags_feature_key_index` (Unique: No)
  - `sqlite_autoindex_enterprise_feature_flags_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `feature_key` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `is_enabled` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `payload_config` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `failed_jobs`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `failed_jobs_connection_queue_failed_at_index` (Unique: No)
  - `sqlite_autoindex_failed_jobs_2` (Unique: Yes)
  - `sqlite_autoindex_failed_jobs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `uuid` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `connection` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `queue` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `payload` | `TEXT` | No | NULL | Operational entity attribute |
| `exception` | `TEXT` | No | NULL | Operational entity attribute |
| `failed_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |

---

### `job_batches`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `sqlite_autoindex_job_batches_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `total_jobs` | `INTEGER` | No | NULL | Monetary or financial decimal quantity |
| `pending_jobs` | `INTEGER` | No | NULL | Operational entity attribute |
| `failed_jobs` | `INTEGER` | No | NULL | Operational entity attribute |
| `failed_job_ids` | `TEXT` | No | NULL | Operational entity attribute |
| `options` | `TEXT` | Yes | NULL | Operational entity attribute |
| `cancelled_at` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `created_at` | `INTEGER` | No | NULL | Timestamp of record creation |
| `finished_at` | `INTEGER` | Yes | NULL | Operational entity attribute |

---

### `jobs`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `jobs_queue_index` (Unique: No)
  - `sqlite_autoindex_jobs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `queue` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `payload` | `TEXT` | No | NULL | Operational entity attribute |
| `attempts` | `INTEGER` | No | NULL | Operational entity attribute |
| `reserved_at` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `available_at` | `INTEGER` | No | NULL | Operational entity attribute |
| `created_at` | `INTEGER` | No | NULL | Timestamp of record creation |

---

### `password_reset_tokens`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `sqlite_autoindex_password_reset_tokens_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `token` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |

---

### `personal_access_tokens`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `personal_access_tokens_tokenable_type_tokenable_id_index` (Unique: No)
  - `personal_access_tokens_expires_at_index` (Unique: No)
  - `sqlite_autoindex_personal_access_tokens_2` (Unique: Yes)
  - `sqlite_autoindex_personal_access_tokens_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tokenable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `tokenable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for tokenable |
| `name` | `TEXT` | No | NULL | Operational entity attribute |
| `token` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `abilities` | `TEXT` | Yes | NULL | Operational entity attribute |
| `last_used_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `expires_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sessions`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `sessions_user_id_index` (Unique: No)
  - `sessions_last_activity_index` (Unique: No)
  - `sqlite_autoindex_sessions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `user_agent` | `TEXT` | Yes | NULL | Operational entity attribute |
| `payload` | `TEXT` | No | NULL | Operational entity attribute |
| `last_activity` | `INTEGER` | No | NULL | Operational entity attribute |

---

### `tenant_backups`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `tenant_backups_tenant_id_status_completed_at_index` (Unique: No)
  - `tenant_backups_status_index` (Unique: No)
  - `sqlite_autoindex_tenant_backups_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `filename` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `disk` | `VARCHAR(255)` | No | `'private'` | Operational entity attribute |
| `file_size_bytes` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `error_message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `tenant_user`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_tenant_user_2` (Unique: Yes)
  - `sqlite_autoindex_tenant_user_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `role` | `VARCHAR(255)` | No | `'member'` | Operational entity attribute |
| `permissions` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `tenants`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `tenants_vat_number_index` (Unique: No)
  - `tenants_uid_number_index` (Unique: No)
  - `tenants_fiscal_code_index` (Unique: No)
  - `tenants_country_index` (Unique: No)
  - `sqlite_autoindex_tenants_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `legal_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `fiscal_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `vat_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `uid_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `default_currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `qr_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `sdi_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `pec_email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `settings` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `is_maintenance` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |

---

### `translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_translations_2` (Unique: Yes)
  - `sqlite_autoindex_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `group` | `VARCHAR(255)` | No | `'messages'` | Operational entity attribute |
| `key` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `value` | `TEXT` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `users`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `sqlite_autoindex_users_2` (Unique: Yes)
  - `sqlite_autoindex_users_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `password` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `locale` | `VARCHAR(255)` | No | `'it'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `email_verified_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `remember_token` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

