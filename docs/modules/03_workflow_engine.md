# Module Reference: Workflow Engine & Approval Matrix

**Module ID**: `03_workflow_engine`  
**Tables Count**: `21`  
**Description**: Dynamic multi-step approval workflows, state machines, business calendars, and delegation logic.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `approval_decisions` | Tenant-Scoped | `id` | `undefined->workflow_instance_steps, undefined->approval_tokens` | `idx_approval_decisions_step, approval_decisions_user_id_index` |
| `approval_matrix_rules` | Tenant-Scoped | `id` | `undefined->approval_matrixes` | `idx_matrix_rules_parent, approval_matrix_rules_tenant_id_index` |
| `approval_matrix_tiers` | Tenant-Scoped | `id` | `undefined->approval_matrixes` | `idx_matrix_tiers_sort, approval_matrix_tiers_tenant_id_index` |
| `approval_matrixes` | Tenant-Scoped | `id` | None | `idx_approval_matrixes_tenant, approval_matrixes_tenant_id_index` |
| `approval_status_translations` | Shared Lookup | `id` | `undefined->approval_statuses` | `approval_status_translations_tenant_id_index, approval_status_translations_locale_index` |
| `approval_statuses` | Shared Lookup | `id` | None | `approval_statuses_tenant_id_index` |
| `approval_tokens` | Tenant-Scoped | `id` | `undefined->workflow_instance_steps` | `idx_approval_tokens_active, approval_tokens_used_at_index` |
| `workflow_audit_entries` | Tenant-Scoped | `id` | `undefined->workflow_instances, undefined->workflow_instance_steps` | `workflow_audit_entries_tenant_id_index, workflow_audit_entries_event_type_index` |
| `workflow_comments` | Tenant-Scoped | `id` | `undefined->workflow_instances, undefined->workflow_instance_steps` | `workflow_comments_user_id_index, workflow_comments_tenant_id_index` |
| `workflow_definitions` | Tenant-Scoped | `id` | None | `workflow_definitions_tenant_id_index, workflow_definitions_company_id_index` |
| `workflow_delegations` | Tenant-Scoped | `id` | None | `workflow_delegations_tenant_id_index, workflow_delegations_delegator_user_id_index` |
| `workflow_delivery_attempts` | Tenant-Scoped | `id` | `undefined->workflow_webhook_subscriptions, undefined->workflow_outbound_events` | `workflow_delivery_attempts_tenant_id_index, idx_delivery_attempts_retry` |
| `workflow_escalation_rules` | Tenant-Scoped | `id` | None | `workflow_escalation_rules_tenant_id_index` |
| `workflow_instance_steps` | Tenant-Scoped | `id` | `undefined->workflow_instances, undefined->workflow_nodes` | `workflow_instance_steps_tenant_id_index, workflow_instance_steps_assigned_user_id_index` |
| `workflow_instances` | Tenant-Scoped | `id` | `undefined->workflow_definitions` | `workflow_instances_tenant_id_index, workflow_instances_company_id_index` |
| `workflow_nodes` | Tenant-Scoped | `id` | `undefined->workflow_definitions, undefined->business_calendars` | `workflow_nodes_tenant_id_index, idx_workflow_nodes_tenant` |
| `workflow_outbound_events` | Tenant-Scoped | `id` | None | `workflow_outbound_events_tenant_id_index, workflow_outbound_events_event_name_index` |
| `workflow_state_translations` | Shared Lookup | `id` | `undefined->workflow_states` | `workflow_state_translations_tenant_id_index, workflow_state_translations_locale_index` |
| `workflow_states` | Shared Lookup | `id` | None | `workflow_states_tenant_id_index, workflow_states_scope_index` |
| `workflow_transitions` | Tenant-Scoped | `id` | `undefined->workflow_definitions, undefined->workflow_nodes, undefined->workflow_nodes` | `workflow_transitions_tenant_id_index, workflow_transitions_idempotency_key_index` |
| `workflow_webhook_subscriptions` | Tenant-Scoped | `id` | None | `workflow_webhook_subscriptions_tenant_id_index, workflow_webhook_subscriptions_company_id_index` |

---

## Detailed Entity Schema & Data Dictionary

### `approval_decisions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_instance_step_id` -> `workflow_instance_steps(id)`
  - `approval_token_id` -> `approval_tokens(id)`
- **Indexes & Constraints**:
  - `idx_approval_decisions_step` (Unique: No)
  - `approval_decisions_user_id_index` (Unique: No)
  - `approval_decisions_tenant_id_index` (Unique: No)
  - `approval_decisions_idempotency_key_index` (Unique: No)
  - `approval_decisions_effective_user_id_index` (Unique: No)
  - `sqlite_autoindex_approval_decisions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_instance_step_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_instance_step |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `effective_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for effective_user |
| `decision` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `comment` | `TEXT` | Yes | NULL | Operational entity attribute |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `user_agent` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `signature_payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `decided_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `idempotency_key` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approval_token_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for approval_token |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `approval_matrix_rules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `approval_matrix_id` -> `approval_matrixes(id)`
- **Indexes & Constraints**:
  - `idx_matrix_rules_parent` (Unique: No)
  - `approval_matrix_rules_tenant_id_index` (Unique: No)
  - `approval_matrix_rules_cost_center_id_index` (Unique: No)
  - `sqlite_autoindex_approval_matrix_rules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `approval_matrix_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approval_matrix |
| `field_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `operator` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `value_string` | `TEXT` | Yes | NULL | Operational entity attribute |
| `value_numeric` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `value_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `approval_matrix_tiers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `approval_matrix_id` -> `approval_matrixes(id)`
- **Indexes & Constraints**:
  - `idx_matrix_tiers_sort` (Unique: No)
  - `approval_matrix_tiers_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_approval_matrix_tiers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `approval_matrix_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approval_matrix |
| `tier_level` | `INTEGER` | No | `1` | Operational entity attribute |
| `approver_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `approver_value` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `approval_type` | `VARCHAR(255)` | No | `'or_parallel'` | Operational entity attribute |
| `threshold_min` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `threshold_max` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `approval_matrixes`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `idx_approval_matrixes_tenant` (Unique: No)
  - `approval_matrixes_tenant_id_index` (Unique: No)
  - `approval_matrixes_company_id_index` (Unique: No)
  - `sqlite_autoindex_approval_matrixes_2` (Unique: Yes)
  - `sqlite_autoindex_approval_matrixes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `target_entity_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `approval_status_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `approval_status_id` -> `approval_statuses(id)`
- **Indexes & Constraints**:
  - `approval_status_translations_tenant_id_index` (Unique: No)
  - `approval_status_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_approval_status_translations_2` (Unique: Yes)
  - `sqlite_autoindex_approval_status_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `approval_status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approval_status |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `approval_statuses`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `approval_statuses_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_approval_statuses_2` (Unique: Yes)
  - `sqlite_autoindex_approval_statuses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `color_badge` | `VARCHAR(255)` | No | `'#F59E0B'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `approval_tokens`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_instance_step_id` -> `workflow_instance_steps(id)`
- **Indexes & Constraints**:
  - `idx_approval_tokens_active` (Unique: No)
  - `approval_tokens_used_at_index` (Unique: No)
  - `approval_tokens_tenant_id_index` (Unique: No)
  - `approval_tokens_expires_at_index` (Unique: No)
  - `approval_tokens_authorized_user_id_index` (Unique: No)
  - `sqlite_autoindex_approval_tokens_2` (Unique: Yes)
  - `sqlite_autoindex_approval_tokens_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_instance_step_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_instance_step |
| `token_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `action_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `authorized_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for authorized_user |
| `expires_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `used_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_audit_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_instance_id` -> `workflow_instances(id)`
  - `workflow_instance_step_id` -> `workflow_instance_steps(id)`
- **Indexes & Constraints**:
  - `workflow_audit_entries_tenant_id_index` (Unique: No)
  - `workflow_audit_entries_event_type_index` (Unique: No)
  - `workflow_audit_entries_company_id_index` (Unique: No)
  - `workflow_audit_entries_actor_user_id_index` (Unique: No)
  - `idx_wf_audit_tenant_event` (Unique: No)
  - `idx_wf_audit_inst_seq` (Unique: No)
  - `sqlite_autoindex_workflow_audit_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `workflow_instance_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_instance |
| `workflow_instance_step_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance_step |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `event_payload` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `actor_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for actor_user |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `user_agent` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `hmac_signature` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Timestamp of record creation |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_comments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_instance_id` -> `workflow_instances(id)`
  - `workflow_instance_step_id` -> `workflow_instance_steps(id)`
- **Indexes & Constraints**:
  - `workflow_comments_user_id_index` (Unique: No)
  - `workflow_comments_tenant_id_index` (Unique: No)
  - `idx_wf_comments_instance` (Unique: No)
  - `sqlite_autoindex_workflow_comments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_instance_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_instance |
| `workflow_instance_step_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance_step |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `comment` | `TEXT` | No | NULL | Operational entity attribute |
| `is_internal_only` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_definitions`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `workflow_definitions_tenant_id_index` (Unique: No)
  - `workflow_definitions_company_id_index` (Unique: No)
  - `idx_workflow_defs_lookup` (Unique: No)
  - `sqlite_autoindex_workflow_definitions_2` (Unique: Yes)
  - `sqlite_autoindex_workflow_definitions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `target_entity_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `version` | `INTEGER` | No | `1` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `is_active` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `configuration` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `published_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_delegations`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `workflow_delegations_tenant_id_index` (Unique: No)
  - `workflow_delegations_delegator_user_id_index` (Unique: No)
  - `workflow_delegations_delegate_user_id_index` (Unique: No)
  - `workflow_delegations_company_id_index` (Unique: No)
  - `idx_wf_delegations_active` (Unique: No)
  - `sqlite_autoindex_workflow_delegations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `delegator_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for delegator_user |
| `delegate_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for delegate_user |
| `scope` | `VARCHAR(255)` | No | `'all'` | Operational entity attribute |
| `starts_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `ends_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_delivery_attempts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `subscription_id` -> `workflow_webhook_subscriptions(id)`
  - `outbound_event_id` -> `workflow_outbound_events(id)`
- **Indexes & Constraints**:
  - `workflow_delivery_attempts_tenant_id_index` (Unique: No)
  - `idx_delivery_attempts_retry` (Unique: No)
  - `sqlite_autoindex_workflow_delivery_attempts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `outbound_event_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for outbound_event |
| `attempt_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `http_status` | `INTEGER` | Yes | NULL | State machine status indicator |
| `response_body` | `TEXT` | Yes | NULL | Operational entity attribute |
| `latency_ms` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `next_retry_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_escalation_rules`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `workflow_escalation_rules_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_workflow_escalation_rules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `reminder_hours` | `INTEGER` | No | `24` | Operational entity attribute |
| `escalation_hours` | `INTEGER` | No | `48` | Operational entity attribute |
| `escalate_to_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `escalate_to_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for escalate_to |
| `auto_action` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_instance_steps`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_instance_id` -> `workflow_instances(id)`
  - `workflow_node_id` -> `workflow_nodes(id)`
- **Indexes & Constraints**:
  - `workflow_instance_steps_tenant_id_index` (Unique: No)
  - `workflow_instance_steps_assigned_user_id_index` (Unique: No)
  - `idx_instance_steps_pending` (Unique: No)
  - `idx_instance_steps_due` (Unique: No)
  - `sqlite_autoindex_workflow_instance_steps_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_instance_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_instance |
| `workflow_node_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_node |
| `assigned_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_user |
| `assigned_role` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `tier_level` | `INTEGER` | No | `1` | Operational entity attribute |
| `due_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `reminded_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `escalated_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_instances`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_definition_id` -> `workflow_definitions(id)`
- **Indexes & Constraints**:
  - `workflow_instances_tenant_id_index` (Unique: No)
  - `workflow_instances_company_id_index` (Unique: No)
  - `idx_workflow_inst_status` (Unique: No)
  - `idx_workflow_inst_morph` (Unique: No)
  - `sqlite_autoindex_workflow_instances_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `workflow_definition_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_definition |
| `approvable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `approvable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approvable |
| `current_node_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for current_node |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `context_snapshot` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `started_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `workflow_definition_version` | `INTEGER` | No | `1` | Operational entity attribute |
| `workflow_definition_snapshot` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `locked_fiscal_document` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |

---

### `workflow_nodes`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_definition_id` -> `workflow_definitions(id)`
  - `business_calendar_id` -> `business_calendars(id)`
- **Indexes & Constraints**:
  - `workflow_nodes_tenant_id_index` (Unique: No)
  - `idx_workflow_nodes_tenant` (Unique: No)
  - `sqlite_autoindex_workflow_nodes_2` (Unique: Yes)
  - `sqlite_autoindex_workflow_nodes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_definition_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_definition |
| `node_key` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `node_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `approval_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `assignee_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `assignee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assignee |
| `timeout_hours` | `INTEGER` | Yes | `48` | Operational entity attribute |
| `escalation_rule_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for escalation_rule |
| `ui_metadata` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `business_calendar_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for business_calendar |
| `voting_threshold_percentage` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `minimum_votes_required` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `locks_approvable_on_completion` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_outbound_events`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `workflow_outbound_events_tenant_id_index` (Unique: No)
  - `workflow_outbound_events_event_name_index` (Unique: No)
  - `idx_outbound_events_created` (Unique: No)
  - `sqlite_autoindex_workflow_outbound_events_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `event_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `event_payload` | `TEXT` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Timestamp of record creation |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_state_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `workflow_state_id` -> `workflow_states(id)`
- **Indexes & Constraints**:
  - `workflow_state_translations_tenant_id_index` (Unique: No)
  - `workflow_state_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_workflow_state_translations_2` (Unique: Yes)
  - `sqlite_autoindex_workflow_state_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `workflow_state_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_state |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `workflow_states`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `workflow_states_tenant_id_index` (Unique: No)
  - `workflow_states_scope_index` (Unique: No)
  - `sqlite_autoindex_workflow_states_2` (Unique: Yes)
  - `sqlite_autoindex_workflow_states_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `scope` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `is_initial` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_final` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `workflow_transitions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `workflow_definition_id` -> `workflow_definitions(id)`
  - `from_node_id` -> `workflow_nodes(id)`
  - `to_node_id` -> `workflow_nodes(id)`
- **Indexes & Constraints**:
  - `workflow_transitions_tenant_id_index` (Unique: No)
  - `workflow_transitions_idempotency_key_index` (Unique: No)
  - `idx_workflow_trans_nav` (Unique: No)
  - `sqlite_autoindex_workflow_transitions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `workflow_definition_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for workflow_definition |
| `from_node_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for from_node |
| `to_node_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for to_node |
| `action_trigger` | `VARCHAR(255)` | No | `'approve'` | Operational entity attribute |
| `condition_rules` | `TEXT` | No | `'[]'` | Operational entity attribute |
| `priority` | `INTEGER` | No | `1` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `idempotency_key` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `workflow_webhook_subscriptions`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `workflow_webhook_subscriptions_tenant_id_index` (Unique: No)
  - `workflow_webhook_subscriptions_company_id_index` (Unique: No)
  - `idx_wf_webhooks_tenant` (Unique: No)
  - `sqlite_autoindex_workflow_webhook_subscriptions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `target_url` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `secret_key` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `subscribed_events` | `TEXT` | No | `'["workflow.completed", "workflow.rejected"]'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

