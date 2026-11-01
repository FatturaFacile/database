# Module Reference: Master Reference Data & Specialized Verticals

**Module ID**: `17_master_data_and_verticals`  
**Tables Count**: `41`  
**Description**: Geographic registers, business calendars, fleet/vehicle rentals, automotive tire management, expenses, and legal tracking.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `alerts` | Shared Lookup | `id` | `undefined->tenants` | `alerts_tenant_id_is_active_index, alerts_created_by_index` |
| `attachments` | Shared Lookup | `id` | `undefined->tenants` | `attachments_uploaded_by_index, attachments_tenant_id_index` |
| `business_calendar_holidays` | Tenant-Scoped | `id` | `undefined->business_calendars` | `business_calendar_holidays_tenant_id_index` |
| `business_calendars` | Tenant-Scoped | `id` | None | `idx_biz_cal_lookup, business_calendars_tenant_id_index` |
| `carbon_ledger` | Tenant-Scoped | `id` | None | `carbon_ledger_tenant_id_index, carbon_ledger_journal_entry_id_index` |
| `conformity_certificates` | Shared Lookup | `id` | `undefined->tenants, undefined->construction_sites` | `conformity_certificates_type_index, conformity_certificates_tenant_id_index` |
| `countries` | Shared Lookup | `id` | None | `countries_tenant_id_index` |
| `country_translations` | Shared Lookup | `id` | `undefined->countries` | `country_translations_tenant_id_index, country_translations_locale_index` |
| `currency_translations` | Shared Lookup | `id` | `undefined->currencies` | `currency_translations_tenant_id_index, currency_translations_locale_index` |
| `customs_declarations` | Shared Lookup | `id` | `undefined->tenants, undefined->delivery_notes` | `customs_declarations_mrn_number_index, customs_declarations_declaration_number_index` |
| `damage_inspections` | Shared Lookup | `id` | `undefined->tenants, undefined->rental_bookings, undefined->users` | `damage_inspections_type_index, damage_inspections_tenant_id_index` |
| `discount_policies` | Tenant-Scoped | `id` | `undefined->tenants` | `discount_policies_code_index` |
| `discount_policy_rules` | System / Global | `id` | `undefined->discount_policies, undefined->products, undefined->customer_groups` | `PRIMARY` |
| `document_emails` | Shared Lookup | `id` | `undefined->tenants` | `document_emails_user_id_index, document_emails_tenant_id_index` |
| `document_events` | Shared Lookup | `id` | `undefined->tenants` | `document_events_user_id_index, document_events_tenant_id_index` |
| `document_sequences` | Shared Lookup | `id` | `undefined->tenants` | `PRIMARY` |
| `document_status_translations` | Shared Lookup | `id` | `undefined->document_statuses` | `document_status_translations_tenant_id_index, document_status_translations_locale_index` |
| `document_statuses` | Shared Lookup | `id` | None | `document_statuses_tenant_id_index, document_statuses_scope_index` |
| `expense_attachments` | Tenant-Scoped | `id` | `undefined->tenants, undefined->expenses, undefined->attachments...` | `expense_attachments_tenant_id_expense_id_index` |
| `expense_categories` | Shared Lookup | `id` | None | `expense_categories_tenant_id_index` |
| `expense_category_translations` | Shared Lookup | `id` | `undefined->expense_categories` | `expense_category_translations_tenant_id_index, expense_category_translations_locale_index` |
| `expense_items` | System / Global | `id` | `undefined->expense_reports` | `expense_items_category_index` |
| `expense_reports` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `expense_reports_tenant_id_user_id_status_index, expense_reports_status_index` |
| `expenses` | Tenant-Scoped | `id` | `undefined->tenants, undefined->lookup_items, undefined->contacts...` | `expenses_tenant_id_user_id_index, expenses_tenant_id_ticket_id_index` |
| `forecast_scenarios` | Tenant-Scoped | `id` | None | `forecast_scenarios_tenant_id_index, forecast_scenarios_company_id_index` |
| `legal_cases` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `legal_cases_status_index, legal_cases_case_number_index` |
| `lookup_categories` | System / Global | `id` | None | `PRIMARY` |
| `lookup_item_translations` | Shared Lookup | `id` | `undefined->tenants, undefined->lookup_items` | `lookup_item_translations_tenant_id_index` |
| `lookup_items` | Shared Lookup | `id` | `undefined->tenants, undefined->lookup_categories` | `lookup_items_tenant_id_index` |
| `notification_type_translations` | Shared Lookup | `id` | `undefined->notification_types` | `notification_type_translations_tenant_id_index, notification_type_translations_locale_index` |
| `notification_types` | Shared Lookup | `id` | None | `notification_types_tenant_id_index` |
| `quote_items` | Shared Lookup | `id` | `undefined->quotes, undefined->tenants` | `quote_items_product_id_index` |
| `region_translations` | Shared Lookup | `id` | `undefined->regions` | `region_translations_tenant_id_index, region_translations_locale_index` |
| `regions` | Shared Lookup | `id` | `undefined->countries` | `regions_tenant_id_index` |
| `rental_bookings` | Shared Lookup | `id` | `undefined->tenants, undefined->rental_vehicles, undefined->contacts` | `rental_bookings_tenant_id_index, rental_bookings_status_index` |
| `rental_contracts` | Shared Lookup | `id` | `undefined->tenants, undefined->rental_bookings` | `rental_contracts_contract_number_index` |
| `rental_vehicles` | Shared Lookup | `id` | `undefined->tenants, undefined->vehicles` | `rental_vehicles_tenant_id_index, rental_vehicles_is_available_index` |
| `tire_hotel_records` | Shared Lookup | `id` | `undefined->tenants, undefined->vehicles` | `tire_hotel_records_tenant_id_vehicle_id_status_index, tire_hotel_records_status_index` |
| `units_of_measure` | Shared Lookup | `id` | `undefined->tenants` | `PRIMARY` |
| `vehicle_inspections` | Shared Lookup | `id` | `undefined->tenants, undefined->vehicles` | `vehicle_inspections_type_index, vehicle_inspections_tenant_id_index` |
| `vehicles` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `vehicles_vin_chassis_index, vehicles_license_plate_index` |

---

## Detailed Entity Schema & Data Dictionary

### `alerts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `alerts_tenant_id_is_active_index` (Unique: No)
  - `alerts_created_by_index` (Unique: No)
  - `alerts_alertable_type_alertable_id_index` (Unique: No)
  - `sqlite_autoindex_alerts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `alertable_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `alertable_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for alertable |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `severity` | `VARCHAR(255)` | No | `'info'` | Operational entity attribute |
| `starts_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `ends_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `attachments`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `attachments_uploaded_by_index` (Unique: No)
  - `attachments_tenant_id_index` (Unique: No)
  - `attachments_tenant_attachable_idx` (Unique: No)
  - `attachments_attachable_type_attachable_id_index` (Unique: No)
  - `sqlite_autoindex_attachments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `attachable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `attachable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for attachable |
| `uploaded_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `original_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `path` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `mime_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `size` | `INTEGER` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `disk` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `business_calendar_holidays`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `business_calendar_id` -> `business_calendars(id)`
- **Indexes & Constraints**:
  - `business_calendar_holidays_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_business_calendar_holidays_2` (Unique: Yes)
  - `sqlite_autoindex_business_calendar_holidays_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `business_calendar_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for business_calendar |
| `holiday_date` | `DATE` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `business_calendars`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `idx_biz_cal_lookup` (Unique: No)
  - `business_calendars_tenant_id_index` (Unique: No)
  - `business_calendars_company_id_index` (Unique: No)
  - `sqlite_autoindex_business_calendars_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `timezone` | `VARCHAR(255)` | No | `'Europe/Rome'` | Operational entity attribute |
| `work_monday` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `work_tuesday` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `work_wednesday` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `work_thursday` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `work_friday` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `work_saturday` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `work_sunday` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `work_hours_start` | `TIME` | No | `'08:30:00'` | Operational entity attribute |
| `work_hours_end` | `TIME` | No | `'17:30:00'` | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `carbon_ledger`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `carbon_ledger_tenant_id_index` (Unique: No)
  - `carbon_ledger_journal_entry_id_index` (Unique: No)
  - `carbon_ledger_company_id_index` (Unique: No)
  - `sqlite_autoindex_carbon_ledger_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `scope` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `emission_category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `activity_data_metric` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `activity_uom` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `emission_factor` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `total_co2e_kg` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `source_module` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `posting_date` | `DATE` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `conformity_certificates`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `construction_site_id` -> `construction_sites(id)`
- **Indexes & Constraints**:
  - `conformity_certificates_type_index` (Unique: No)
  - `conformity_certificates_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_conformity_certificates_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `construction_site_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for construction_site |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `certificate_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `inspector_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `certified_at` | `DATE` | No | NULL | Operational entity attribute |
| `document_path` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `countries`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `countries_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_countries_4` (Unique: Yes)
  - `sqlite_autoindex_countries_3` (Unique: Yes)
  - `sqlite_autoindex_countries_2` (Unique: Yes)
  - `sqlite_autoindex_countries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `iso_code_2` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `iso_code_3` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `numeric_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `phone_prefix` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_eu_member` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_sepa_member` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `currency_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `country_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `country_id` -> `countries(id)`
- **Indexes & Constraints**:
  - `country_translations_tenant_id_index` (Unique: No)
  - `country_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_country_translations_2` (Unique: Yes)
  - `sqlite_autoindex_country_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `country_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for country |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `nationality` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `currency_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `currency_id` -> `currencies(id)`
- **Indexes & Constraints**:
  - `currency_translations_tenant_id_index` (Unique: No)
  - `currency_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_currency_translations_2` (Unique: Yes)
  - `sqlite_autoindex_currency_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `currency_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for currency |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `subunit_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `customs_declarations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ddt_id` -> `delivery_notes(id)`
- **Indexes & Constraints**:
  - `customs_declarations_mrn_number_index` (Unique: No)
  - `customs_declarations_declaration_number_index` (Unique: No)
  - `sqlite_autoindex_customs_declarations_2` (Unique: Yes)
  - `sqlite_autoindex_customs_declarations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `ddt_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ddt |
| `declaration_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `mrn_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `type` | `VARCHAR(255)` | No | `'export_it_to_ch'` | Operational entity attribute |
| `customs_office` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `customs_agent` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `declared_value` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `incoterms` | `VARCHAR(255)` | No | `'DAP'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `damage_inspections`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `rental_booking_id` -> `rental_bookings(id)`
  - `inspected_by_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `damage_inspections_type_index` (Unique: No)
  - `damage_inspections_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_damage_inspections_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `rental_booking_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for rental_booking |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `mileage` | `INTEGER` | No | NULL | Operational entity attribute |
| `fuel_level` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `damage_markers` | `TEXT` | Yes | NULL | Operational entity attribute |
| `photos` | `TEXT` | Yes | NULL | Operational entity attribute |
| `inspected_by_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for inspected_by_user |
| `inspected_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `discount_policies`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `discount_policies_code_index` (Unique: No)
  - `sqlite_autoindex_discount_policies_2` (Unique: Yes)
  - `sqlite_autoindex_discount_policies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `discount_type` | `VARCHAR(255)` | No | `'percentage'` | Operational entity attribute |
| `value` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `min_order_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `min_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `valid_from` | `DATE` | Yes | NULL | Operational entity attribute |
| `valid_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `discount_policy_rules`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `discount_policy_id` -> `discount_policies(id)`
  - `product_id` -> `products(id)`
  - `customer_group_id` -> `customer_groups(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_discount_policy_rules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `discount_policy_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for discount_policy |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `customer_group_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for customer_group |
| `min_threshold` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `discount_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `discount_fixed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `document_emails`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `document_emails_user_id_index` (Unique: No)
  - `document_emails_tenant_id_index` (Unique: No)
  - `document_emails_emailable_type_emailable_id_index` (Unique: No)
  - `sqlite_autoindex_document_emails_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `emailable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `emailable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for emailable |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `recipient` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `subject` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'queued'` | State machine status indicator |
| `error` | `TEXT` | Yes | NULL | Operational entity attribute |
| `sent_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `attachment_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `document_events`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `document_events_user_id_index` (Unique: No)
  - `document_events_tenant_id_index` (Unique: No)
  - `document_events_eventable_type_eventable_id_index` (Unique: No)
  - `document_events_event_index` (Unique: No)
  - `sqlite_autoindex_document_events_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `eventable_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `eventable_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for eventable |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `event` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `payload` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `document_sequences`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_document_sequences_2` (Unique: Yes)
  - `sqlite_autoindex_document_sequences_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `document_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `fiscal_year` | `INTEGER` | No | NULL | Operational entity attribute |
| `prefix` | `VARCHAR(255)` | No | `''` | Operational entity attribute |
| `last_number` | `INTEGER` | No | `0` | Unique business identification code or document number |
| `padding` | `INTEGER` | No | `4` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `document_status_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `document_status_id` -> `document_statuses(id)`
- **Indexes & Constraints**:
  - `document_status_translations_tenant_id_index` (Unique: No)
  - `document_status_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_document_status_translations_2` (Unique: Yes)
  - `sqlite_autoindex_document_status_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `document_status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for document_status |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `label` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `document_statuses`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `document_statuses_tenant_id_index` (Unique: No)
  - `document_statuses_scope_index` (Unique: No)
  - `sqlite_autoindex_document_statuses_2` (Unique: Yes)
  - `sqlite_autoindex_document_statuses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `scope` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `color_badge` | `VARCHAR(255)` | No | `'#64748B'` | Operational entity attribute |
| `sort_order` | `INTEGER` | No | `0` | Operational entity attribute |
| `is_terminal` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `expense_attachments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `expense_id` -> `expenses(id)`
  - `attachment_id` -> `attachments(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `expense_attachments_tenant_id_expense_id_index` (Unique: No)
  - `sqlite_autoindex_expense_attachments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `expense_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for expense |
| `attachment_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for attachment |
| `disk` | `VARCHAR(255)` | No | `'local'` | Operational entity attribute |
| `path` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `original_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `mime_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `size` | `INTEGER` | No | NULL | Operational entity attribute |
| `is_receipt` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `ocr_raw_text` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `expense_categories`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `expense_categories_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_expense_categories_2` (Unique: Yes)
  - `sqlite_autoindex_expense_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `requires_receipt` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `suggested_account_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `expense_category_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `expense_category_id` -> `expense_categories(id)`
- **Indexes & Constraints**:
  - `expense_category_translations_tenant_id_index` (Unique: No)
  - `expense_category_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_expense_category_translations_2` (Unique: Yes)
  - `sqlite_autoindex_expense_category_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `expense_category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for expense_category |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `expense_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `expense_report_id` -> `expense_reports(id)`
- **Indexes & Constraints**:
  - `expense_items_category_index` (Unique: No)
  - `sqlite_autoindex_expense_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `expense_report_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for expense_report |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `receipt_path` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_mileage` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `kilometers` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `vat_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `expense_reports`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `expense_reports_tenant_id_user_id_status_index` (Unique: No)
  - `expense_reports_status_index` (Unique: No)
  - `sqlite_autoindex_expense_reports_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `expenses`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `category_id` -> `lookup_items(id)`
  - `contact_id` -> `contacts(id)`
  - `user_id` -> `users(id)`
  - `ticket_id` -> `tickets(id)`
  - `service_report_id` -> `service_reports(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `expenses_tenant_id_user_id_index` (Unique: No)
  - `expenses_tenant_id_ticket_id_index` (Unique: No)
  - `expenses_tenant_id_status_index` (Unique: No)
  - `expenses_tenant_id_service_report_id_index` (Unique: No)
  - `expenses_tenant_id_project_id_index` (Unique: No)
  - `expenses_tenant_id_date_index` (Unique: No)
  - `expenses_tenant_id_contact_id_index` (Unique: No)
  - `expenses_tenant_id_category_id_index` (Unique: No)
  - `expenses_tenant_id_accounting_exported_at_index` (Unique: No)
  - `expenses_status_index` (Unique: No)
  - `expenses_project_id_index` (Unique: No)
  - `expenses_payment_method_index` (Unique: No)
  - `expenses_merchant_name_index` (Unique: No)
  - `expenses_expense_number_index` (Unique: No)
  - `expenses_date_index` (Unique: No)
  - `expenses_accounting_exported_at_index` (Unique: No)
  - `sqlite_autoindex_expenses_2` (Unique: Yes)
  - `sqlite_autoindex_expenses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `expense_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for category |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `amount_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `amount_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `merchant_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `payment_method` | `VARCHAR(255)` | No | `'cash'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'submitted'` | State machine status indicator |
| `is_billable` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_reimbursable` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `accounting_exported_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `service_report_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for service_report |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `forecast_scenarios`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `forecast_scenarios_tenant_id_index` (Unique: No)
  - `forecast_scenarios_company_id_index` (Unique: No)
  - `forecast_scenarios_code_index` (Unique: No)
  - `sqlite_autoindex_forecast_scenarios_2` (Unique: Yes)
  - `sqlite_autoindex_forecast_scenarios_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_baseline` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `collection_delay_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `disbursement_acceleration_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `sales_growth_factor` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `legal_cases`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `client_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `legal_cases_status_index` (Unique: No)
  - `legal_cases_case_number_index` (Unique: No)
  - `legal_cases_aml_kyc_completed_index` (Unique: No)
  - `sqlite_autoindex_legal_cases_2` (Unique: Yes)
  - `sqlite_autoindex_legal_cases_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `case_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `aml_kyc_completed` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `jurisdiction` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `lookup_categories`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `sqlite_autoindex_lookup_categories_2` (Unique: Yes)
  - `sqlite_autoindex_lookup_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_system` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `lookup_item_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `lookup_item_id` -> `lookup_items(id)`
- **Indexes & Constraints**:
  - `lookup_item_translations_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_lookup_item_translations_2` (Unique: Yes)
  - `sqlite_autoindex_lookup_item_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `lookup_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for lookup_item |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `label` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `short_label` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `lookup_items`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `category_id` -> `lookup_categories(id)`
- **Indexes & Constraints**:
  - `lookup_items_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_lookup_items_2` (Unique: Yes)
  - `sqlite_autoindex_lookup_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for category |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `sort_order` | `INTEGER` | No | `0` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_system` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `notification_type_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `notification_type_id` -> `notification_types(id)`
- **Indexes & Constraints**:
  - `notification_type_translations_tenant_id_index` (Unique: No)
  - `notification_type_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_notification_type_translations_2` (Unique: Yes)
  - `sqlite_autoindex_notification_type_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `notification_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for notification_type |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `notification_types`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `notification_types_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_notification_types_2` (Unique: Yes)
  - `sqlite_autoindex_notification_types_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `channel` | `VARCHAR(255)` | No | `'in_app'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `quote_items`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `quote_id` -> `quotes(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `quote_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_quote_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `quote_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for quote |
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
| `tax_code_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for tax_code |
| `cost_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `margin_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `uom` | `VARCHAR(255)` | No | `'EA'` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `region_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `region_id` -> `regions(id)`
- **Indexes & Constraints**:
  - `region_translations_tenant_id_index` (Unique: No)
  - `region_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_region_translations_2` (Unique: Yes)
  - `sqlite_autoindex_region_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `region_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for region |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `regions`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `country_id` -> `countries(id)`
- **Indexes & Constraints**:
  - `regions_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_regions_2` (Unique: Yes)
  - `sqlite_autoindex_regions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `country_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for country |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `type` | `VARCHAR(255)` | No | `'province'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `rental_bookings`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `rental_vehicle_id` -> `rental_vehicles(id)`
  - `client_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `rental_bookings_tenant_id_index` (Unique: No)
  - `rental_bookings_status_index` (Unique: No)
  - `sqlite_autoindex_rental_bookings_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `rental_vehicle_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for rental_vehicle |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `start_date` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `end_date` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `pickup_location` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `return_location` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `total_estimated` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `deposit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'reserved'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `rental_contracts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `rental_booking_id` -> `rental_bookings(id)`
- **Indexes & Constraints**:
  - `rental_contracts_contract_number_index` (Unique: No)
  - `sqlite_autoindex_rental_contracts_2` (Unique: Yes)
  - `sqlite_autoindex_rental_contracts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `rental_booking_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for rental_booking |
| `contract_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `agreement_terms` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `is_closed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `rental_vehicles`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `vehicle_id` -> `vehicles(id)`
- **Indexes & Constraints**:
  - `rental_vehicles_tenant_id_index` (Unique: No)
  - `rental_vehicles_is_available_index` (Unique: No)
  - `sqlite_autoindex_rental_vehicles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `vehicle_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for vehicle |
| `category` | `VARCHAR(255)` | No | `'economy'` | Operational entity attribute |
| `daily_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `fuel_type` | `VARCHAR(255)` | No | `'petrol'` | Operational entity attribute |
| `transmission` | `VARCHAR(255)` | No | `'manual'` | Operational entity attribute |
| `is_available` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `current_mileage` | `INTEGER` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `tire_hotel_records`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `vehicle_id` -> `vehicles(id)`
- **Indexes & Constraints**:
  - `tire_hotel_records_tenant_id_vehicle_id_status_index` (Unique: No)
  - `tire_hotel_records_status_index` (Unique: No)
  - `tire_hotel_records_season_index` (Unique: No)
  - `sqlite_autoindex_tire_hotel_records_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `vehicle_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for vehicle |
| `season` | `VARCHAR(255)` | No | `'winter'` | Operational entity attribute |
| `brand` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `model` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `size` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `dot` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `front_left_tread_mm` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `front_right_tread_mm` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `rear_left_tread_mm` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `rear_right_tread_mm` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `warehouse_shelf_location` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'stored'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `units_of_measure`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_units_of_measure_2` (Unique: Yes)
  - `sqlite_autoindex_units_of_measure_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `vehicle_inspections`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `vehicle_id` -> `vehicles(id)`
- **Indexes & Constraints**:
  - `vehicle_inspections_type_index` (Unique: No)
  - `vehicle_inspections_tenant_id_index` (Unique: No)
  - `vehicle_inspections_scheduled_date_index` (Unique: No)
  - `vehicle_inspections_result_index` (Unique: No)
  - `sqlite_autoindex_vehicle_inspections_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `vehicle_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for vehicle |
| `type` | `VARCHAR(255)` | No | `'it_revisione'` | Operational entity attribute |
| `scheduled_date` | `DATE` | No | NULL | Operational entity attribute |
| `passed_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `result` | `VARCHAR(255)` | No | `'pending'` | Operational entity attribute |
| `certificate_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `inspector_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `vehicles`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `client_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `vehicles_vin_chassis_index` (Unique: No)
  - `vehicles_license_plate_index` (Unique: No)
  - `sqlite_autoindex_vehicles_2` (Unique: Yes)
  - `sqlite_autoindex_vehicles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `license_plate` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `vin_chassis` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `make` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `model` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `year` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `registration_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `mileage_km` | `INTEGER` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

