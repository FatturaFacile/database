# Module Reference: Manufacturing, Bills of Materials & MRP

**Module ID**: `11_manufacturing_and_mrp`  
**Tables Count**: `29`  
**Description**: Multi-level BOMs, work centers, routings, production orders, shop floor tracking, quality inspections, and costing.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `bills_of_materials` | Shared Lookup | `id` | `undefined->tenants, undefined->products` | `bills_of_materials_tenant_id_index` |
| `bom_items` | System / Global | `id` | `undefined->bills_of_materials, undefined->products` | `PRIMARY` |
| `mfg_bom_components` | Tenant-Scoped | `id` | `undefined->mfg_boms` | `mfg_bom_components_tenant_id_index, mfg_bom_components_component_item_id_index` |
| `mfg_boms` | Tenant-Scoped | `id` | None | `mfg_boms_tenant_id_index, mfg_boms_status_index` |
| `mfg_engineering_change_orders` | Tenant-Scoped | `id` | None | `mfg_engineering_change_orders_tenant_id_index, mfg_engineering_change_orders_status_index` |
| `mfg_items` | Tenant-Scoped | `id` | None | `mfg_items_tenant_id_index, mfg_items_stock_item_id_index` |
| `mfg_labor_time_logs` | Tenant-Scoped | `id` | `undefined->mfg_shop_floor_executions` | `mfg_labor_time_logs_tenant_id_index, mfg_labor_time_logs_operator_id_index` |
| `mfg_machine_centers` | Tenant-Scoped | `id` | `undefined->mfg_work_centers` | `mfg_machine_centers_work_center_id_index, mfg_machine_centers_tenant_id_index` |
| `mfg_machine_logs` | Tenant-Scoped | `id` | `undefined->mfg_shop_floor_executions` | `mfg_machine_logs_tenant_id_index, mfg_machine_logs_machine_id_index` |
| `mfg_mrp_peggings` | Tenant-Scoped | `id` | `undefined->mfg_mrp_planned_orders` | `mfg_mrp_peggings_tenant_id_index, mfg_mrp_peggings_planned_order_id_index` |
| `mfg_mrp_planned_orders` | Tenant-Scoped | `id` | `undefined->mfg_mrp_runs` | `mfg_mrp_planned_orders_tenant_id_index, mfg_mrp_planned_orders_status_index` |
| `mfg_mrp_runs` | Tenant-Scoped | `id` | None | `mfg_mrp_runs_tenant_id_index, mfg_mrp_runs_status_index` |
| `mfg_mrp_shortages` | Tenant-Scoped | `id` | `undefined->mfg_mrp_runs` | `mfg_mrp_shortages_tenant_id_index, mfg_mrp_shortages_mrp_run_id_index` |
| `mfg_operations` | Tenant-Scoped | `id` | `undefined->mfg_routings, undefined->mfg_work_centers` | `mfg_operations_work_center_id_index, mfg_operations_tenant_id_index` |
| `mfg_production_costs` | Tenant-Scoped | `id` | `undefined->mfg_production_orders` | `mfg_production_costs_tenant_id_index, mfg_production_costs_production_order_id_index` |
| `mfg_production_order_lines` | Tenant-Scoped | `id` | `undefined->mfg_production_orders` | `mfg_production_order_lines_tenant_id_index, mfg_production_order_lines_production_order_id_index` |
| `mfg_production_order_operations` | Tenant-Scoped | `id` | `undefined->mfg_production_orders` | `mfg_production_order_operations_work_center_id_index, mfg_production_order_operations_tenant_id_index` |
| `mfg_production_orders` | Tenant-Scoped | `id` | None | `mfg_production_orders_tenant_id_index, mfg_production_orders_status_index` |
| `mfg_production_versions` | Tenant-Scoped | `id` | `undefined->mfg_boms, undefined->mfg_routings` | `mfg_production_versions_version_code_index, mfg_production_versions_tenant_id_index` |
| `mfg_quality_characteristics` | Tenant-Scoped | `id` | `undefined->mfg_quality_plans` | `mfg_quality_characteristics_tenant_id_index, mfg_quality_characteristics_quality_plan_id_index` |
| `mfg_quality_inspections` | Tenant-Scoped | `id` | `undefined->mfg_quality_plans` | `mfg_quality_inspections_tenant_id_index, mfg_quality_inspections_status_index` |
| `mfg_quality_non_conformances` | Tenant-Scoped | `id` | None | `mfg_quality_non_conformances_tenant_id_index, mfg_quality_non_conformances_status_index` |
| `mfg_quality_plans` | Tenant-Scoped | `id` | None | `mfg_quality_plans_tenant_id_index, mfg_quality_plans_plan_code_index` |
| `mfg_routings` | Tenant-Scoped | `id` | None | `mfg_routings_tenant_id_index, mfg_routings_status_index` |
| `mfg_shop_floor_executions` | Tenant-Scoped | `id` | `undefined->mfg_production_orders` | `mfg_shop_floor_executions_work_center_id_index, mfg_shop_floor_executions_tenant_id_index` |
| `mfg_work_center_capacities` | Tenant-Scoped | `id` | `undefined->mfg_work_centers` | `mfg_work_center_capacities_work_center_id_index, mfg_work_center_capacities_tenant_id_index` |
| `mfg_work_centers` | Tenant-Scoped | `id` | None | `mfg_work_centers_work_center_code_index, mfg_work_centers_tenant_id_index` |
| `production_order_stages` | System / Global | `id` | `undefined->production_orders` | `production_order_stages_status_index` |
| `production_orders` | Shared Lookup | `id` | `undefined->tenants, undefined->bills_of_materials` | `production_orders_status_index, production_orders_order_number_index` |

---

## Detailed Entity Schema & Data Dictionary

### `bills_of_materials`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `finished_product_id` -> `products(id)`
- **Indexes & Constraints**:
  - `bills_of_materials_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_bills_of_materials_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `finished_product_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for finished_product |
| `version` | `VARCHAR(255)` | No | `'1.0'` | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bom_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `bill_of_materials_id` -> `bills_of_materials(id)`
  - `raw_product_id` -> `products(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_bom_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `bill_of_materials_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bill_of_materials |
| `raw_product_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for raw_product |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `scrap_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `mfg_bom_components`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `bom_id` -> `mfg_boms(id)`
- **Indexes & Constraints**:
  - `mfg_bom_components_tenant_id_index` (Unique: No)
  - `mfg_bom_components_component_item_id_index` (Unique: No)
  - `mfg_bom_components_bom_id_index` (Unique: No)
  - `mfg_bom_components_alternate_for_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_bom_components_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bom_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bom |
| `component_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for component_item |
| `sequence` | `INTEGER` | No | `10` | Operational entity attribute |
| `quantity_per` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `scrap_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `yield_percentage` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `is_phantom` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `alternate_for_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for alternate_for |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_boms`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_boms_tenant_id_index` (Unique: No)
  - `mfg_boms_status_index` (Unique: No)
  - `mfg_boms_mfg_item_id_index` (Unique: No)
  - `mfg_boms_bom_type_index` (Unique: No)
  - `mfg_boms_bom_number_index` (Unique: No)
  - `sqlite_autoindex_mfg_boms_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_boms_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bom_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `revision` | `VARCHAR(255)` | No | `'A'` | Operational entity attribute |
| `version` | `INTEGER` | No | `1` | Operational entity attribute |
| `bom_type` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `base_quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `effective_from` | `DATE` | Yes | NULL | Operational entity attribute |
| `effective_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_engineering_change_orders`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_engineering_change_orders_tenant_id_index` (Unique: No)
  - `mfg_engineering_change_orders_status_index` (Unique: No)
  - `mfg_engineering_change_orders_eco_number_index` (Unique: No)
  - `sqlite_autoindex_mfg_engineering_change_orders_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_engineering_change_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `eco_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `reason` | `TEXT` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `change_type` | `VARCHAR(255)` | No | `'bom_change'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `effective_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `requested_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `implemented_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `change_payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_items`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_items_tenant_id_index` (Unique: No)
  - `mfg_items_stock_item_id_index` (Unique: No)
  - `mfg_items_item_type_index` (Unique: No)
  - `mfg_items_item_code_index` (Unique: No)
  - `mfg_items_is_active_index` (Unique: No)
  - `mfg_items_default_routing_id_index` (Unique: No)
  - `mfg_items_default_bom_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_items_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `item_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `item_type` | `VARCHAR(255)` | No | `'raw_material'` | Operational entity attribute |
| `stock_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for stock_item |
| `default_bom_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for default_bom |
| `default_routing_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for default_routing |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `standard_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `current_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scrap_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `safety_stock` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `min_lot_size` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `max_lot_size` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `lead_time_days` | `INTEGER` | No | `1` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `custom_attributes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_labor_time_logs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `execution_id` -> `mfg_shop_floor_executions(id)`
- **Indexes & Constraints**:
  - `mfg_labor_time_logs_tenant_id_index` (Unique: No)
  - `mfg_labor_time_logs_operator_id_index` (Unique: No)
  - `mfg_labor_time_logs_execution_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_labor_time_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `execution_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for execution |
| `operator_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for operator |
| `start_time` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `end_time` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `duration_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `labor_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_machine_centers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `work_center_id` -> `mfg_work_centers(id)`
- **Indexes & Constraints**:
  - `mfg_machine_centers_work_center_id_index` (Unique: No)
  - `mfg_machine_centers_tenant_id_index` (Unique: No)
  - `mfg_machine_centers_status_index` (Unique: No)
  - `mfg_machine_centers_machine_code_index` (Unique: No)
  - `mfg_machine_centers_asset_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_machine_centers_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_machine_centers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `machine_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `work_center_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_center |
| `asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `power_kw` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `last_serviced_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_machine_logs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `execution_id` -> `mfg_shop_floor_executions(id)`
- **Indexes & Constraints**:
  - `mfg_machine_logs_tenant_id_index` (Unique: No)
  - `mfg_machine_logs_machine_id_index` (Unique: No)
  - `mfg_machine_logs_execution_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_machine_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `execution_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for execution |
| `machine_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for machine |
| `start_time` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `end_time` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `run_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `downtime_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `machine_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_mrp_peggings`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `planned_order_id` -> `mfg_mrp_planned_orders(id)`
- **Indexes & Constraints**:
  - `mfg_mrp_peggings_tenant_id_index` (Unique: No)
  - `mfg_mrp_peggings_planned_order_id_index` (Unique: No)
  - `mfg_mrp_peggings_demand_type_index` (Unique: No)
  - `mfg_mrp_peggings_demand_reference_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_mrp_peggings_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `planned_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for planned_order |
| `demand_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `demand_reference_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for demand_reference |
| `pegged_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_mrp_planned_orders`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `mrp_run_id` -> `mfg_mrp_runs(id)`
- **Indexes & Constraints**:
  - `mfg_mrp_planned_orders_tenant_id_index` (Unique: No)
  - `mfg_mrp_planned_orders_status_index` (Unique: No)
  - `mfg_mrp_planned_orders_routing_id_index` (Unique: No)
  - `mfg_mrp_planned_orders_planned_order_number_index` (Unique: No)
  - `mfg_mrp_planned_orders_order_type_index` (Unique: No)
  - `mfg_mrp_planned_orders_mrp_run_id_index` (Unique: No)
  - `mfg_mrp_planned_orders_mfg_item_id_index` (Unique: No)
  - `mfg_mrp_planned_orders_converted_order_id_index` (Unique: No)
  - `mfg_mrp_planned_orders_bom_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_mrp_planned_orders_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_mrp_planned_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `planned_order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mrp_run_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mrp_run |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `order_type` | `VARCHAR(255)` | No | `'make'` | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'planned'` | State machine status indicator |
| `bom_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bom |
| `routing_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for routing |
| `converted_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for converted_order |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_mrp_runs`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_mrp_runs_tenant_id_index` (Unique: No)
  - `mfg_mrp_runs_status_index` (Unique: No)
  - `mfg_mrp_runs_run_type_index` (Unique: No)
  - `mfg_mrp_runs_run_number_index` (Unique: No)
  - `sqlite_autoindex_mfg_mrp_runs_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_mrp_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `run_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `run_type` | `VARCHAR(255)` | No | `'regenerative'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'running'` | State machine status indicator |
| `horizon_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `horizon_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `total_items_processed` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `total_planned_orders` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `total_shortages` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `executed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `executed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `error_message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `parameters` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_mrp_shortages`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `mrp_run_id` -> `mfg_mrp_runs(id)`
- **Indexes & Constraints**:
  - `mfg_mrp_shortages_tenant_id_index` (Unique: No)
  - `mfg_mrp_shortages_mrp_run_id_index` (Unique: No)
  - `mfg_mrp_shortages_mfg_item_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_mrp_shortages_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `mrp_run_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mrp_run |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `required_date` | `DATE` | No | NULL | Operational entity attribute |
| `gross_requirement` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `available_inventory` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scheduled_receipts` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `safety_stock` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `net_shortage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `recommended_action` | `VARCHAR(255)` | No | `'purchase_order'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_operations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `routing_id` -> `mfg_routings(id)`
  - `work_center_id` -> `mfg_work_centers(id)`
- **Indexes & Constraints**:
  - `mfg_operations_work_center_id_index` (Unique: No)
  - `mfg_operations_tenant_id_index` (Unique: No)
  - `mfg_operations_routing_id_index` (Unique: No)
  - `mfg_operations_operation_code_index` (Unique: No)
  - `mfg_operations_machine_center_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_operations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `routing_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for routing |
| `sequence` | `INTEGER` | No | `10` | Operational entity attribute |
| `operation_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `work_center_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_center |
| `machine_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for machine_center |
| `setup_time_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `run_time_minutes_per_unit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `labor_time_minutes_per_unit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `queue_time_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `wait_time_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `teardown_time_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `standard_labor_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `standard_machine_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_production_costs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `production_order_id` -> `mfg_production_orders(id)`
- **Indexes & Constraints**:
  - `mfg_production_costs_tenant_id_index` (Unique: No)
  - `mfg_production_costs_production_order_id_index` (Unique: No)
  - `mfg_production_costs_is_posted_to_gl_index` (Unique: No)
  - `mfg_production_costs_gl_journal_id_index` (Unique: No)
  - `mfg_production_costs_cost_type_index` (Unique: No)
  - `sqlite_autoindex_mfg_production_costs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `production_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order |
| `cost_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `standard_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `variance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_posted_to_gl` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `gl_journal_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_production_order_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `production_order_id` -> `mfg_production_orders(id)`
- **Indexes & Constraints**:
  - `mfg_production_order_lines_tenant_id_index` (Unique: No)
  - `mfg_production_order_lines_production_order_id_index` (Unique: No)
  - `mfg_production_order_lines_operation_id_index` (Unique: No)
  - `mfg_production_order_lines_mfg_item_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_production_order_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `production_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `operation_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for operation |
| `required_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `allocated_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `consumed_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scrapped_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_production_order_operations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `production_order_id` -> `mfg_production_orders(id)`
- **Indexes & Constraints**:
  - `mfg_production_order_operations_work_center_id_index` (Unique: No)
  - `mfg_production_order_operations_tenant_id_index` (Unique: No)
  - `mfg_production_order_operations_status_index` (Unique: No)
  - `mfg_production_order_operations_production_order_id_index` (Unique: No)
  - `mfg_production_order_operations_operation_id_index` (Unique: No)
  - `mfg_production_order_operations_machine_center_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_production_order_operations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `production_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order |
| `operation_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for operation |
| `sequence` | `INTEGER` | No | `10` | Operational entity attribute |
| `work_center_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_center |
| `machine_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for machine_center |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `planned_setup_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_setup_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `planned_run_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_run_minutes` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `completed_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scrapped_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_production_orders`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_production_orders_tenant_id_index` (Unique: No)
  - `mfg_production_orders_status_index` (Unique: No)
  - `mfg_production_orders_routing_id_index` (Unique: No)
  - `mfg_production_orders_project_id_index` (Unique: No)
  - `mfg_production_orders_order_number_index` (Unique: No)
  - `mfg_production_orders_mfg_item_id_index` (Unique: No)
  - `mfg_production_orders_bom_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_production_orders_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_production_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `bom_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bom |
| `routing_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for routing |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `status` | `VARCHAR(255)` | No | `'planned'` | State machine status indicator |
| `target_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `completed_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scrapped_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCS'` | Operational entity attribute |
| `planned_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `planned_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `actual_start_date` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `actual_end_date` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `standard_cost_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `actual_cost_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `variance_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `lock_version` | `INTEGER` | No | `1` | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_production_versions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `bom_id` -> `mfg_boms(id)`
  - `routing_id` -> `mfg_routings(id)`
- **Indexes & Constraints**:
  - `mfg_production_versions_version_code_index` (Unique: No)
  - `mfg_production_versions_tenant_id_index` (Unique: No)
  - `mfg_production_versions_routing_id_index` (Unique: No)
  - `mfg_production_versions_mfg_item_id_index` (Unique: No)
  - `mfg_production_versions_bom_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_production_versions_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_production_versions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `version_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `bom_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bom |
| `routing_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for routing |
| `valid_from` | `DATE` | Yes | NULL | Operational entity attribute |
| `valid_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `min_lot_size` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `max_lot_size` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_quality_characteristics`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `quality_plan_id` -> `mfg_quality_plans(id)`
- **Indexes & Constraints**:
  - `mfg_quality_characteristics_tenant_id_index` (Unique: No)
  - `mfg_quality_characteristics_quality_plan_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_quality_characteristics_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `quality_plan_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for quality_plan |
| `characteristic_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `target_value` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `min_tolerance` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `max_tolerance` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'MM'` | Operational entity attribute |
| `inspection_method` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_critical` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_quality_inspections`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `quality_plan_id` -> `mfg_quality_plans(id)`
- **Indexes & Constraints**:
  - `mfg_quality_inspections_tenant_id_index` (Unique: No)
  - `mfg_quality_inspections_status_index` (Unique: No)
  - `mfg_quality_inspections_quality_plan_id_index` (Unique: No)
  - `mfg_quality_inspections_production_order_id_index` (Unique: No)
  - `mfg_quality_inspections_operation_id_index` (Unique: No)
  - `mfg_quality_inspections_inspector_id_index` (Unique: No)
  - `mfg_quality_inspections_inspection_number_index` (Unique: No)
  - `sqlite_autoindex_mfg_quality_inspections_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_quality_inspections_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `inspection_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `quality_plan_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for quality_plan |
| `production_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for production_order |
| `operation_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for operation |
| `inspector_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for inspector |
| `sample_size` | `INTEGER` | No | `1` | Operational entity attribute |
| `defect_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `inspected_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `characteristic_results` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_quality_non_conformances`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_quality_non_conformances_tenant_id_index` (Unique: No)
  - `mfg_quality_non_conformances_status_index` (Unique: No)
  - `mfg_quality_non_conformances_severity_index` (Unique: No)
  - `mfg_quality_non_conformances_quality_inspection_id_index` (Unique: No)
  - `mfg_quality_non_conformances_production_order_id_index` (Unique: No)
  - `mfg_quality_non_conformances_nc_number_index` (Unique: No)
  - `mfg_quality_non_conformances_disposition_index` (Unique: No)
  - `sqlite_autoindex_mfg_quality_non_conformances_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_quality_non_conformances_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `nc_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `quality_inspection_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for quality_inspection |
| `production_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for production_order |
| `severity` | `VARCHAR(255)` | No | `'major'` | Operational entity attribute |
| `defect_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `disposition` | `VARCHAR(255)` | No | `'investigating'` | Operational entity attribute |
| `corrective_action` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `reported_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `resolved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `resolved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_quality_plans`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_quality_plans_tenant_id_index` (Unique: No)
  - `mfg_quality_plans_plan_code_index` (Unique: No)
  - `mfg_quality_plans_mfg_item_id_index` (Unique: No)
  - `mfg_quality_plans_is_active_index` (Unique: No)
  - `mfg_quality_plans_inspection_type_index` (Unique: No)
  - `sqlite_autoindex_mfg_quality_plans_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_quality_plans_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `plan_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `inspection_type` | `VARCHAR(255)` | No | `'in_process'` | Operational entity attribute |
| `mfg_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for mfg_item |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_routings`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_routings_tenant_id_index` (Unique: No)
  - `mfg_routings_status_index` (Unique: No)
  - `mfg_routings_routing_number_index` (Unique: No)
  - `mfg_routings_mfg_item_id_index` (Unique: No)
  - `sqlite_autoindex_mfg_routings_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_routings_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `routing_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mfg_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for mfg_item |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `revision` | `VARCHAR(255)` | No | `'A'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_shop_floor_executions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `production_order_id` -> `mfg_production_orders(id)`
- **Indexes & Constraints**:
  - `mfg_shop_floor_executions_work_center_id_index` (Unique: No)
  - `mfg_shop_floor_executions_tenant_id_index` (Unique: No)
  - `mfg_shop_floor_executions_status_index` (Unique: No)
  - `idx_f615bcfbefae5636_mfg_shop_floor_executions` (Unique: No)
  - `mfg_shop_floor_executions_production_order_id_index` (Unique: No)
  - `mfg_shop_floor_executions_operator_id_index` (Unique: No)
  - `mfg_shop_floor_executions_machine_id_index` (Unique: No)
  - `mfg_shop_floor_executions_execution_number_index` (Unique: No)
  - `sqlite_autoindex_mfg_shop_floor_executions_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_shop_floor_executions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `execution_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `production_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order |
| `production_order_operation_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order_operation |
| `work_center_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_center |
| `operator_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for operator |
| `machine_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for machine |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `good_units` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `scrap_units` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `started_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `downtime_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_work_center_capacities`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `work_center_id` -> `mfg_work_centers(id)`
- **Indexes & Constraints**:
  - `mfg_work_center_capacities_work_center_id_index` (Unique: No)
  - `mfg_work_center_capacities_tenant_id_index` (Unique: No)
  - `mfg_work_center_capacities_calendar_date_index` (Unique: No)
  - `sqlite_autoindex_mfg_work_center_capacities_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_work_center_capacities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `work_center_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_center |
| `calendar_date` | `DATE` | No | NULL | Operational entity attribute |
| `available_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `booked_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `utilization_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `mfg_work_centers`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `mfg_work_centers_work_center_code_index` (Unique: No)
  - `mfg_work_centers_tenant_id_index` (Unique: No)
  - `mfg_work_centers_status_index` (Unique: No)
  - `sqlite_autoindex_mfg_work_centers_2` (Unique: Yes)
  - `sqlite_autoindex_mfg_work_centers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `work_center_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `department_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `capacity_hours_per_day` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `efficiency_rate` | `NUMERIC(16, 4)` | No | `100` | Monetary or financial decimal quantity |
| `availability_rate` | `NUMERIC(16, 4)` | No | `100` | Monetary or financial decimal quantity |
| `hourly_cost_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `hourly_overhead_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `production_order_stages`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `production_order_id` -> `production_orders(id)`
- **Indexes & Constraints**:
  - `production_order_stages_status_index` (Unique: No)
  - `sqlite_autoindex_production_order_stages_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `production_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for production_order |
| `stage_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `sequence` | `INTEGER` | No | `1` | Operational entity attribute |
| `planned_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `production_orders`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `bill_of_materials_id` -> `bills_of_materials(id)`
- **Indexes & Constraints**:
  - `production_orders_status_index` (Unique: No)
  - `production_orders_order_number_index` (Unique: No)
  - `sqlite_autoindex_production_orders_2` (Unique: Yes)
  - `sqlite_autoindex_production_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bill_of_materials_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bill_of_materials |
| `order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `target_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `produced_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'planned'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

