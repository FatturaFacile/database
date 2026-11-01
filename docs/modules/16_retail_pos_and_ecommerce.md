# Module Reference: Retail POS, Ecommerce & Loyalty

**Module ID**: `16_retail_pos_and_ecommerce`  
**Tables Count**: `8`  
**Description**: Point-of-sale registers, omnichannel sales, ecommerce channel sync, loyalty cards, and fiscal cash registers.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `ecommerce_channels` | Shared Lookup | `id` | `undefined->tenants` | `ecommerce_channels_tenant_id_is_active_index` |
| `ecommerce_mappings` | Shared Lookup | `id` | `undefined->tenants, undefined->ecommerce_channels` | `ecommerce_mappings_channel_id_remote_sku_index, ecommerce_mappings_channel_id_entity_type_local_id_index` |
| `loyalty_cards` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `PRIMARY` |
| `loyalty_transactions` | Shared Lookup | `id` | `undefined->tenants, undefined->loyalty_cards, undefined->invoices` | `loyalty_transactions_tenant_id_index, loyalty_transactions_loyalty_card_id_created_at_index` |
| `pos_sale_items` | System / Global | `id` | `undefined->pos_sales` | `pos_sale_items_product_id_index` |
| `pos_sales` | Shared Lookup | `id` | `undefined->pos_sessions, undefined->tenants, undefined->contacts...` | `pos_sales_tenant_id_index, pos_sales_receipt_number_index` |
| `pos_sessions` | Shared Lookup | `id` | `undefined->tenants, undefined->pos_terminals, undefined->users` | `pos_sessions_tenant_id_index, pos_sessions_status_index` |
| `pos_terminals` | Shared Lookup | `id` | `undefined->tenants` | `pos_terminals_terminal_code_index` |

---

## Detailed Entity Schema & Data Dictionary

### `ecommerce_channels`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `ecommerce_channels_tenant_id_is_active_index` (Unique: No)
  - `sqlite_autoindex_ecommerce_channels_2` (Unique: Yes)
  - `sqlite_autoindex_ecommerce_channels_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `driver` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `api_url` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `credentials` | `TEXT` | No | NULL | Operational entity attribute |
| `webhook_secret` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `sync_stock_enabled` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `sync_orders_enabled` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `last_sync_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `settings` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `last_sync_summary` | `TEXT` | Yes | NULL | Operational entity attribute |

---

### `ecommerce_mappings`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `channel_id` -> `ecommerce_channels(id)`
- **Indexes & Constraints**:
  - `ecommerce_mappings_channel_id_remote_sku_index` (Unique: No)
  - `ecommerce_mappings_channel_id_entity_type_local_id_index` (Unique: No)
  - `sqlite_autoindex_ecommerce_mappings_2` (Unique: Yes)
  - `sqlite_autoindex_ecommerce_mappings_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `channel_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for channel |
| `entity_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `local_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for local |
| `remote_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for remote |
| `remote_sku` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `extra_data` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `loyalty_cards`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_loyalty_cards_2` (Unique: Yes)
  - `sqlite_autoindex_loyalty_cards_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `card_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `type` | `VARCHAR(255)` | No | `'loyalty'` | Operational entity attribute |
| `balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `expires_at` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `loyalty_transactions`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `loyalty_card_id` -> `loyalty_cards(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `loyalty_transactions_tenant_id_index` (Unique: No)
  - `loyalty_transactions_loyalty_card_id_created_at_index` (Unique: No)
  - `sqlite_autoindex_loyalty_transactions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `loyalty_card_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for loyalty_card |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `balance_after` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `description` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `pos_sale_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `pos_sale_id` -> `pos_sales(id)`
- **Indexes & Constraints**:
  - `pos_sale_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_pos_sale_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `pos_sale_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for pos_sale |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `line_total` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `pos_sales`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `pos_session_id` -> `pos_sessions(id)`
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
  - `loyalty_card_id` -> `loyalty_cards(id)`
- **Indexes & Constraints**:
  - `pos_sales_tenant_id_index` (Unique: No)
  - `pos_sales_receipt_number_index` (Unique: No)
  - `sqlite_autoindex_pos_sales_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `pos_session_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for pos_session |
| `receipt_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `total_net` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `payment_method` | `VARCHAR(255)` | No | `'cash'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `loyalty_card_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for loyalty_card |
| `cash_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `card_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'completed'` | State machine status indicator |
| `refunded_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |

---

### `pos_sessions`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `pos_terminal_id` -> `pos_terminals(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `pos_sessions_tenant_id_index` (Unique: No)
  - `pos_sessions_status_index` (Unique: No)
  - `sqlite_autoindex_pos_sessions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `pos_terminal_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for pos_terminal |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `opened_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `closed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `opening_float` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `closing_cash` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `total_sales` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `expected_cash` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `cash_difference` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |

---

### `pos_terminals`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `pos_terminals_terminal_code_index` (Unique: No)
  - `sqlite_autoindex_pos_terminals_2` (Unique: Yes)
  - `sqlite_autoindex_pos_terminals_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `terminal_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `hardware_serial` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `rt_serial_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

