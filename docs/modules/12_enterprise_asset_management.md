# Module Reference: Enterprise Asset Management (EAM)

**Module ID**: `12_enterprise_asset_management`  
**Tables Count**: `18`  
**Description**: Fixed asset registers, depreciation schedules, preventive maintenance plans, inspections, and asset lifecycle tracking.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `eam_asset_assignments` | Tenant-Scoped | `id` | `undefined->eam_fixed_assets` | `eam_asset_assignments_tenant_id_index, eam_asset_assignments_status_index` |
| `eam_asset_categories` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_asset_categories` | `eam_asset_categories_parent_id_index, eam_asset_categories_company_id_index` |
| `eam_asset_classes` | Tenant-Scoped | `id` | `undefined->tenants` | `eam_asset_classes_code_index` |
| `eam_asset_components` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_fixed_assets` | `PRIMARY` |
| `eam_asset_custodians` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->users...` | `eam_asset_custodians_status_index` |
| `eam_asset_disposals` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->users` | `eam_asset_disposals_workflow_instance_id_index, eam_asset_disposals_status_index` |
| `eam_asset_documents` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->users` | `eam_asset_documents_expiry_date_index, eam_asset_documents_document_type_index` |
| `eam_asset_locations` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_asset_locations` | `eam_asset_locations_warehouse_id_index, eam_asset_locations_parent_id_index` |
| `eam_asset_relationships` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_fixed_assets` | `eam_asset_relationships_relationship_type_index` |
| `eam_asset_transfers` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_asset_locations...` | `eam_asset_transfers_workflow_instance_id_index, eam_asset_transfers_transfer_number_index` |
| `eam_asset_valuations` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->users` | `eam_asset_valuations_workflow_instance_id_index, eam_asset_valuations_valuation_type_index` |
| `eam_depreciation_runs` | Tenant-Scoped | `id` | `undefined->tenants, undefined->users` | `eam_depreciation_runs_status_index, eam_depreciation_runs_run_number_index` |
| `eam_depreciation_schedules` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_depreciation_runs` | `eam_depreciation_schedules_status_index, eam_depreciation_schedules_period_code_index` |
| `eam_fixed_assets` | Tenant-Scoped | `id` | `undefined->users, undefined->eam_asset_locations, undefined->eam_asset_classes...` | `eam_fixed_assets_workflow_instance_id_index, eam_fixed_assets_supplier_id_index` |
| `eam_maintenance_activities` | Tenant-Scoped | `id` | `undefined->eam_maintenance_work_orders, undefined->eam_fixed_assets` | `eam_maintenance_activities_work_order_id_index, eam_maintenance_activities_tenant_id_index` |
| `eam_maintenance_plans` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_asset_classes` | `eam_maintenance_plans_plan_code_index, eam_maintenance_plans_next_due_date_index` |
| `eam_maintenance_work_orders` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->eam_maintenance_plans...` | `eam_maintenance_work_orders_workflow_instance_id_index, eam_maintenance_work_orders_work_order_number_index` |
| `eam_project_asset_allocations` | Tenant-Scoped | `id` | `undefined->tenants, undefined->eam_fixed_assets, undefined->users` | `eam_project_asset_allocations_status_index, eam_project_asset_allocations_project_id_index` |

---

## Detailed Entity Schema & Data Dictionary

### `eam_asset_assignments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `asset_id` -> `eam_fixed_assets(id)`
- **Indexes & Constraints**:
  - `eam_asset_assignments_tenant_id_index` (Unique: No)
  - `eam_asset_assignments_status_index` (Unique: No)
  - `eam_asset_assignments_project_id_index` (Unique: No)
  - `eam_asset_assignments_location_id_index` (Unique: No)
  - `eam_asset_assignments_department_id_index` (Unique: No)
  - `eam_asset_assignments_company_id_index` (Unique: No)
  - `eam_asset_assignments_assignee_id_index` (Unique: No)
  - `eam_asset_assignments_asset_id_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_assignments_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_assignments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `assignment_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `assignee_type` | `VARCHAR(255)` | No | `'employee'` | Operational entity attribute |
| `assignee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assignee |
| `assignee_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for location |
| `assigned_at` | `DATE` | No | NULL | Operational entity attribute |
| `expected_return_at` | `DATE` | Yes | NULL | Operational entity attribute |
| `returned_at` | `DATE` | Yes | NULL | Operational entity attribute |
| `condition_on_assignment` | `VARCHAR(255)` | No | `'good'` | Operational entity attribute |
| `condition_on_return` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `assigned_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_categories`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `parent_id` -> `eam_asset_categories(id)`
- **Indexes & Constraints**:
  - `eam_asset_categories_parent_id_index` (Unique: No)
  - `eam_asset_categories_company_id_index` (Unique: No)
  - `eam_asset_categories_code_index` (Unique: No)
  - `eam_asset_categories_asset_type_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_categories_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `parent_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `asset_type` | `VARCHAR(255)` | No | `'tangible'` | Operational entity attribute |
| `depreciation_method` | `VARCHAR(255)` | No | `'straight_line'` | Operational entity attribute |
| `useful_life_years` | `INTEGER` | No | `5` | Operational entity attribute |
| `useful_life_months` | `INTEGER` | No | `60` | Operational entity attribute |
| `statutory_rate_percent` | `NUMERIC(16, 4)` | No | `20` | Monetary or financial decimal quantity |
| `salvage_value_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `gl_asset_account_code` | `VARCHAR(255)` | No | `'1600'` | Unique business identification code or document number |
| `gl_accumulated_depreciation_code` | `VARCHAR(255)` | No | `'1650'` | Unique business identification code or document number |
| `gl_depreciation_expense_code` | `VARCHAR(255)` | No | `'6400'` | Unique business identification code or document number |
| `gl_impairment_account_code` | `VARCHAR(255)` | No | `'6450'` | Unique business identification code or document number |
| `gl_revaluation_reserve_code` | `VARCHAR(255)` | No | `'3300'` | Unique business identification code or document number |
| `gl_disposal_gain_loss_code` | `VARCHAR(255)` | No | `'7500'` | Unique business identification code or document number |
| `gl_clearing_account_code` | `VARCHAR(255)` | No | `'2150'` | Unique business identification code or document number |
| `is_depreciable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_classes`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `eam_asset_classes_code_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_classes_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_classes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `criticality` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `default_maintenance_interval_days` | `INTEGER` | No | `180` | Operational entity attribute |
| `requires_custodian` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `requires_calibration` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `technical_schema` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_components`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `parent_asset_id` -> `eam_fixed_assets(id)`
  - `component_asset_id` -> `eam_fixed_assets(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_eam_asset_components_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `parent_asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for parent_asset |
| `component_asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for component_asset |
| `component_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `serial_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `cost_allocation` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `useful_life_months` | `INTEGER` | No | `36` | Operational entity attribute |
| `condition` | `VARCHAR(255)` | No | `'new'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `installed_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_custodians`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `custodian_user_id` -> `users(id)`
  - `assigned_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_asset_custodians_status_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_custodians_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `custodian_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for custodian_user |
| `assigned_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_by_user |
| `department` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `assigned_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `expected_return_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `returned_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `condition_on_checkout` | `VARCHAR(255)` | No | `'good'` | Operational entity attribute |
| `condition_on_return` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_disposals`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `initiated_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_asset_disposals_workflow_instance_id_index` (Unique: No)
  - `eam_asset_disposals_status_index` (Unique: No)
  - `eam_asset_disposals_journal_entry_id_index` (Unique: No)
  - `eam_asset_disposals_disposal_type_index` (Unique: No)
  - `eam_asset_disposals_disposal_number_index` (Unique: No)
  - `eam_asset_disposals_buyer_contact_id_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_disposals_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_disposals_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `disposal_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `disposal_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `disposal_date` | `DATE` | No | NULL | Operational entity attribute |
| `asset_cost_at_disposal` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `accumulated_depreciation_at_disposal` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `carrying_amount_at_disposal` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `proceeds_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `disposal_costs` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `gain_loss_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `buyer_contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for buyer_contact |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `initiated_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for initiated_by_user |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_documents`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `uploaded_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_asset_documents_expiry_date_index` (Unique: No)
  - `eam_asset_documents_document_type_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_documents_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `document_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `document_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `file_path` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `issue_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `expiry_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `uploaded_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for uploaded_by_user |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_locations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `parent_id` -> `eam_asset_locations(id)`
- **Indexes & Constraints**:
  - `eam_asset_locations_warehouse_id_index` (Unique: No)
  - `eam_asset_locations_parent_id_index` (Unique: No)
  - `eam_asset_locations_code_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_locations_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_locations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `parent_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent |
| `warehouse_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `location_type` | `VARCHAR(255)` | No | `'facility'` | Operational entity attribute |
| `address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `city` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `latitude` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `longitude` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_relationships`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `source_asset_id` -> `eam_fixed_assets(id)`
  - `target_asset_id` -> `eam_fixed_assets(id)`
- **Indexes & Constraints**:
  - `eam_asset_relationships_relationship_type_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_relationships_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_relationships_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `source_asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for source_asset |
| `target_asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for target_asset |
| `relationship_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_critical_dependency` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_asset_transfers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `from_location_id` -> `eam_asset_locations(id)`
  - `to_location_id` -> `eam_asset_locations(id)`
  - `from_custodian_id` -> `users(id)`
  - `to_custodian_id` -> `users(id)`
  - `initiated_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_asset_transfers_workflow_instance_id_index` (Unique: No)
  - `eam_asset_transfers_transfer_number_index` (Unique: No)
  - `eam_asset_transfers_to_project_id_index` (Unique: No)
  - `eam_asset_transfers_status_index` (Unique: No)
  - `eam_asset_transfers_from_project_id_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_transfers_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_transfers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `transfer_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `from_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_location |
| `to_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_location |
| `from_custodian_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_custodian |
| `to_custodian_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_custodian |
| `from_project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_project |
| `to_project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_project |
| `transfer_date` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `initiated_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for initiated_by_user |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `locked_by_workflow_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |

---

### `eam_asset_valuations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `created_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_asset_valuations_workflow_instance_id_index` (Unique: No)
  - `eam_asset_valuations_valuation_type_index` (Unique: No)
  - `eam_asset_valuations_valuation_number_index` (Unique: No)
  - `eam_asset_valuations_status_index` (Unique: No)
  - `eam_asset_valuations_journal_entry_id_index` (Unique: No)
  - `sqlite_autoindex_eam_asset_valuations_2` (Unique: Yes)
  - `sqlite_autoindex_eam_asset_valuations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `valuation_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `valuation_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `valuation_date` | `DATE` | No | NULL | Operational entity attribute |
| `carrying_amount_before` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `fair_value` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `value_in_use` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `recoverable_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `adjustment_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `revaluation_reserve_delta` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `impairment_loss_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `carrying_amount_after` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `appraiser_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for created_by_user |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_depreciation_runs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `executed_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_depreciation_runs_status_index` (Unique: No)
  - `eam_depreciation_runs_run_number_index` (Unique: No)
  - `eam_depreciation_runs_period_code_index` (Unique: No)
  - `eam_depreciation_runs_fiscal_period_id_index` (Unique: No)
  - `eam_depreciation_runs_company_id_index` (Unique: No)
  - `sqlite_autoindex_eam_depreciation_runs_2` (Unique: Yes)
  - `sqlite_autoindex_eam_depreciation_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `run_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_type` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `ledger_type` | `VARCHAR(255)` | No | `'statutory'` | Operational entity attribute |
| `assets_processed_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `total_depreciation_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'calculated'` | State machine status indicator |
| `fiscal_period_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for fiscal_period |
| `executed_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for executed_by_user |
| `executed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `summary_metrics` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_depreciation_schedules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `run_id` -> `eam_depreciation_runs(id)`
- **Indexes & Constraints**:
  - `eam_depreciation_schedules_status_index` (Unique: No)
  - `eam_depreciation_schedules_period_code_index` (Unique: No)
  - `eam_depreciation_schedules_ledger_type_index` (Unique: No)
  - `eam_depreciation_schedules_journal_entry_id_index` (Unique: No)
  - `sqlite_autoindex_eam_depreciation_schedules_2` (Unique: Yes)
  - `sqlite_autoindex_eam_depreciation_schedules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `run_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for run |
| `ledger_type` | `VARCHAR(255)` | No | `'statutory'` | Operational entity attribute |
| `period_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_type` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `depreciation_method` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `opening_book_value` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `depreciation_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `closing_book_value` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `accumulated_depreciation` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `units_produced` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'calculated'` | State machine status indicator |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `calculated_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `calculation_snapshot` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_fixed_assets`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `custodian_user_id` -> `users(id)`
  - `location_id` -> `eam_asset_locations(id)`
  - `asset_class_id` -> `eam_asset_classes(id)`
  - `category_id` -> `eam_asset_categories(id)`
  - `tenant_id` -> `tenants(id)`
  - `parent_asset_id` -> `eam_fixed_assets(id)`
- **Indexes & Constraints**:
  - `eam_fixed_assets_workflow_instance_id_index` (Unique: No)
  - `eam_fixed_assets_supplier_id_index` (Unique: No)
  - `eam_fixed_assets_status_index` (Unique: No)
  - `eam_fixed_assets_serial_number_index` (Unique: No)
  - `eam_fixed_assets_purchase_receipt_id_index` (Unique: No)
  - `eam_fixed_assets_purchase_order_id_index` (Unique: No)
  - `eam_fixed_assets_project_id_index` (Unique: No)
  - `eam_fixed_assets_parent_asset_id_index` (Unique: No)
  - `eam_fixed_assets_inventory_item_id_index` (Unique: No)
  - `eam_fixed_assets_condition_index` (Unique: No)
  - `eam_fixed_assets_company_id_index` (Unique: No)
  - `eam_fixed_assets_barcode_tag_index` (Unique: No)
  - `eam_fixed_assets_asset_number_index` (Unique: No)
  - `eam_fixed_assets_approval_status_index` (Unique: No)
  - `sqlite_autoindex_eam_fixed_assets_2` (Unique: Yes)
  - `sqlite_autoindex_eam_fixed_assets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for category |
| `asset_class_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset_class |
| `location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for location |
| `parent_asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_asset |
| `custodian_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for custodian_user |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `supplier_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier |
| `purchase_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_order |
| `purchase_receipt_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_receipt |
| `inventory_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for inventory_item |
| `asset_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `barcode_tag` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `serial_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `condition` | `VARCHAR(255)` | No | `'new'` | Operational entity attribute |
| `acquisition_type` | `VARCHAR(255)` | No | `'purchase'` | Operational entity attribute |
| `acquisition_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `capitalization_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `commissioning_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `in_service_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `warranty_expiry_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `retirement_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `disposal_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `acquisition_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `capitalized_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `salvage_value` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `depreciable_base` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `accumulated_depreciation` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `impairment_loss_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `revaluation_surplus_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `carrying_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `replacement_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `depreciation_method` | `VARCHAR(255)` | No | `'straight_line'` | Operational entity attribute |
| `useful_life_years` | `INTEGER` | No | `5` | Operational entity attribute |
| `useful_life_months` | `INTEGER` | No | `60` | Operational entity attribute |
| `depreciation_rate_percent` | `NUMERIC(16, 4)` | No | `20` | Monetary or financial decimal quantity |
| `total_expected_units` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `consumed_units` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `last_depreciation_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_depreciable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_fully_depreciated` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'not_required'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `specifications` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_maintenance_activities`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `work_order_id` -> `eam_maintenance_work_orders(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
- **Indexes & Constraints**:
  - `eam_maintenance_activities_work_order_id_index` (Unique: No)
  - `eam_maintenance_activities_tenant_id_index` (Unique: No)
  - `eam_maintenance_activities_status_index` (Unique: No)
  - `eam_maintenance_activities_performed_by_index` (Unique: No)
  - `eam_maintenance_activities_company_id_index` (Unique: No)
  - `eam_maintenance_activities_asset_id_index` (Unique: No)
  - `sqlite_autoindex_eam_maintenance_activities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `activity_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `activity_type` | `VARCHAR(255)` | No | `'inspection'` | Operational entity attribute |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `performed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `duration_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `labor_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `spare_parts_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `spare_parts_consumed` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'completed'` | State machine status indicator |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_maintenance_plans`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `asset_class_id` -> `eam_asset_classes(id)`
- **Indexes & Constraints**:
  - `eam_maintenance_plans_plan_code_index` (Unique: No)
  - `eam_maintenance_plans_next_due_date_index` (Unique: No)
  - `eam_maintenance_plans_maintenance_type_index` (Unique: No)
  - `sqlite_autoindex_eam_maintenance_plans_2` (Unique: Yes)
  - `sqlite_autoindex_eam_maintenance_plans_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset |
| `asset_class_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset_class |
| `plan_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `maintenance_type` | `VARCHAR(255)` | No | `'preventive'` | Operational entity attribute |
| `frequency_days` | `INTEGER` | No | `90` | Operational entity attribute |
| `meter_interval_units` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `estimated_duration_hours` | `NUMERIC(16, 4)` | No | `2` | Operational entity attribute |
| `estimated_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `last_executed_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `next_due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `checklist` | `TEXT` | Yes | NULL | Operational entity attribute |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `eam_maintenance_work_orders`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `plan_id` -> `eam_maintenance_plans(id)`
  - `assigned_technician_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_maintenance_work_orders_workflow_instance_id_index` (Unique: No)
  - `eam_maintenance_work_orders_work_order_number_index` (Unique: No)
  - `eam_maintenance_work_orders_status_index` (Unique: No)
  - `eam_maintenance_work_orders_priority_index` (Unique: No)
  - `eam_maintenance_work_orders_maintenance_type_index` (Unique: No)
  - `sqlite_autoindex_eam_maintenance_work_orders_2` (Unique: Yes)
  - `sqlite_autoindex_eam_maintenance_work_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `plan_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for plan |
| `work_order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `maintenance_type` | `VARCHAR(255)` | No | `'preventive'` | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'scheduled'` | State machine status indicator |
| `scheduled_date` | `DATE` | No | NULL | Operational entity attribute |
| `started_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `downtime_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `labor_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `parts_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `external_service_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `capitalize_as_upgrade` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `condition_after_maintenance` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `assigned_technician_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_technician |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `problem_description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `resolution_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `parts_consumed` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `approval_status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `locked_by_workflow_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |

---

### `eam_project_asset_allocations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `asset_id` -> `eam_fixed_assets(id)`
  - `allocated_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `eam_project_asset_allocations_status_index` (Unique: No)
  - `eam_project_asset_allocations_project_id_index` (Unique: No)
  - `sqlite_autoindex_eam_project_asset_allocations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `asset_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for asset |
| `project_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for project |
| `allocated_from` | `DATE` | No | NULL | Operational entity attribute |
| `allocated_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `daily_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `utilized_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `utilized_days` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `attributed_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `allocated_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for allocated_by_user |
| `released_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

