# Module Reference: Procurement, Suppliers & Accounts Payable

**Module ID**: `06_procurement_and_ap`  
**Tables Count**: `24`  
**Description**: Vendor master catalogs, purchase requisitions/orders, passive invoices, three-way matching, and supplier scorecards.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `goods_receipt_items` | System / Global | `id` | `undefined->goods_receipts, undefined->purchase_order_items` | `goods_receipt_items_product_id_index` |
| `goods_receipts` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts, undefined->purchase_orders` | `PRIMARY` |
| `passive_invoices` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `passive_invoices_tenant_id_supplier_id_idx, passive_invoices_tenant_id_is_reconciled_index` |
| `purchase_order_items` | System / Global | `id` | `undefined->purchase_orders` | `purchase_order_items_product_id_index` |
| `purchase_order_lines` | Tenant-Scoped | `id` | `undefined->purchase_orders, undefined->supplier_catalogs` | `purchase_order_lines_tenant_id_index, purchase_order_lines_is_closed_index` |
| `purchase_orders` | Shared Lookup | `id` | `undefined->purchase_requests, undefined->contacts, undefined->tenants...` | `purchase_orders_tenant_id_supplier_id_idx, purchase_orders_tenant_id_status_idx` |
| `purchase_receipt_lines` | Tenant-Scoped | `id` | `undefined->purchase_receipts, undefined->purchase_order_lines` | `purchase_receipt_lines_tenant_id_index` |
| `purchase_receipts` | Tenant-Scoped | `id` | `undefined->purchase_orders, undefined->users` | `purchase_receipts_warehouse_id_index, purchase_receipts_tenant_id_index` |
| `purchase_requests` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `purchase_requests_status_index, purchase_requests_request_number_index` |
| `purchase_requisition_lines` | Tenant-Scoped | `id` | `undefined->purchase_requisitions, undefined->supplier_catalogs, undefined->suppliers` | `purchase_requisition_lines_tenant_id_index` |
| `purchase_requisitions` | Tenant-Scoped | `id` | `undefined->users` | `purchase_requisitions_tenant_id_index, purchase_requisitions_status_index` |
| `purchase_return_lines` | Tenant-Scoped | `id` | `undefined->purchase_returns, undefined->purchase_order_lines` | `purchase_return_lines_tenant_id_index` |
| `purchase_returns` | Tenant-Scoped | `id` | `undefined->purchase_orders, undefined->purchase_receipts, undefined->suppliers...` | `purchase_returns_tenant_id_index, purchase_returns_status_index` |
| `supplier_catalogs` | Tenant-Scoped | `id` | `undefined->suppliers` | `supplier_catalogs_tenant_id_index, supplier_catalogs_internal_sku_index` |
| `supplier_categories` | Tenant-Scoped | `id` | None | `supplier_categories_tenant_id_index, supplier_categories_company_id_index` |
| `supplier_contacts` | Tenant-Scoped | `id` | `undefined->suppliers` | `supplier_contacts_tenant_id_index, supplier_contacts_email_index` |
| `supplier_contracts` | Tenant-Scoped | `id` | `undefined->suppliers` | `supplier_contracts_tenant_id_index, supplier_contracts_status_index` |
| `supplier_evaluations` | Tenant-Scoped | `id` | `undefined->suppliers, undefined->users` | `supplier_evaluations_tenant_id_index, supplier_evaluations_company_id_index` |
| `supplier_ledger` | Tenant-Scoped | `id` | `undefined->journal_entries` | `supplier_ledger_tenant_id_index, supplier_ledger_supplier_id_index` |
| `supplier_payments` | Shared Lookup | `id` | `undefined->tenants, undefined->passive_invoices` | `supplier_payments_tenant_id_index, supplier_payments_passive_invoice_id_paid_at_index` |
| `supplier_price_lists` | Tenant-Scoped | `id` | `undefined->supplier_catalogs` | `supplier_price_lists_tenant_id_index, idx_supp_price_validity` |
| `supplier_scorecards` | Tenant-Scoped | `id` | `undefined->suppliers` | `supplier_scorecards_tenant_id_index, supplier_scorecards_company_id_index` |
| `suppliers` | Tenant-Scoped | `id` | `undefined->contacts, undefined->supplier_categories` | `suppliers_vat_number_index, suppliers_tenant_id_index` |
| `three_way_match_logs` | Tenant-Scoped | `id` | `undefined->purchase_orders, undefined->purchase_receipts` | `three_way_match_logs_tenant_id_index, three_way_match_logs_passive_invoice_id_index` |

---

## Detailed Entity Schema & Data Dictionary

### `goods_receipt_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `goods_receipt_id` -> `goods_receipts(id)`
  - `purchase_order_item_id` -> `purchase_order_items(id)`
- **Indexes & Constraints**:
  - `goods_receipt_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_goods_receipt_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `goods_receipt_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for goods_receipt |
| `purchase_order_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_order_item |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `goods_receipts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `supplier_id` -> `contacts(id)`
  - `purchase_order_id` -> `purchase_orders(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_goods_receipts_2` (Unique: Yes)
  - `sqlite_autoindex_goods_receipts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `purchase_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_order |
| `receipt_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `passive_invoices`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `supplier_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `passive_invoices_tenant_id_supplier_id_idx` (Unique: No)
  - `passive_invoices_tenant_id_is_reconciled_index` (Unique: No)
  - `passive_invoices_tenant_id_is_reconciled_idx` (Unique: No)
  - `passive_invoices_tenant_id_date_index` (Unique: No)
  - `passive_invoices_tenant_id_date_idx` (Unique: No)
  - `passive_invoices_sdi_lot_id_index` (Unique: No)
  - `passive_invoices_is_reconciled_index` (Unique: No)
  - `passive_invoices_invoice_number_index` (Unique: No)
  - `sqlite_autoindex_passive_invoices_2` (Unique: Yes)
  - `sqlite_autoindex_passive_invoices_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `invoice_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `sdi_lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sdi_lot |
| `is_reconciled` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `xml_payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `qr_raw_payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `document_type` | `VARCHAR(255)` | No | `'TD01'` | Operational entity attribute |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `payment_status` | `VARCHAR(255)` | No | `'unpaid'` | State machine status indicator |
| `document_hash` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `sdi_file_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `total_paid` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |

---

### `purchase_order_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `purchase_order_id` -> `purchase_orders(id)`
- **Indexes & Constraints**:
  - `purchase_order_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_order_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `purchase_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `quantity_received` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |

---

### `purchase_order_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_order_id` -> `purchase_orders(id)`
  - `supplier_catalog_id` -> `supplier_catalogs(id)`
- **Indexes & Constraints**:
  - `purchase_order_lines_tenant_id_index` (Unique: No)
  - `purchase_order_lines_is_closed_index` (Unique: No)
  - `idx_pol_po_closed` (Unique: No)
  - `sqlite_autoindex_purchase_order_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `purchase_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order |
| `line_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `supplier_catalog_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier_catalog |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity_ordered` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `quantity_received` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `quantity_invoiced` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `quantity_cancelled` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `22` | Monetary or financial decimal quantity |
| `line_net_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `line_tax_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `line_total_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `is_closed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_orders`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `purchase_request_id` -> `purchase_requests(id)`
  - `supplier_id` -> `contacts(id)`
  - `tenant_id` -> `tenants(id)`
  - `supplier_contract_id` -> `supplier_contracts(id)`
  - `purchase_requisition_id` -> `purchase_requisitions(id)`
- **Indexes & Constraints**:
  - `purchase_orders_tenant_id_supplier_id_idx` (Unique: No)
  - `purchase_orders_tenant_id_status_idx` (Unique: No)
  - `purchase_orders_tenant_id_date_idx` (Unique: No)
  - `purchase_orders_status_index` (Unique: No)
  - `purchase_orders_project_id_index` (Unique: No)
  - `purchase_orders_po_number_index` (Unique: No)
  - `purchase_orders_order_number_index` (Unique: No)
  - `purchase_orders_is_budget_encumbered_index` (Unique: No)
  - `purchase_orders_department_id_index` (Unique: No)
  - `purchase_orders_cost_center_id_index` (Unique: No)
  - `purchase_orders_company_id_index` (Unique: No)
  - `purchase_orders_branch_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_orders_2` (Unique: Yes)
  - `sqlite_autoindex_purchase_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `purchase_request_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_request |
| `order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `delivery_due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `branch_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for branch |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `supplier_contract_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier_contract |
| `purchase_requisition_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_requisition |
| `po_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `order_type` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `expected_delivery_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `exchange_rate` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `net_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `budget_committed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `payment_terms_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `incoterms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `shipping_address` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `is_budget_encumbered` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `purchase_receipt_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_receipt_id` -> `purchase_receipts(id)`
  - `purchase_order_line_id` -> `purchase_order_lines(id)`
- **Indexes & Constraints**:
  - `purchase_receipt_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_receipt_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `purchase_receipt_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_receipt |
| `purchase_order_line_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order_line |
| `quantity_received` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `quantity_accepted` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `quantity_rejected` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `lot_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `serial_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `warehouse_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse_location |
| `rejection_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_receipts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_order_id` -> `purchase_orders(id)`
  - `received_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `purchase_receipts_warehouse_id_index` (Unique: No)
  - `purchase_receipts_tenant_id_index` (Unique: No)
  - `purchase_receipts_company_id_index` (Unique: No)
  - `idx_prc_tenant_po` (Unique: No)
  - `sqlite_autoindex_purchase_receipts_2` (Unique: Yes)
  - `sqlite_autoindex_purchase_receipts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `purchase_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order |
| `receipt_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `supplier_delivery_note_ref` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `received_date` | `DATE` | No | NULL | Operational entity attribute |
| `received_by_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for received_by_user |
| `warehouse_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse |
| `inspection_status` | `VARCHAR(255)` | No | `'passed'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_requests`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `purchase_requests_status_index` (Unique: No)
  - `purchase_requests_request_number_index` (Unique: No)
  - `sqlite_autoindex_purchase_requests_2` (Unique: Yes)
  - `sqlite_autoindex_purchase_requests_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `request_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `department` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `total_estimated` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `requested_date` | `DATE` | No | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_requisition_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_requisition_id` -> `purchase_requisitions(id)`
  - `supplier_catalog_id` -> `supplier_catalogs(id)`
  - `suggested_supplier_id` -> `suppliers(id)`
- **Indexes & Constraints**:
  - `purchase_requisition_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_requisition_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `purchase_requisition_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_requisition |
| `line_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `supplier_catalog_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier_catalog |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity_requested` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `estimated_unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `estimated_total_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `suggested_supplier_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for suggested_supplier |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_requisitions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `requestor_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `purchase_requisitions_tenant_id_index` (Unique: No)
  - `purchase_requisitions_status_index` (Unique: No)
  - `purchase_requisitions_project_id_index` (Unique: No)
  - `purchase_requisitions_department_id_index` (Unique: No)
  - `purchase_requisitions_cost_center_id_index` (Unique: No)
  - `purchase_requisitions_company_id_index` (Unique: No)
  - `purchase_requisitions_branch_id_index` (Unique: No)
  - `idx_pr_tenant_status` (Unique: No)
  - `sqlite_autoindex_purchase_requisitions_2` (Unique: Yes)
  - `sqlite_autoindex_purchase_requisitions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `branch_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for branch |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `requisition_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `requestor_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for requestor_user |
| `urgency` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `required_by_date` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `total_estimated_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_return_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_return_id` -> `purchase_returns(id)`
  - `purchase_order_line_id` -> `purchase_order_lines(id)`
- **Indexes & Constraints**:
  - `purchase_return_lines_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_return_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `purchase_return_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_return |
| `purchase_order_line_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order_line |
| `quantity_returned` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `line_total` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `purchase_returns`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_order_id` -> `purchase_orders(id)`
  - `purchase_receipt_id` -> `purchase_receipts(id)`
  - `supplier_id` -> `suppliers(id)`
  - `returned_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `purchase_returns_tenant_id_index` (Unique: No)
  - `purchase_returns_status_index` (Unique: No)
  - `purchase_returns_company_id_index` (Unique: No)
  - `sqlite_autoindex_purchase_returns_2` (Unique: Yes)
  - `sqlite_autoindex_purchase_returns_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `purchase_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order |
| `purchase_receipt_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for purchase_receipt |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `return_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `return_date` | `DATE` | No | NULL | Operational entity attribute |
| `returned_by_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for returned_by_user |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_catalogs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_id` -> `suppliers(id)`
- **Indexes & Constraints**:
  - `supplier_catalogs_tenant_id_index` (Unique: No)
  - `supplier_catalogs_internal_sku_index` (Unique: No)
  - `supplier_catalogs_company_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_catalogs_2` (Unique: Yes)
  - `sqlite_autoindex_supplier_catalogs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `supplier_part_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `internal_sku` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'PCE'` | Operational entity attribute |
| `lead_time_days` | `INTEGER` | No | `7` | Operational entity attribute |
| `minimum_order_quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_categories`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `supplier_categories_tenant_id_index` (Unique: No)
  - `supplier_categories_company_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_categories_2` (Unique: Yes)
  - `sqlite_autoindex_supplier_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_contacts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_id` -> `suppliers(id)`
- **Indexes & Constraints**:
  - `supplier_contacts_tenant_id_index` (Unique: No)
  - `supplier_contacts_email_index` (Unique: No)
  - `sqlite_autoindex_supplier_contacts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `role` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_primary` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_contracts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_id` -> `suppliers(id)`
- **Indexes & Constraints**:
  - `supplier_contracts_tenant_id_index` (Unique: No)
  - `supplier_contracts_status_index` (Unique: No)
  - `supplier_contracts_company_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_contracts_2` (Unique: Yes)
  - `sqlite_autoindex_supplier_contracts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `contract_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `contract_type` | `VARCHAR(255)` | No | `'framework'` | Operational entity attribute |
| `total_committed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `consumed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `starts_at` | `DATE` | No | NULL | Operational entity attribute |
| `ends_at` | `DATE` | No | NULL | Operational entity attribute |
| `payment_terms_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `incoterms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_evaluations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_id` -> `suppliers(id)`
  - `evaluator_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `supplier_evaluations_tenant_id_index` (Unique: No)
  - `supplier_evaluations_company_id_index` (Unique: No)
  - `idx_se_tenant_supp_rate` (Unique: No)
  - `sqlite_autoindex_supplier_evaluations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `evaluation_period_start` | `DATE` | No | NULL | Operational entity attribute |
| `evaluation_period_end` | `DATE` | No | NULL | Operational entity attribute |
| `on_time_delivery_rate` | `NUMERIC(16, 4)` | No | `100` | Monetary or financial decimal quantity |
| `quality_acceptance_rate` | `NUMERIC(16, 4)` | No | `100` | Monetary or financial decimal quantity |
| `price_competitiveness_score` | `NUMERIC(16, 4)` | No | `100` | Monetary or financial decimal quantity |
| `overall_rating` | `VARCHAR(255)` | No | `'A'` | Operational entity attribute |
| `is_approved_vendor` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `evaluator_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for evaluator_user |
| `comments` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_ledger`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `journal_entry_id` -> `journal_entries(id)`
- **Indexes & Constraints**:
  - `supplier_ledger_tenant_id_index` (Unique: No)
  - `supplier_ledger_supplier_id_index` (Unique: No)
  - `supplier_ledger_journal_entry_id_index` (Unique: No)
  - `supplier_ledger_company_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_ledger_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `journal_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for journal_entry |
| `posting_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | No | NULL | Operational entity attribute |
| `original_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `open_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_payments`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `passive_invoice_id` -> `passive_invoices(id)`
- **Indexes & Constraints**:
  - `supplier_payments_tenant_id_index` (Unique: No)
  - `supplier_payments_passive_invoice_id_paid_at_index` (Unique: No)
  - `supplier_payments_bank_statement_line_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_payments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `passive_invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for passive_invoice |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `paid_at` | `DATE` | No | NULL | Operational entity attribute |
| `type` | `VARCHAR(255)` | No | `'payment'` | Operational entity attribute |
| `reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `bank_statement_line_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_statement_line |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `supplier_price_lists`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_catalog_id` -> `supplier_catalogs(id)`
- **Indexes & Constraints**:
  - `supplier_price_lists_tenant_id_index` (Unique: No)
  - `idx_supp_price_validity` (Unique: No)
  - `sqlite_autoindex_supplier_price_lists_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `supplier_catalog_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier_catalog |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `min_quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `valid_from` | `DATE` | No | NULL | Operational entity attribute |
| `valid_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `supplier_scorecards`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `supplier_id` -> `suppliers(id)`
- **Indexes & Constraints**:
  - `supplier_scorecards_tenant_id_index` (Unique: No)
  - `supplier_scorecards_company_id_index` (Unique: No)
  - `sqlite_autoindex_supplier_scorecards_2` (Unique: Yes)
  - `sqlite_autoindex_supplier_scorecards_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `supplier_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for supplier |
| `year` | `INTEGER` | No | NULL | Operational entity attribute |
| `quarter` | `INTEGER` | No | NULL | Operational entity attribute |
| `otif_percentage` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `defect_ppm` | `INTEGER` | No | `0` | Operational entity attribute |
| `cost_savings_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `compliance_score` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `risk_level` | `VARCHAR(255)` | No | `'low'` | Operational entity attribute |
| `is_avl_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `scorecard_data` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `suppliers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `contact_id` -> `contacts(id)`
  - `supplier_category_id` -> `supplier_categories(id)`
- **Indexes & Constraints**:
  - `suppliers_vat_number_index` (Unique: No)
  - `suppliers_tenant_id_index` (Unique: No)
  - `suppliers_status_index` (Unique: No)
  - `suppliers_is_approved_vendor_index` (Unique: No)
  - `suppliers_fiscal_code_index` (Unique: No)
  - `suppliers_company_id_index` (Unique: No)
  - `idx_supp_status_avl` (Unique: No)
  - `sqlite_autoindex_suppliers_2` (Unique: Yes)
  - `sqlite_autoindex_suppliers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `supplier_category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for supplier_category |
| `supplier_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `company_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `vat_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `fiscal_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `payment_terms_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `incoterms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `is_approved_vendor` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `credit_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `rating` | `VARCHAR(255)` | No | `'B'` | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | No | `'{}'` | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `three_way_match_logs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `purchase_order_id` -> `purchase_orders(id)`
  - `purchase_receipt_id` -> `purchase_receipts(id)`
- **Indexes & Constraints**:
  - `three_way_match_logs_tenant_id_index` (Unique: No)
  - `three_way_match_logs_passive_invoice_id_index` (Unique: No)
  - `three_way_match_logs_match_status_index` (Unique: No)
  - `three_way_match_logs_company_id_index` (Unique: No)
  - `idx_twm_tenant_eval` (Unique: No)
  - `sqlite_autoindex_three_way_match_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `purchase_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_order |
| `purchase_receipt_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for purchase_receipt |
| `passive_invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for passive_invoice |
| `match_status` | `VARCHAR(255)` | No | `'matched'` | State machine status indicator |
| `po_total_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `grn_total_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `invoice_total_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `variance_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `variance_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `discrepancy_details` | `TEXT` | No | `'[]'` | Operational entity attribute |
| `evaluated_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

