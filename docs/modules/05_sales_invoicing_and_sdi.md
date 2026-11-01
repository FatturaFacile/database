# Module Reference: Sales, Invoicing & Electronic Invoicing (SDI)

**Module ID**: `05_sales_invoicing_and_sdi`  
**Tables Count**: `20`  
**Description**: Billing lifecycle, quotes, sales orders, invoices, credit notes, delivery notes, and Italian SDI / Swiss QR-Bill integrations.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `delivery_note_items` | Shared Lookup | `id` | `undefined->sales_order_items, undefined->delivery_notes, undefined->tenants` | `delivery_note_items_product_id_index` |
| `delivery_notes` | Shared Lookup | `id` | `undefined->contacts, undefined->tenants, undefined->sales_orders` | `delivery_notes_tenant_id_date_idx, delivery_notes_tenant_id_contact_id_idx` |
| `ei_inbound_logs` | Shared Lookup | `id` | `undefined->tenants, undefined->invoices` | `ei_inbound_logs_sdi_uuid_index, ei_inbound_logs_invoice_id_created_at_index` |
| `ei_outbound_logs` | Shared Lookup | `id` | `undefined->tenants, undefined->invoices` | `ei_outbound_logs_tenant_id_index, ei_outbound_logs_invoice_id_created_at_index` |
| `fee_notes` | Shared Lookup | `id` | `undefined->tenants, undefined->legal_cases, undefined->contacts` | `fee_notes_status_index, fee_notes_note_number_index` |
| `invoice_credit_applications` | Tenant-Scoped | `id` | `undefined->tenants, undefined->invoices, undefined->invoices` | `PRIMARY` |
| `invoice_items` | Shared Lookup | `id` | `undefined->invoices, undefined->tenants` | `invoice_items_product_id_index` |
| `invoice_qr_bill_data` | System / Global | `id` | `undefined->invoices` | `invoice_qr_bill_data_scor_reference_index` |
| `invoice_sdi_metadata` | System / Global | `id` | `undefined->invoices` | `invoice_sdi_metadata_sdi_status_index, invoice_sdi_metadata_sdi_identifier_index` |
| `invoice_service_reports` | Tenant-Scoped | `id` | `undefined->tenants, undefined->invoices, undefined->service_reports...` | `invoice_service_reports_tenant_id_invoice_id_index` |
| `invoices` | Shared Lookup | `id` | `undefined->subscriptions, undefined->invoices, undefined->sales_orders...` | `invoices_tenant_id_payment_status_index, invoices_tenant_id_date_index` |
| `quotes` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `quotes_tenant_id_status_idx, quotes_tenant_id_date_idx` |
| `rt_fiscal_receipts` | System / Global | `id` | `undefined->pos_sales` | `rt_fiscal_receipts_fiscal_document_number_index` |
| `sales_commissions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sales_representatives, undefined->sales_orders...` | `sales_commissions_status_index` |
| `sales_opportunities` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts` | `sales_opportunities_stage_index, sales_opportunities_opportunity_number_index` |
| `sales_order_holds` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sales_orders` | `sales_order_holds_status_index, sales_order_holds_hold_type_index` |
| `sales_order_items` | Shared Lookup | `id` | `undefined->sales_orders, undefined->tenants` | `sales_order_items_product_id_index` |
| `sales_orders` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts, undefined->quotes` | `sales_orders_tenant_id_status_idx, sales_orders_tenant_id_date_idx` |
| `sales_representatives` | Tenant-Scoped | `id` | `undefined->tenants` | `sales_representatives_rep_code_index` |
| `sdi_uuid_links` | Shared Lookup | `id` | `undefined->tenants, undefined->invoices` | `sdi_uuid_links_tenant_id_index, sdi_uuid_links_invoice_id_index` |

---

## Detailed Entity Schema & Data Dictionary

### `delivery_note_items`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `sales_order_item_id` -> `sales_order_items(id)`
  - `delivery_note_id` -> `delivery_notes(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `delivery_note_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_delivery_note_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `delivery_note_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for delivery_note |
| `sales_order_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order_item |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `batch_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `serial_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `warehouse_location_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse_location |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `delivery_notes`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `contact_id` -> `contacts(id)`
  - `tenant_id` -> `tenants(id)`
  - `sales_order_id` -> `sales_orders(id)`
- **Indexes & Constraints**:
  - `delivery_notes_tenant_id_date_idx` (Unique: No)
  - `delivery_notes_tenant_id_contact_id_idx` (Unique: No)
  - `delivery_notes_status_index` (Unique: No)
  - `delivery_notes_shipping_status_index` (Unique: No)
  - `delivery_notes_ddt_number_index` (Unique: No)
  - `sqlite_autoindex_delivery_notes_2` (Unique: Yes)
  - `sqlite_autoindex_delivery_notes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `ddt_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `transport_reason` | `VARCHAR(255)` | No | `'Vendita'` | Operational entity attribute |
| `goods_appearance` | `VARCHAR(255)` | No | `'A vista'` | Operational entity attribute |
| `packages_count` | `INTEGER` | No | `1` | Operational entity attribute |
| `gross_weight_kg` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `carrier_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `carrier_license_plate` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `departure_time` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `sales_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order |
| `shipping_address` | `TEXT` | Yes | NULL | Operational entity attribute |
| `courier` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `show_prices` | `BOOLEAN` | No | `FALSE` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `warehouse_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse |
| `shipping_status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `shipped_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `delivered_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `tracking_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `ei_inbound_logs`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `ei_inbound_logs_sdi_uuid_index` (Unique: No)
  - `ei_inbound_logs_invoice_id_created_at_index` (Unique: No)
  - `sqlite_autoindex_ei_inbound_logs_2` (Unique: Yes)
  - `sqlite_autoindex_ei_inbound_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `provider` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `sdi_uuid` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `fingerprint` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'received'` | State machine status indicator |
| `error` | `TEXT` | Yes | NULL | Operational entity attribute |
| `processed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `ei_outbound_logs`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `ei_outbound_logs_tenant_id_index` (Unique: No)
  - `ei_outbound_logs_invoice_id_created_at_index` (Unique: No)
  - `sqlite_autoindex_ei_outbound_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `provider` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `action` | `VARCHAR(255)` | No | `'send'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | NULL | State machine status indicator |
| `sdi_uuid` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `file_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `response` | `TEXT` | Yes | NULL | Operational entity attribute |
| `error` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `fee_notes`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `legal_case_id` -> `legal_cases(id)`
  - `client_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `fee_notes_status_index` (Unique: No)
  - `fee_notes_note_number_index` (Unique: No)
  - `sqlite_autoindex_fee_notes_2` (Unique: Yes)
  - `sqlite_autoindex_fee_notes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `legal_case_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for legal_case |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `note_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `taxable_fees` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `cassa_previdenza_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `ritenuta_acconto_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `vat_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `net_payable` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `invoice_credit_applications`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `credit_note_id` -> `invoices(id)`
  - `original_invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_invoice_credit_applications_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `credit_note_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for credit_note |
| `original_invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for original_invoice |
| `applied_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `application_date` | `DATE` | No | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `applied_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `invoice_items`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `invoice_id` -> `invoices(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `invoice_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_invoice_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `sales_order_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order_item |
| `delivery_note_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for delivery_note_item |
| `revenue_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for revenue_account |
| `tax_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for tax_account |
| `tax_code_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for tax_code |
| `uom` | `VARCHAR(255)` | No | `'EA'` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `invoice_qr_bill_data`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `invoice_qr_bill_data_scor_reference_index` (Unique: No)
  - `sqlite_autoindex_invoice_qr_bill_data_2` (Unique: Yes)
  - `sqlite_autoindex_invoice_qr_bill_data_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `qr_iban` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `scor_reference` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `creditor_info` | `TEXT` | No | NULL | Operational entity attribute |
| `debtor_info` | `TEXT` | No | NULL | Operational entity attribute |
| `qr_bill_svg` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `invoice_sdi_metadata`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `invoice_sdi_metadata_sdi_status_index` (Unique: No)
  - `invoice_sdi_metadata_sdi_identifier_index` (Unique: No)
  - `sqlite_autoindex_invoice_sdi_metadata_2` (Unique: Yes)
  - `sqlite_autoindex_invoice_sdi_metadata_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `transmission_format` | `VARCHAR(255)` | No | `'FPR12'` | Operational entity attribute |
| `sdi_identifier` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `sdi_status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `file_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `xml_content` | `TEXT` | Yes | NULL | Operational entity attribute |
| `sent_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `delivered_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `invoice_service_reports`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
  - `service_report_id` -> `service_reports(id)`
  - `created_by` -> `users(id)`
- **Indexes & Constraints**:
  - `invoice_service_reports_tenant_id_invoice_id_index` (Unique: No)
  - `sqlite_autoindex_invoice_service_reports_2` (Unique: Yes)
  - `sqlite_autoindex_invoice_service_reports_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `service_report_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for service_report |
| `is_consolidated` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `invoiced_net_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `invoices`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `subscription_id` -> `subscriptions(id)`
  - `related_invoice_id` -> `invoices(id)`
  - `sales_order_id` -> `sales_orders(id)`
  - `proforma_id` -> `invoices(id)`
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
  - `delivery_note_id` -> `delivery_notes(id)`
  - `quote_id` -> `quotes(id)`
- **Indexes & Constraints**:
  - `invoices_tenant_id_payment_status_index` (Unique: No)
  - `invoices_tenant_id_date_index` (Unique: No)
  - `invoices_tenant_id_contact_id_idx` (Unique: No)
  - `invoices_status_index` (Unique: No)
  - `invoices_project_milestone_id_index` (Unique: No)
  - `invoices_project_id_index` (Unique: No)
  - `invoices_payment_status_index` (Unique: No)
  - `invoices_jurisdiction_index` (Unique: No)
  - `invoices_invoice_number_index` (Unique: No)
  - `invoices_gl_journal_entry_id_index` (Unique: No)
  - `sqlite_autoindex_invoices_2` (Unique: Yes)
  - `sqlite_autoindex_invoices_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `invoice_type` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `invoice_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `exchange_rate` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `rounding_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `payment_status` | `VARCHAR(255)` | No | `'unpaid'` | State machine status indicator |
| `jurisdiction` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `split_payment` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `reverse_charge` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `fiscal_year` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `sequential_number` | `INTEGER` | Yes | NULL | Unique business identification code or document number |
| `total_paid` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `proforma_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for proforma |
| `sales_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order |
| `related_invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for related_invoice |
| `payment_method` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `payment_terms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `bank_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `bank_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `vat_payability` | `VARCHAR(255)` | No | `'I'` | Operational entity attribute |
| `withholding_tax_enabled` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `withholding_tax_percent` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `withholding_tax_amount` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `stamp_duty_applied` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `stamp_duty_amount` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `fund_enabled` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `fund_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `fund_percent` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `fund_amount` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `delivery_note_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for delivery_note |
| `subscription_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for subscription |
| `is_deposit` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `quote_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for quote |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `subtotal` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `posted_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `receivable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `customer_agreement_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for customer_agreement |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `project_milestone_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project_milestone |
| `sales_rep_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_rep |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `quotes`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `quotes_tenant_id_status_idx` (Unique: No)
  - `quotes_tenant_id_date_idx` (Unique: No)
  - `quotes_tenant_id_contact_id_idx` (Unique: No)
  - `quotes_status_index` (Unique: No)
  - `quotes_quote_number_index` (Unique: No)
  - `sqlite_autoindex_quotes_2` (Unique: Yes)
  - `sqlite_autoindex_quotes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `quote_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `valid_until` | `DATE` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `custom_text` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signature_data` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `signed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `subtotal` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_policy_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for discount_policy |
| `price_list_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for price_list |
| `payment_terms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `shipping_terms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `revision_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `converted_to_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for converted_to_order |

---

### `rt_fiscal_receipts`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `pos_sale_id` -> `pos_sales(id)`
- **Indexes & Constraints**:
  - `rt_fiscal_receipts_fiscal_document_number_index` (Unique: No)
  - `sqlite_autoindex_rt_fiscal_receipts_2` (Unique: Yes)
  - `sqlite_autoindex_rt_fiscal_receipts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `pos_sale_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for pos_sale |
| `z_report_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `fiscal_document_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `xml_lot_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for xml_lot |
| `rt_status` | `VARCHAR(255)` | No | `'transmitted'` | State machine status indicator |
| `transmitted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sales_commissions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `sales_representative_id` -> `sales_representatives(id)`
  - `sales_order_id` -> `sales_orders(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `sales_commissions_status_index` (Unique: No)
  - `sqlite_autoindex_sales_commissions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `sales_representative_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for sales_representative |
| `sales_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `base_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `commission_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `commission_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'accrued'` | State machine status indicator |
| `paid_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sales_opportunities`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `customer_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `sales_opportunities_stage_index` (Unique: No)
  - `sales_opportunities_opportunity_number_index` (Unique: No)
  - `sqlite_autoindex_sales_opportunities_2` (Unique: Yes)
  - `sqlite_autoindex_sales_opportunities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `opportunity_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `stage` | `VARCHAR(255)` | No | `'lead'` | Operational entity attribute |
| `estimated_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `probability_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `expected_close_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `assigned_to_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_to_user |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sales_order_holds`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `sales_order_id` -> `sales_orders(id)`
- **Indexes & Constraints**:
  - `sales_order_holds_status_index` (Unique: No)
  - `sales_order_holds_hold_type_index` (Unique: No)
  - `sqlite_autoindex_sales_order_holds_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `sales_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for sales_order |
| `hold_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `hold_reason` | `TEXT` | No | NULL | Operational entity attribute |
| `placed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `placed_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `released_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `released_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `release_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sales_order_items`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `sales_order_id` -> `sales_orders(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sales_order_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_sales_order_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `sales_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for sales_order |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `quantity_delivered` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `quantity_reserved` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `quantity_invoiced` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `tax_code_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for tax_code |
| `cost_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `uom` | `VARCHAR(255)` | No | `'EA'` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sales_orders`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
  - `quote_id` -> `quotes(id)`
- **Indexes & Constraints**:
  - `sales_orders_tenant_id_status_idx` (Unique: No)
  - `sales_orders_tenant_id_date_idx` (Unique: No)
  - `sales_orders_tenant_id_contact_id_idx` (Unique: No)
  - `sales_orders_status_index` (Unique: No)
  - `sales_orders_order_number_index` (Unique: No)
  - `sales_orders_inventory_status_index` (Unique: No)
  - `sales_orders_fulfillment_status_index` (Unique: No)
  - `sales_orders_credit_status_index` (Unique: No)
  - `sales_orders_billing_status_index` (Unique: No)
  - `sqlite_autoindex_sales_orders_2` (Unique: Yes)
  - `sqlite_autoindex_sales_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `quote_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for quote |
| `order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `subtotal` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_policy_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for discount_policy |
| `price_list_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for price_list |
| `customer_agreement_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for customer_agreement |
| `sales_rep_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_rep |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `credit_status` | `VARCHAR(255)` | No | `'pending_check'` | State machine status indicator |
| `credit_hold_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `inventory_status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `fulfillment_status` | `VARCHAR(255)` | No | `'unfulfilled'` | State machine status indicator |
| `billing_status` | `VARCHAR(255)` | No | `'unbilled'` | State machine status indicator |
| `payment_terms` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `shipping_method` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `shipping_address` | `TEXT` | Yes | NULL | Operational entity attribute |
| `billing_address` | `TEXT` | Yes | NULL | Operational entity attribute |
| `confirmed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |

---

### `sales_representatives`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sales_representatives_rep_code_index` (Unique: No)
  - `sqlite_autoindex_sales_representatives_2` (Unique: Yes)
  - `sqlite_autoindex_sales_representatives_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `rep_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `territory` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `default_commission_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sdi_uuid_links`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `sdi_uuid_links_tenant_id_index` (Unique: No)
  - `sdi_uuid_links_invoice_id_index` (Unique: No)
  - `sqlite_autoindex_sdi_uuid_links_2` (Unique: Yes)
  - `sqlite_autoindex_sdi_uuid_links_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `provider` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `sdi_uuid` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

