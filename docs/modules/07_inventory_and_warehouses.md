# Module Reference: Inventory, Warehouses & Logistics

**Module ID**: `07_inventory_and_warehouses`  
**Tables Count**: `28`  
**Description**: Multi-warehouse storage, bins, stock items, lots, serial numbers, quants, reservations, and pick/pack operations.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `inventory_adjustments` | Tenant-Scoped | `id` | `undefined->warehouses` | `inventory_adjustments_tenant_id_index, inventory_adjustments_company_id_index` |
| `inventory_audit_entries` | Tenant-Scoped | `id` | `undefined->stock_items` | `inventory_audit_entries_tenant_id_index, inventory_audit_entries_movement_id_index` |
| `inventory_count_lines` | Tenant-Scoped | `id` | `undefined->inventory_count_sessions, undefined->warehouse_bins, undefined->stock_items...` | `inventory_count_lines_tenant_id_index` |
| `inventory_count_sessions` | Tenant-Scoped | `id` | `undefined->warehouses` | `inventory_count_sessions_tenant_id_index, inventory_count_sessions_company_id_index` |
| `inventory_movement_type_translations` | Shared Lookup | `id` | `undefined->inventory_movement_types` | `inventory_movement_type_translations_tenant_id_index, inventory_movement_type_translations_locale_index` |
| `inventory_movement_types` | Shared Lookup | `id` | None | `inventory_movement_types_tenant_id_index` |
| `price_list_items` | System / Global | `id` | `undefined->price_lists, undefined->products` | `PRIMARY` |
| `price_lists` | Shared Lookup | `id` | `undefined->tenants` | `price_lists_tenant_id_is_default_index` |
| `product_brands` | Shared Lookup | `id` | `undefined->tenants` | `PRIMARY` |
| `product_categories` | Shared Lookup | `id` | `undefined->tenants, undefined->product_categories` | `PRIMARY` |
| `products` | Shared Lookup | `id` | `undefined->units_of_measure, undefined->product_brands, undefined->product_categories...` | `products_sku_index, products_is_variant_index` |
| `stock_item_categories` | Tenant-Scoped | `id` | `undefined->stock_item_categories` | `stock_item_categories_tenant_id_index, stock_item_categories_company_id_index` |
| `stock_items` | Tenant-Scoped | `id` | `undefined->stock_item_categories` | `stock_items_tenant_id_index, stock_items_sku_index` |
| `stock_lots` | Tenant-Scoped | `id` | `undefined->stock_items` | `stock_lots_tenant_id_index, stock_lots_expiration_date_index` |
| `stock_movements` | Shared Lookup | `id` | `undefined->warehouses, undefined->products, undefined->tenants` | `stock_movements_type_index, stock_movements_tenant_id_created_at_index` |
| `stock_packing_lists` | Tenant-Scoped | `id` | `undefined->stock_pick_lists` | `stock_packing_lists_tenant_id_index` |
| `stock_pick_lines` | Tenant-Scoped | `id` | `undefined->stock_pick_lists, undefined->stock_items, undefined->warehouse_bins...` | `stock_pick_lines_tenant_id_index` |
| `stock_pick_lists` | Tenant-Scoped | `id` | `undefined->warehouses` | `stock_pick_lists_tenant_id_index, stock_pick_lists_company_id_index` |
| `stock_quants` | Tenant-Scoped | `id` | `undefined->warehouse_bins, undefined->stock_items, undefined->stock_lots` | `stock_quants_tenant_id_index, stock_quants_company_id_index` |
| `stock_reorder_rules` | Tenant-Scoped | `id` | `undefined->warehouses, undefined->stock_items` | `stock_reorder_rules_tenant_id_index, stock_reorder_rules_company_id_index` |
| `stock_reservations` | Tenant-Scoped | `id` | `undefined->stock_items, undefined->warehouses` | `stock_reservations_tenant_id_index, stock_reservations_company_id_index` |
| `stock_serial_numbers` | Tenant-Scoped | `id` | `undefined->stock_items, undefined->warehouse_bins, undefined->stock_lots` | `stock_serial_numbers_tenant_id_index, stock_serial_numbers_company_id_index` |
| `stock_valuation_snapshots` | Tenant-Scoped | `id` | `undefined->warehouses, undefined->stock_items` | `stock_valuation_snapshots_tenant_id_index, stock_valuation_snapshots_company_id_index` |
| `warehouse_aisles` | Tenant-Scoped | `id` | `undefined->warehouse_zones` | `warehouse_aisles_tenant_id_index` |
| `warehouse_bins` | Tenant-Scoped | `id` | `undefined->warehouse_racks` | `warehouse_bins_tenant_id_index, warehouse_bins_barcode_index` |
| `warehouse_racks` | Tenant-Scoped | `id` | `undefined->warehouse_aisles` | `warehouse_racks_tenant_id_index` |
| `warehouse_zones` | Tenant-Scoped | `id` | `undefined->warehouses` | `warehouse_zones_tenant_id_index` |
| `warehouses` | Shared Lookup | `id` | `undefined->tenants` | `warehouses_company_id_index, warehouses_code_index` |

---

## Detailed Entity Schema & Data Dictionary

### `inventory_adjustments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
- **Indexes & Constraints**:
  - `inventory_adjustments_tenant_id_index` (Unique: No)
  - `inventory_adjustments_company_id_index` (Unique: No)
  - `sqlite_autoindex_inventory_adjustments_2` (Unique: Yes)
  - `sqlite_autoindex_inventory_adjustments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `adjustment_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `reason` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `net_valuation_change` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `inventory_audit_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_item_id` -> `stock_items(id)`
- **Indexes & Constraints**:
  - `inventory_audit_entries_tenant_id_index` (Unique: No)
  - `inventory_audit_entries_movement_id_index` (Unique: No)
  - `inventory_audit_entries_company_id_index` (Unique: No)
  - `inventory_audit_entries_actor_user_id_index` (Unique: No)
  - `idx_inv_audit_item` (Unique: No)
  - `sqlite_autoindex_inventory_audit_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `movement_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for movement |
| `actor_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for actor_user |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity_change` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `valuation_impact` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `source_location_desc` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `dest_location_desc` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reason_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `inventory_count_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `inventory_count_session_id` -> `inventory_count_sessions(id)`
  - `warehouse_bin_id` -> `warehouse_bins(id)`
  - `stock_item_id` -> `stock_items(id)`
  - `lot_id` -> `stock_lots(id)`
- **Indexes & Constraints**:
  - `inventory_count_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_inventory_count_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `inventory_count_session_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for inventory_count_session |
| `warehouse_bin_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_bin |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lot |
| `system_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `counted_quantity` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `discrepancy_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `discrepancy_valuation` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `counted_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for counted_by_user |
| `counted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `inventory_count_sessions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
- **Indexes & Constraints**:
  - `inventory_count_sessions_tenant_id_index` (Unique: No)
  - `inventory_count_sessions_company_id_index` (Unique: No)
  - `sqlite_autoindex_inventory_count_sessions_2` (Unique: Yes)
  - `sqlite_autoindex_inventory_count_sessions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `session_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `count_type` | `VARCHAR(255)` | No | `'cycle'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'in_progress'` | State machine status indicator |
| `scheduled_date` | `DATE` | No | NULL | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `inventory_movement_type_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `movement_type_id` -> `inventory_movement_types(id)`
- **Indexes & Constraints**:
  - `inventory_movement_type_translations_tenant_id_index` (Unique: No)
  - `inventory_movement_type_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_inventory_movement_type_translations_2` (Unique: Yes)
  - `sqlite_autoindex_inventory_movement_type_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `movement_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for movement_type |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `inventory_movement_types`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `inventory_movement_types_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_inventory_movement_types_2` (Unique: Yes)
  - `sqlite_autoindex_inventory_movement_types_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `direction` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `affects_cogs` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `price_list_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `price_list_id` -> `price_lists(id)`
  - `product_id` -> `products(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_price_list_items_2` (Unique: Yes)
  - `sqlite_autoindex_price_list_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `price_list_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for price_list |
| `product_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for product |
| `price` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `min_quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `price_lists`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `price_lists_tenant_id_is_default_index` (Unique: No)
  - `sqlite_autoindex_price_lists_2` (Unique: Yes)
  - `sqlite_autoindex_price_lists_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `valid_from` | `DATE` | Yes | NULL | Operational entity attribute |
| `valid_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `product_brands`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_product_brands_2` (Unique: Yes)
  - `sqlite_autoindex_product_brands_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `product_categories`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `parent_id` -> `product_categories(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_product_categories_2` (Unique: Yes)
  - `sqlite_autoindex_product_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `parent_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `products`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `unit_of_measure_id` -> `units_of_measure(id)`
  - `brand_id` -> `product_brands(id)`
  - `category_id` -> `product_categories(id)`
  - `tenant_id` -> `tenants(id)`
  - `parent_id` -> `products(id)`
- **Indexes & Constraints**:
  - `products_sku_index` (Unique: No)
  - `products_is_variant_index` (Unique: No)
  - `products_barcode_index` (Unique: No)
  - `sqlite_autoindex_products_2` (Unique: Yes)
  - `sqlite_autoindex_products_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `sku` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `barcode` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `unit_measure` | `VARCHAR(255)` | No | `'PZ'` | Operational entity attribute |
| `cost_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `sale_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `22` | Monetary or financial decimal quantity |
| `hs_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `track_inventory` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for category |
| `brand_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for brand |
| `unit_of_measure_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for unit_of_measure |
| `parent_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent |
| `is_variant` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `attributes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `min_stock` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |

---

### `stock_item_categories`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `parent_category_id` -> `stock_item_categories(id)`
- **Indexes & Constraints**:
  - `stock_item_categories_tenant_id_index` (Unique: No)
  - `stock_item_categories_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_item_categories_2` (Unique: Yes)
  - `sqlite_autoindex_stock_item_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `parent_category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_category |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `valuation_method` | `VARCHAR(255)` | No | `'fifo'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_items`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `category_id` -> `stock_item_categories(id)`
- **Indexes & Constraints**:
  - `stock_items_tenant_id_index` (Unique: No)
  - `stock_items_sku_index` (Unique: No)
  - `stock_items_company_id_index` (Unique: No)
  - `stock_items_barcode_ean13_index` (Unique: No)
  - `stock_items_barcode_custom_index` (Unique: No)
  - `sqlite_autoindex_stock_items_2` (Unique: Yes)
  - `sqlite_autoindex_stock_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for category |
| `sku` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `barcode_ean13` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `barcode_custom` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `tracking_type` | `VARCHAR(255)` | No | `'none'` | Operational entity attribute |
| `standard_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `current_moving_average_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `weight_kg` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_lots`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_item_id` -> `stock_items(id)`
- **Indexes & Constraints**:
  - `stock_lots_tenant_id_index` (Unique: No)
  - `stock_lots_expiration_date_index` (Unique: No)
  - `stock_lots_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_lots_2` (Unique: Yes)
  - `sqlite_autoindex_stock_lots_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `lot_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `supplier_lot_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `supplier_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier |
| `manufacturing_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `expiration_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_quarantined` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_movements`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
  - `product_id` -> `products(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `stock_movements_type_index` (Unique: No)
  - `stock_movements_tenant_id_created_at_index` (Unique: No)
  - `stock_movements_stock_item_id_index` (Unique: No)
  - `stock_movements_source_location_id_index` (Unique: No)
  - `stock_movements_serial_number_id_index` (Unique: No)
  - `stock_movements_reference_type_reference_id_index` (Unique: No)
  - `stock_movements_movement_type_index` (Unique: No)
  - `stock_movements_lot_id_index` (Unique: No)
  - `stock_movements_executed_by_user_id_index` (Unique: No)
  - `stock_movements_executed_at_index` (Unique: No)
  - `stock_movements_destination_location_id_index` (Unique: No)
  - `stock_movements_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_movements_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `warehouse_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse |
| `type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `reference_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reference_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for reference |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `stock_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for stock_item |
| `source_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for source_location |
| `destination_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for destination_location |
| `lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lot |
| `serial_number_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for serial_number |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `total_valuation` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `movement_type` | `VARCHAR(255)` | No | `'internal_transfer'` | Operational entity attribute |
| `origin_document_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `origin_document_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for origin_document |
| `executed_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for executed_by_user |
| `executed_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_packing_lists`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_pick_list_id` -> `stock_pick_lists(id)`
- **Indexes & Constraints**:
  - `stock_packing_lists_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_stock_packing_lists_2` (Unique: Yes)
  - `sqlite_autoindex_stock_packing_lists_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `stock_pick_list_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_pick_list |
| `packing_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `total_packages` | `INTEGER` | No | `1` | Monetary or financial decimal quantity |
| `total_weight_kg` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `shipping_carrier` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `tracking_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `packed_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for packed_by_user |
| `packed_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_pick_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_pick_list_id` -> `stock_pick_lists(id)`
  - `stock_item_id` -> `stock_items(id)`
  - `warehouse_bin_id` -> `warehouse_bins(id)`
  - `lot_id` -> `stock_lots(id)`
- **Indexes & Constraints**:
  - `stock_pick_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_stock_pick_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `stock_pick_list_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_pick_list |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `warehouse_bin_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_bin |
| `lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lot |
| `quantity_to_pick` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `quantity_picked` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `picked_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_pick_lists`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
- **Indexes & Constraints**:
  - `stock_pick_lists_tenant_id_index` (Unique: No)
  - `stock_pick_lists_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_pick_lists_2` (Unique: Yes)
  - `sqlite_autoindex_stock_pick_lists_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `pick_list_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `assigned_picker_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_picker_user |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `origin_document_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `origin_document_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for origin_document |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_quants`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_bin_id` -> `warehouse_bins(id)`
  - `stock_item_id` -> `stock_items(id)`
  - `lot_id` -> `stock_lots(id)`
- **Indexes & Constraints**:
  - `stock_quants_tenant_id_index` (Unique: No)
  - `stock_quants_company_id_index` (Unique: No)
  - `idx_quants_item` (Unique: No)
  - `sqlite_autoindex_stock_quants_2` (Unique: Yes)
  - `sqlite_autoindex_stock_quants_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_bin_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_bin |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lot |
| `quantity_on_hand` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `quantity_reserved` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_reorder_rules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
  - `stock_item_id` -> `stock_items(id)`
- **Indexes & Constraints**:
  - `stock_reorder_rules_tenant_id_index` (Unique: No)
  - `stock_reorder_rules_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_reorder_rules_2` (Unique: Yes)
  - `sqlite_autoindex_stock_reorder_rules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `min_stock_level` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `max_stock_level` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `reorder_point` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `economic_order_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `lead_time_days` | `INTEGER` | No | `7` | Operational entity attribute |
| `preferred_supplier_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for preferred_supplier |
| `auto_trigger_requisition` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_reservations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_item_id` -> `stock_items(id)`
  - `warehouse_id` -> `warehouses(id)`
- **Indexes & Constraints**:
  - `stock_reservations_tenant_id_index` (Unique: No)
  - `stock_reservations_company_id_index` (Unique: No)
  - `idx_reservations_target` (Unique: No)
  - `idx_reservations_alloc` (Unique: No)
  - `sqlite_autoindex_stock_reservations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `reserved_for_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `reserved_for_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for reserved_for |
| `quantity_reserved` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `expires_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_serial_numbers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `stock_item_id` -> `stock_items(id)`
  - `current_warehouse_bin_id` -> `warehouse_bins(id)`
  - `lot_id` -> `stock_lots(id)`
- **Indexes & Constraints**:
  - `stock_serial_numbers_tenant_id_index` (Unique: No)
  - `stock_serial_numbers_company_id_index` (Unique: No)
  - `idx_serial_status` (Unique: No)
  - `sqlite_autoindex_stock_serial_numbers_2` (Unique: Yes)
  - `sqlite_autoindex_stock_serial_numbers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `serial_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `status` | `VARCHAR(255)` | No | `'in_stock'` | State machine status indicator |
| `current_warehouse_bin_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for current_warehouse_bin |
| `lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lot |
| `warranty_start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `warranty_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `customer_asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for customer_asset |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `stock_valuation_snapshots`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
  - `stock_item_id` -> `stock_items(id)`
- **Indexes & Constraints**:
  - `stock_valuation_snapshots_tenant_id_index` (Unique: No)
  - `stock_valuation_snapshots_company_id_index` (Unique: No)
  - `sqlite_autoindex_stock_valuation_snapshots_2` (Unique: Yes)
  - `sqlite_autoindex_stock_valuation_snapshots_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for company |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `stock_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stock_item |
| `snapshot_date` | `DATE` | No | NULL | Operational entity attribute |
| `valuation_method` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity_on_hand` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `total_valuation` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `warehouse_aisles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_zone_id` -> `warehouse_zones(id)`
- **Indexes & Constraints**:
  - `warehouse_aisles_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_warehouse_aisles_2` (Unique: Yes)
  - `sqlite_autoindex_warehouse_aisles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `warehouse_zone_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_zone |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `warehouse_bins`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_rack_id` -> `warehouse_racks(id)`
- **Indexes & Constraints**:
  - `warehouse_bins_tenant_id_index` (Unique: No)
  - `warehouse_bins_barcode_index` (Unique: No)
  - `sqlite_autoindex_warehouse_bins_2` (Unique: Yes)
  - `sqlite_autoindex_warehouse_bins_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `warehouse_rack_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_rack |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `barcode` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `max_weight_kg` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `max_volume_cbm` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `warehouse_racks`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_aisle_id` -> `warehouse_aisles(id)`
- **Indexes & Constraints**:
  - `warehouse_racks_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_warehouse_racks_2` (Unique: Yes)
  - `sqlite_autoindex_warehouse_racks_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `warehouse_aisle_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse_aisle |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `warehouse_zones`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `warehouse_id` -> `warehouses(id)`
- **Indexes & Constraints**:
  - `warehouse_zones_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_warehouse_zones_2` (Unique: Yes)
  - `sqlite_autoindex_warehouse_zones_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `warehouse_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for warehouse |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `zone_type` | `VARCHAR(255)` | No | `'storage'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `warehouses`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `warehouses_company_id_index` (Unique: No)
  - `warehouses_code_index` (Unique: No)
  - `warehouses_assigned_user_id_index` (Unique: No)
  - `sqlite_autoindex_warehouses_2` (Unique: Yes)
  - `sqlite_autoindex_warehouses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_primary` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `warehouse_type` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `assigned_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_user |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |

---

