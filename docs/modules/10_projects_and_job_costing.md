# Module Reference: Projects, Job Costing & Timesheets

**Module ID**: `10_projects_and_job_costing`  
**Tables Count**: `42`  
**Description**: Project portfolios, task tracking, billable activities, resource allocations, milestone billing, and construction sites.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `billable_activities` | Shared Lookup | `id` | `undefined->tenants, undefined->legal_cases, undefined->users` | `billable_activities_tenant_id_index, billable_activities_is_billed_index` |
| `construction_sites` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `construction_sites_status_index, construction_sites_code_index` |
| `progress_billings` | Shared Lookup | `id` | `undefined->tenants, undefined->construction_sites` | `progress_billings_tenant_id_index, progress_billings_status_index` |
| `project_audit_entries` | Tenant-Scoped | `id` | `undefined->projects` | `project_audit_entries_tenant_id_index, project_audit_entries_company_id_index` |
| `project_billing_events` | Tenant-Scoped | `id` | `undefined->projects` | `project_billing_events_tenant_id_index, project_billing_events_company_id_index` |
| `project_budget_approvals` | Tenant-Scoped | `id` | `undefined->project_budgets, undefined->project_budget_versions` | `project_budget_approvals_tenant_id_index` |
| `project_budget_lines` | Tenant-Scoped | `id` | `undefined->project_budgets, undefined->project_phases` | `project_budget_lines_tenant_id_index, idx_budget_lines_cat` |
| `project_budget_versions` | Tenant-Scoped | `id` | `undefined->project_budgets` | `project_budget_versions_tenant_id_index` |
| `project_budgets` | Tenant-Scoped | `id` | `undefined->projects` | `project_budgets_tenant_id_index, project_budgets_company_id_index` |
| `project_change_order_lines` | Tenant-Scoped | `id` | `undefined->project_change_orders` | `project_change_order_lines_tenant_id_index` |
| `project_change_orders` | Tenant-Scoped | `id` | `undefined->projects` | `project_change_orders_tenant_id_index, project_change_orders_company_id_index` |
| `project_cost_allocations` | Tenant-Scoped | `id` | `undefined->project_cost_entries, undefined->project_tasks` | `project_cost_allocations_tenant_id_index` |
| `project_cost_entries` | Tenant-Scoped | `id` | `undefined->projects, undefined->project_phases, undefined->project_tasks` | `project_cost_entries_tenant_id_index, project_cost_entries_company_id_index` |
| `project_cost_snapshots` | Tenant-Scoped | `id` | `undefined->projects` | `project_cost_snapshots_tenant_id_index` |
| `project_documents` | Tenant-Scoped | `id` | `undefined->projects, undefined->users` | `project_documents_tenant_id_index, project_documents_company_id_index` |
| `project_financial_summaries` | Tenant-Scoped | `id` | `undefined->projects` | `project_financial_summaries_tenant_id_index, project_financial_summaries_company_id_index` |
| `project_invoice_links` | Tenant-Scoped | `id` | `undefined->projects` | `project_invoice_links_tenant_id_index, idx_proj_inv_link` |
| `project_issues` | Tenant-Scoped | `id` | `undefined->projects, undefined->users` | `project_issues_tenant_id_index, project_issues_company_id_index` |
| `project_milestones` | Tenant-Scoped | `id` | `undefined->projects, undefined->project_phases` | `project_milestones_tenant_id_index, project_milestones_company_id_index` |
| `project_notes` | Tenant-Scoped | `id` | `undefined->projects, undefined->users` | `project_notes_tenant_id_index, project_notes_company_id_index` |
| `project_phases` | Tenant-Scoped | `id` | `undefined->projects` | `project_phases_tenant_id_index, project_phases_company_id_index` |
| `project_portfolios` | Tenant-Scoped | `id` | `undefined->users` | `project_portfolios_tenant_id_index, project_portfolios_company_id_index` |
| `project_profitability_snapshots` | Tenant-Scoped | `id` | `undefined->projects` | `project_profitability_snapshots_tenant_id_index, project_profitability_snapshots_company_id_index` |
| `project_resources` | Tenant-Scoped | `id` | `undefined->users, undefined->contacts` | `project_resources_tenant_id_index, project_resources_company_id_index` |
| `project_revenue_recognition` | Tenant-Scoped | `id` | `undefined->projects` | `project_revenue_recognition_tenant_id_index, project_revenue_recognition_company_id_index` |
| `project_risks` | Tenant-Scoped | `id` | `undefined->projects, undefined->users` | `project_risks_tenant_id_index, project_risks_company_id_index` |
| `project_status_histories` | Tenant-Scoped | `id` | `undefined->projects, undefined->users` | `project_status_histories_tenant_id_index, project_status_histories_company_id_index` |
| `project_status_translations` | Shared Lookup | `id` | `undefined->project_statuses` | `project_status_translations_tenant_id_index, project_status_translations_locale_index` |
| `project_statuses` | Shared Lookup | `id` | None | `project_statuses_tenant_id_index` |
| `project_task_assignments` | Tenant-Scoped | `id` | `undefined->project_tasks, undefined->users` | `project_task_assignments_tenant_id_index, idx_task_assignments` |
| `project_task_dependencies` | Tenant-Scoped | `id` | `undefined->project_tasks, undefined->project_tasks` | `project_task_dependencies_tenant_id_index` |
| `project_tasks` | Tenant-Scoped | `id` | `undefined->project_milestones, undefined->project_phases, undefined->projects...` | `project_tasks_tenant_id_index, project_tasks_company_id_index` |
| `project_templates` | Tenant-Scoped | `id` | None | `project_templates_tenant_id_index, project_templates_company_id_index` |
| `project_timesheets` | Tenant-Scoped | `id` | `undefined->projects, undefined->project_tasks, undefined->users` | `project_timesheets_tenant_id_index, project_timesheets_company_id_index` |
| `project_variation_requests` | Tenant-Scoped | `id` | `undefined->projects` | `project_variation_requests_tenant_id_index` |
| `projects` | Tenant-Scoped | `id` | `undefined->users, undefined->contacts, undefined->project_portfolios...` | `projects_tenant_id_index, projects_cost_center_id_index` |
| `resource_allocations` | Tenant-Scoped | `id` | `undefined->projects, undefined->project_tasks, undefined->project_resources` | `resource_allocations_tenant_id_index, idx_resource_alloc` |
| `resource_calendars` | Tenant-Scoped | `id` | `undefined->project_resources` | `resource_calendars_tenant_id_index` |
| `resource_capacity_profiles` | Tenant-Scoped | `id` | `undefined->project_resources` | `resource_capacity_profiles_tenant_id_index` |
| `task_status_translations` | Shared Lookup | `id` | `undefined->task_statuses` | `task_status_translations_tenant_id_index, task_status_translations_locale_index` |
| `task_statuses` | Shared Lookup | `id` | None | `task_statuses_tenant_id_index` |
| `time_entries` | Shared Lookup | `id` | `undefined->tenants, undefined->users, undefined->users` | `time_entries_tenant_id_user_id_clock_in_index, time_entries_clock_out_index` |

---

## Detailed Entity Schema & Data Dictionary

### `billable_activities`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `legal_case_id` -> `legal_cases(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `billable_activities_tenant_id_index` (Unique: No)
  - `billable_activities_is_billed_index` (Unique: No)
  - `sqlite_autoindex_billable_activities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `legal_case_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for legal_case |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `duration_minutes` | `INTEGER` | No | NULL | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `fee_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_billed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `construction_sites`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `client_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `construction_sites_status_index` (Unique: No)
  - `construction_sites_code_index` (Unique: No)
  - `sqlite_autoindex_construction_sites_2` (Unique: Yes)
  - `sqlite_autoindex_construction_sites_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `address` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `sia_norm_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `npk_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `estimated_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'planning'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `progress_billings`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `construction_site_id` -> `construction_sites(id)`
- **Indexes & Constraints**:
  - `progress_billings_tenant_id_index` (Unique: No)
  - `progress_billings_status_index` (Unique: No)
  - `progress_billings_sal_number_index` (Unique: No)
  - `sqlite_autoindex_progress_billings_2` (Unique: Yes)
  - `sqlite_autoindex_progress_billings_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `construction_site_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for construction_site |
| `sal_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_start` | `DATE` | No | NULL | Operational entity attribute |
| `period_end` | `DATE` | No | NULL | Operational entity attribute |
| `gross_certified_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `retention_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `net_payable_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_audit_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_audit_entries_tenant_id_index` (Unique: No)
  - `project_audit_entries_company_id_index` (Unique: No)
  - `idx_proj_audit_seq` (Unique: No)
  - `sqlite_autoindex_project_audit_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `actor_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for actor_user |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `before_state` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `after_state` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_billing_events`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_billing_events_tenant_id_index` (Unique: No)
  - `project_billing_events_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_billing_events_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `source_reference_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for source_reference |
| `billing_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_budget_approvals`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_budget_id` -> `project_budgets(id)`
  - `budget_version_id` -> `project_budget_versions(id)`
- **Indexes & Constraints**:
  - `project_budget_approvals_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_budget_approvals_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_budget_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_budget |
| `budget_version_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for budget_version |
| `approver_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approver_user |
| `status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `decision_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_budget_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_budget_id` -> `project_budgets(id)`
  - `project_phase_id` -> `project_phases(id)`
- **Indexes & Constraints**:
  - `project_budget_lines_tenant_id_index` (Unique: No)
  - `idx_budget_lines_cat` (Unique: No)
  - `sqlite_autoindex_project_budget_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_budget_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_budget |
| `project_phase_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_phase |
| `cost_category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `planned_quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `planned_unit_cost` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `planned_total_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `planned_revenue_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_budget_versions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_budget_id` -> `project_budgets(id)`
- **Indexes & Constraints**:
  - `project_budget_versions_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_budget_versions_2` (Unique: Yes)
  - `sqlite_autoindex_project_budget_versions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_budget_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_budget |
| `version_number` | `INTEGER` | No | NULL | Unique business identification code or document number |
| `revision_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `snapshot_payload` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `total_revenue_budget` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_cost_budget` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `is_baseline` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_budgets`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_budgets_tenant_id_index` (Unique: No)
  - `project_budgets_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_budgets_2` (Unique: Yes)
  - `sqlite_autoindex_project_budgets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `current_version_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `total_revenue_budget` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_cost_budget` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `labour_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `material_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `supplier_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `fleet_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `expense_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `contingency_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `projected_margin_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `projected_margin_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_change_order_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_change_order_id` -> `project_change_orders(id)`
- **Indexes & Constraints**:
  - `project_change_order_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_change_order_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_change_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_change_order |
| `cost_category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity_delta` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_cost_delta` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `total_cost_delta` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `revenue_delta` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_change_orders`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_change_orders_tenant_id_index` (Unique: No)
  - `project_change_orders_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_change_orders_2` (Unique: Yes)
  - `sqlite_autoindex_project_change_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `scope_description` | `TEXT` | No | NULL | Operational entity attribute |
| `cost_impact_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `revenue_impact_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `schedule_impact_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `approved_by_client_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_cost_allocations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_cost_entry_id` -> `project_cost_entries(id)`
  - `project_task_id` -> `project_tasks(id)`
- **Indexes & Constraints**:
  - `project_cost_allocations_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_cost_allocations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_cost_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_cost_entry |
| `project_task_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_task |
| `allocation_percentage` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `allocated_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_cost_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `project_phase_id` -> `project_phases(id)`
  - `project_task_id` -> `project_tasks(id)`
- **Indexes & Constraints**:
  - `project_cost_entries_tenant_id_index` (Unique: No)
  - `project_cost_entries_company_id_index` (Unique: No)
  - `idx_cost_source` (Unique: No)
  - `idx_cost_entries_rollup` (Unique: No)
  - `sqlite_autoindex_project_cost_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `project_phase_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_phase |
| `project_task_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_task |
| `cost_source_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `cost_source_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for cost_source |
| `cost_category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_invoiced` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `invoice_line_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice_line |
| `incurred_date` | `DATE` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_cost_snapshots`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_cost_snapshots_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_cost_snapshots_2` (Unique: Yes)
  - `sqlite_autoindex_project_cost_snapshots_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `snapshot_date` | `DATE` | No | NULL | Operational entity attribute |
| `total_material_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_labour_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_supplier_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_fleet_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_expense_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `cumulative_total_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_documents`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `uploaded_by` -> `users(id)`
- **Indexes & Constraints**:
  - `project_documents_tenant_id_index` (Unique: No)
  - `project_documents_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_documents_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `document_category` | `VARCHAR(255)` | No | `'general'` | Operational entity attribute |
| `file_path` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `file_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `file_size_bytes` | `INTEGER` | No | `0` | Operational entity attribute |
| `mime_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `version` | `INTEGER` | No | `1` | Operational entity attribute |
| `uploaded_by` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_financial_summaries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_financial_summaries_tenant_id_index` (Unique: No)
  - `project_financial_summaries_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_financial_summaries_2` (Unique: Yes)
  - `sqlite_autoindex_project_financial_summaries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `total_contract_revenue` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_invoiced_revenue` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_recognized_revenue` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `actual_material_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_labour_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_supplier_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_fleet_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_expense_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_actual_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `committed_po_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `gross_profit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `gross_profit_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `planned_value_pv` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `earned_value_ev` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `budget_at_completion_bac` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `cost_performance_index_cpi` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `schedule_performance_index_spi` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `estimate_at_completion_eac` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `estimate_to_complete_etc` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `variance_at_completion_vac` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `last_recalculated_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_invoice_links`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_invoice_links_tenant_id_index` (Unique: No)
  - `idx_proj_inv_link` (Unique: No)
  - `sqlite_autoindex_project_invoice_links_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `allocated_revenue` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_issues`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `assigned_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_issues_tenant_id_index` (Unique: No)
  - `project_issues_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_issues_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `severity` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `resolution` | `TEXT` | Yes | NULL | Operational entity attribute |
| `assigned_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_user |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_milestones`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `project_phase_id` -> `project_phases(id)`
- **Indexes & Constraints**:
  - `project_milestones_tenant_id_index` (Unique: No)
  - `project_milestones_company_id_index` (Unique: No)
  - `idx_milestones_due` (Unique: No)
  - `sqlite_autoindex_project_milestones_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `project_phase_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_phase |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `milestone_date` | `DATE` | No | NULL | Operational entity attribute |
| `billing_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `billing_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_completed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `is_billed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_notes`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `author_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_notes_tenant_id_index` (Unique: No)
  - `project_notes_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_notes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `author_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for author_user |
| `title` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `content` | `TEXT` | No | NULL | Operational entity attribute |
| `is_pinned` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_phases`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_phases_tenant_id_index` (Unique: No)
  - `project_phases_company_id_index` (Unique: No)
  - `idx_project_phases` (Unique: No)
  - `sqlite_autoindex_project_phases_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `sequence_order` | `INTEGER` | No | `1` | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `planned_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `planned_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `actual_start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `actual_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `progress_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_portfolios`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `portfolio_manager_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_portfolios_tenant_id_index` (Unique: No)
  - `project_portfolios_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_portfolios_2` (Unique: Yes)
  - `sqlite_autoindex_project_portfolios_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `portfolio_manager_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for portfolio_manager_user |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_profitability_snapshots`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_profitability_snapshots_tenant_id_index` (Unique: No)
  - `project_profitability_snapshots_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_profitability_snapshots_2` (Unique: Yes)
  - `sqlite_autoindex_project_profitability_snapshots_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `snapshot_date` | `DATE` | No | NULL | Operational entity attribute |
| `contract_revenue` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `invoiced_revenue` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `net_profit_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `profit_margin_pct` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `cpi` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `spi` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `progress_percentage` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_resources`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `user_id` -> `users(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `project_resources_tenant_id_index` (Unique: No)
  - `project_resources_company_id_index` (Unique: No)
  - `idx_proj_resources` (Unique: No)
  - `sqlite_autoindex_project_resources_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `resource_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `internal_hourly_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `billing_hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_revenue_recognition`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_revenue_recognition_tenant_id_index` (Unique: No)
  - `project_revenue_recognition_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_revenue_recognition_2` (Unique: Yes)
  - `sqlite_autoindex_project_revenue_recognition_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `accounting_period_date` | `DATE` | No | NULL | Operational entity attribute |
| `cumulative_actual_cost` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `estimated_total_cost_eac` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `cost_completion_percentage` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `cumulative_recognized_revenue` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `period_revenue_adjustment` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `is_posted_to_gl` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_risks`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `owner_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_risks_tenant_id_index` (Unique: No)
  - `project_risks_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_risks_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `category` | `VARCHAR(255)` | No | `'operational'` | Operational entity attribute |
| `probability` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `impact` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `severity` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `potential_cost_impact` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `mitigation_plan` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'identified'` | State machine status indicator |
| `owner_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for owner_user |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_status_histories`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `changed_by` -> `users(id)`
- **Indexes & Constraints**:
  - `project_status_histories_tenant_id_index` (Unique: No)
  - `project_status_histories_company_id_index` (Unique: No)
  - `idx_proj_status_hist` (Unique: No)
  - `sqlite_autoindex_project_status_histories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `from_status` | `VARCHAR(255)` | No | NULL | State machine status indicator |
| `to_status` | `VARCHAR(255)` | No | NULL | State machine status indicator |
| `change_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `changed_by` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_status_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `project_status_id` -> `project_statuses(id)`
- **Indexes & Constraints**:
  - `project_status_translations_tenant_id_index` (Unique: No)
  - `project_status_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_project_status_translations_2` (Unique: Yes)
  - `sqlite_autoindex_project_status_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `project_status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_status |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `label` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `project_statuses`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `project_statuses_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_statuses_2` (Unique: Yes)
  - `sqlite_autoindex_project_statuses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `color_badge` | `VARCHAR(255)` | No | `'#6366F1'` | Operational entity attribute |
| `sort_order` | `INTEGER` | No | `0` | Operational entity attribute |
| `is_terminal` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `project_task_assignments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_task_id` -> `project_tasks(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_task_assignments_tenant_id_index` (Unique: No)
  - `idx_task_assignments` (Unique: No)
  - `sqlite_autoindex_project_task_assignments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_task_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_task |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `role_description` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `allocated_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_task_dependencies`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `predecessor_task_id` -> `project_tasks(id)`
  - `successor_task_id` -> `project_tasks(id)`
- **Indexes & Constraints**:
  - `project_task_dependencies_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_task_dependencies_2` (Unique: Yes)
  - `sqlite_autoindex_project_task_dependencies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `predecessor_task_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for predecessor_task |
| `successor_task_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for successor_task |
| `dependency_type` | `VARCHAR(255)` | No | `'finish_to_start'` | Operational entity attribute |
| `lag_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_tasks`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_milestone_id` -> `project_milestones(id)`
  - `project_phase_id` -> `project_phases(id)`
  - `project_id` -> `projects(id)`
  - `parent_task_id` -> `project_tasks(id)`
- **Indexes & Constraints**:
  - `project_tasks_tenant_id_index` (Unique: No)
  - `project_tasks_company_id_index` (Unique: No)
  - `idx_project_tasks_nav` (Unique: No)
  - `sqlite_autoindex_project_tasks_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `project_phase_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_phase |
| `project_milestone_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_milestone |
| `parent_task_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_task |
| `task_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'backlog'` | State machine status indicator |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `planned_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `planned_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `actual_start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `actual_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `estimated_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `progress_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_milestone_driver` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_templates`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `project_templates_tenant_id_index` (Unique: No)
  - `project_templates_company_id_index` (Unique: No)
  - `sqlite_autoindex_project_templates_2` (Unique: Yes)
  - `sqlite_autoindex_project_templates_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `default_wbs_structure` | `TEXT` | No | `'[]'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_timesheets`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `project_task_id` -> `project_tasks(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `project_timesheets_tenant_id_index` (Unique: No)
  - `project_timesheets_company_id_index` (Unique: No)
  - `idx_timesheet_search` (Unique: No)
  - `sqlite_autoindex_project_timesheets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `project_task_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_task |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `work_date` | `DATE` | No | NULL | Operational entity attribute |
| `hours_worked` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `overtime_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `cost_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `charge_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_cost` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_charge` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'submitted'` | State machine status indicator |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `work_summary` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `project_variation_requests`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `project_variation_requests_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_project_variation_requests_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `variation_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `requested_by` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `request_details` | `TEXT` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'under_review'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `projects`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_manager_user_id` -> `users(id)`
  - `contact_id` -> `contacts(id)`
  - `portfolio_id` -> `project_portfolios(id)`
  - `parent_project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `projects_tenant_id_index` (Unique: No)
  - `projects_cost_center_id_index` (Unique: No)
  - `projects_company_id_index` (Unique: No)
  - `projects_branch_id_index` (Unique: No)
  - `idx_projects_lookup` (Unique: No)
  - `sqlite_autoindex_projects_2` (Unique: Yes)
  - `sqlite_autoindex_projects_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `branch_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for branch |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `portfolio_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for portfolio |
| `parent_project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_project |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `project_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `project_type` | `VARCHAR(255)` | No | `'fixed_price'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `billing_method` | `VARCHAR(255)` | No | `'percentage_of_completion'` | Operational entity attribute |
| `planned_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `planned_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `actual_start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `actual_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `project_manager_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project_manager_user |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `contract_value` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `progress_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `health_status` | `VARCHAR(255)` | No | `'green'` | State machine status indicator |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `resource_allocations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `project_id` -> `projects(id)`
  - `project_task_id` -> `project_tasks(id)`
  - `resource_id` -> `project_resources(id)`
- **Indexes & Constraints**:
  - `resource_allocations_tenant_id_index` (Unique: No)
  - `idx_resource_alloc` (Unique: No)
  - `sqlite_autoindex_resource_allocations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `project_task_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_task |
| `resource_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for resource |
| `allocated_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `allocated_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `allocated_hours_per_day` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `total_allocated_hours` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `resource_calendars`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `resource_id` -> `project_resources(id)`
- **Indexes & Constraints**:
  - `resource_calendars_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_resource_calendars_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `resource_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for resource |
| `daily_available_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `exception_date` | `DATE` | No | NULL | Operational entity attribute |
| `is_available` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `resource_capacity_profiles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `resource_id` -> `project_resources(id)`
- **Indexes & Constraints**:
  - `resource_capacity_profiles_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_resource_capacity_profiles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `resource_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for resource |
| `weekly_capacity_hours` | `NUMERIC(16, 4)` | No | `40` | Operational entity attribute |
| `maximum_overtime_hours` | `NUMERIC(16, 4)` | No | `10` | Operational entity attribute |
| `efficiency_factor` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `task_status_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `task_status_id` -> `task_statuses(id)`
- **Indexes & Constraints**:
  - `task_status_translations_tenant_id_index` (Unique: No)
  - `task_status_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_task_status_translations_2` (Unique: Yes)
  - `sqlite_autoindex_task_status_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `task_status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for task_status |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `label` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `task_statuses`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `task_statuses_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_task_statuses_2` (Unique: Yes)
  - `sqlite_autoindex_task_statuses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `color_badge` | `VARCHAR(255)` | No | `'#64748B'` | Operational entity attribute |
| `sort_order` | `INTEGER` | No | `0` | Operational entity attribute |
| `is_terminal` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `time_entries`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
  - `approved_by` -> `users(id)`
- **Indexes & Constraints**:
  - `time_entries_tenant_id_user_id_clock_in_index` (Unique: No)
  - `time_entries_clock_out_index` (Unique: No)
  - `time_entries_clock_in_index` (Unique: No)
  - `sqlite_autoindex_time_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `clock_in` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `clock_out` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `clock_in_lat` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `clock_in_lng` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_simplified_record` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `break_minutes` | `INTEGER` | No | `0` | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

