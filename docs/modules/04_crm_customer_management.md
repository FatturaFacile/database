# Module Reference: CRM & Customer Lifecycle Management

**Module ID**: `04_crm_customer_management`  
**Tables Count**: `24`  
**Description**: Customer master directory, pipeline tracking, opportunities, leads, activities, and contact addresses.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `contact_addresses` | System / Global | `id` | `undefined->contacts` | `contact_addresses_contact_id_type_index` |
| `contact_categories` | Shared Lookup | `id` | None | `contact_categories_tenant_id_index` |
| `contact_category_translations` | Shared Lookup | `id` | `undefined->contact_categories` | `contact_category_translations_tenant_id_index, contact_category_translations_locale_index` |
| `contact_type_translations` | Shared Lookup | `id` | `undefined->contact_types` | `contact_type_translations_tenant_id_index, contact_type_translations_locale_index` |
| `contact_types` | Shared Lookup | `id` | None | `contact_types_tenant_id_index` |
| `contacts` | Shared Lookup | `id` | `undefined->payment_terms, undefined->price_lists, undefined->tenants` | `contacts_vat_number_index, contacts_uid_number_index` |
| `crm_accounts` | Tenant-Scoped | `id` | `undefined->contacts, undefined->tenants, undefined->crm_accounts` | `crm_accounts_tenant_id_tier_status_index, crm_accounts_tenant_id_customer_health_index_index` |
| `crm_activities` | Tenant-Scoped | `id` | `undefined->tenants` | `crm_activities_type_index, crm_activities_tenant_id_status_due_date_index` |
| `crm_campaign_members` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_campaigns, undefined->crm_leads...` | `crm_campaign_members_tenant_id_campaign_id_status_index` |
| `crm_campaign_types` | Tenant-Scoped | `id` | `undefined->tenants` | `crm_campaign_types_tenant_id_is_active_index` |
| `crm_campaigns` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_campaign_types` | `crm_campaigns_tenant_id_status_start_date_index, crm_campaigns_status_index` |
| `crm_contact_roles` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_accounts, undefined->contacts` | `crm_contact_roles_tenant_id_contact_id_index, crm_contact_roles_tenant_id_account_id_role_index` |
| `crm_customer_health_profiles` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_accounts` | `idx_91492eb02e15c6e8_crm_customer_health_profiles, crm_customer_health_profiles_health_index_index` |
| `crm_forecasts` | Tenant-Scoped | `id` | `undefined->tenants` | `crm_forecasts_workflow_instance_id_index, crm_forecasts_user_id_index` |
| `crm_lead_sources` | Tenant-Scoped | `id` | `undefined->tenants` | `crm_lead_sources_tenant_id_is_active_index` |
| `crm_leads` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_lead_sources, undefined->crm_campaigns...` | `crm_leads_tenant_id_status_score_index, crm_leads_tenant_id_company_name_email_index` |
| `crm_opportunities` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_accounts, undefined->contacts...` | `crm_opportunities_workflow_instance_id_index, crm_opportunities_tenant_id_stage_id_status_index` |
| `crm_opportunity_line_items` | Tenant-Scoped | `id` | `undefined->tenants, undefined->crm_opportunities` | `crm_opportunity_line_items_tenant_id_opportunity_id_index` |
| `crm_opportunity_stages` | Tenant-Scoped | `id` | `undefined->tenants` | `crm_opportunity_stages_tenant_id_sequence_index` |
| `customer_agreements` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts, undefined->price_lists...` | `customer_agreements_status_index, customer_agreements_agreement_number_index` |
| `customer_credit_profiles` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts` | `customer_credit_profiles_is_credit_hold_index, customer_credit_profiles_credit_status_index` |
| `customer_groups` | Tenant-Scoped | `id` | `undefined->tenants, undefined->price_lists, undefined->payment_terms` | `customer_groups_code_index` |
| `customer_ledger` | Tenant-Scoped | `id` | `undefined->journal_entries` | `customer_ledger_tenant_id_index, customer_ledger_journal_entry_id_index` |
| `customer_ledger_entries` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts, undefined->invoices` | `customer_ledger_entries_tenant_id_status_due_date_index, idx_a47dc036acd95efb_customer_ledger_entries` |

---

## Detailed Entity Schema & Data Dictionary

### `contact_addresses`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `contact_addresses_contact_id_type_index` (Unique: No)
  - `sqlite_autoindex_contact_addresses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `type` | `VARCHAR(255)` | No | `'billing'` | Operational entity attribute |
| `street` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `house_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `postal_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `city` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `state_canton` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `contact_categories`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `contact_categories_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_contact_categories_2` (Unique: Yes)
  - `sqlite_autoindex_contact_categories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `contact_category_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `contact_category_id` -> `contact_categories(id)`
- **Indexes & Constraints**:
  - `contact_category_translations_tenant_id_index` (Unique: No)
  - `contact_category_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_contact_category_translations_2` (Unique: Yes)
  - `sqlite_autoindex_contact_category_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `contact_category_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact_category |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `contact_type_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `contact_type_id` -> `contact_types(id)`
- **Indexes & Constraints**:
  - `contact_type_translations_tenant_id_index` (Unique: No)
  - `contact_type_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_contact_type_translations_2` (Unique: Yes)
  - `sqlite_autoindex_contact_type_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `contact_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact_type |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `contact_types`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `contact_types_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_contact_types_2` (Unique: Yes)
  - `sqlite_autoindex_contact_types_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `contacts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `payment_term_id` -> `payment_terms(id)`
  - `price_list_id` -> `price_lists(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `contacts_vat_number_index` (Unique: No)
  - `contacts_uid_number_index` (Unique: No)
  - `contacts_type_index` (Unique: No)
  - `contacts_tenant_id_vat_number_idx` (Unique: No)
  - `contacts_tenant_id_type_index` (Unique: No)
  - `contacts_tenant_id_fiscal_code_idx` (Unique: No)
  - `contacts_tenant_id_country_index` (Unique: No)
  - `contacts_fiscal_code_index` (Unique: No)
  - `contacts_email_index` (Unique: No)
  - `contacts_country_index` (Unique: No)
  - `sqlite_autoindex_contacts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `type` | `VARCHAR(255)` | No | `'client'` | Operational entity attribute |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `company_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `first_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `last_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `vat_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `fiscal_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `uid_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `sdi_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `pec` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `qr_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `payment_terms_days` | `INTEGER` | No | `30` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `price_list_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for price_list |
| `payment_term_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payment_term |

---

### `crm_accounts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `contact_id` -> `contacts(id)`
  - `tenant_id` -> `tenants(id)`
  - `parent_account_id` -> `crm_accounts(id)`
- **Indexes & Constraints**:
  - `crm_accounts_tenant_id_tier_status_index` (Unique: No)
  - `crm_accounts_tenant_id_customer_health_index_index` (Unique: No)
  - `crm_accounts_status_index` (Unique: No)
  - `crm_accounts_owner_user_id_index` (Unique: No)
  - `crm_accounts_customer_health_index_index` (Unique: No)
  - `crm_accounts_churn_risk_index` (Unique: No)
  - `sqlite_autoindex_crm_accounts_2` (Unique: Yes)
  - `sqlite_autoindex_crm_accounts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `parent_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_account |
| `account_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `industry` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `tier` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `annual_revenue` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `employee_count` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `website` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `owner_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for owner_user |
| `customer_health_index` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `churn_risk` | `VARCHAR(255)` | No | `'low'` | Operational entity attribute |
| `lifecycle_stage` | `VARCHAR(255)` | No | `'prospect'` | Operational entity attribute |
| `last_activity_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `tags` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_activities`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `crm_activities_type_index` (Unique: No)
  - `crm_activities_tenant_id_status_due_date_index` (Unique: No)
  - `crm_activities_tenant_id_related_type_related_id_index` (Unique: No)
  - `crm_activities_status_index` (Unique: No)
  - `crm_activities_related_type_index` (Unique: No)
  - `crm_activities_related_id_index` (Unique: No)
  - `crm_activities_due_date_index` (Unique: No)
  - `crm_activities_created_by_user_id_index` (Unique: No)
  - `crm_activities_assigned_user_id_index` (Unique: No)
  - `sqlite_autoindex_crm_activities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subject` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `due_date` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `assigned_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_user |
| `created_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for created_by_user |
| `related_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `related_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for related |
| `duration_minutes` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `location` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `outcome` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_campaign_members`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `campaign_id` -> `crm_campaigns(id)`
  - `lead_id` -> `crm_leads(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `crm_campaign_members_tenant_id_campaign_id_status_index` (Unique: No)
  - `sqlite_autoindex_crm_campaign_members_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `campaign_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for campaign |
| `lead_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lead |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `status` | `VARCHAR(255)` | No | `'sent'` | State machine status indicator |
| `first_associated_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_campaign_types`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `crm_campaign_types_tenant_id_is_active_index` (Unique: No)
  - `sqlite_autoindex_crm_campaign_types_2` (Unique: Yes)
  - `sqlite_autoindex_crm_campaign_types_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_campaigns`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `campaign_type_id` -> `crm_campaign_types(id)`
- **Indexes & Constraints**:
  - `crm_campaigns_tenant_id_status_start_date_index` (Unique: No)
  - `crm_campaigns_status_index` (Unique: No)
  - `sqlite_autoindex_crm_campaigns_2` (Unique: Yes)
  - `sqlite_autoindex_crm_campaigns_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `campaign_type_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for campaign_type |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'planned'` | State machine status indicator |
| `start_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `budgeted_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `expected_revenue` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `actual_revenue` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `utm_source` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `utm_medium` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `utm_campaign` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_contact_roles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `account_id` -> `crm_accounts(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `crm_contact_roles_tenant_id_contact_id_index` (Unique: No)
  - `crm_contact_roles_tenant_id_account_id_role_index` (Unique: No)
  - `sqlite_autoindex_crm_contact_roles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `role` | `VARCHAR(255)` | No | `'evaluator'` | Operational entity attribute |
| `is_primary` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_customer_health_profiles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `account_id` -> `crm_accounts(id)`
- **Indexes & Constraints**:
  - `idx_91492eb02e15c6e8_crm_customer_health_profiles` (Unique: No)
  - `crm_customer_health_profiles_health_index_index` (Unique: No)
  - `crm_customer_health_profiles_churn_risk_indicator_index` (Unique: No)
  - `sqlite_autoindex_crm_customer_health_profiles_2` (Unique: Yes)
  - `sqlite_autoindex_crm_customer_health_profiles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `activity_score` | `NUMERIC(16, 4)` | No | `50` | Operational entity attribute |
| `engagement_score` | `NUMERIC(16, 4)` | No | `50` | Operational entity attribute |
| `revenue_score` | `NUMERIC(16, 4)` | No | `50` | Operational entity attribute |
| `risk_score` | `NUMERIC(16, 4)` | No | `10` | Operational entity attribute |
| `churn_risk_indicator` | `VARCHAR(255)` | No | `'low'` | Operational entity attribute |
| `health_index` | `NUMERIC(16, 4)` | No | `85` | Operational entity attribute |
| `last_interaction_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `last_invoiced_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `open_receivable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `overdue_receivable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `evaluation_metrics` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_forecasts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `crm_forecasts_workflow_instance_id_index` (Unique: No)
  - `crm_forecasts_user_id_index` (Unique: No)
  - `crm_forecasts_tenant_id_period_status_index` (Unique: No)
  - `crm_forecasts_status_index` (Unique: No)
  - `crm_forecasts_period_index` (Unique: No)
  - `sqlite_autoindex_crm_forecasts_2` (Unique: Yes)
  - `sqlite_autoindex_crm_forecasts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `period` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `pipeline_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `best_case_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `commit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `closed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `weighted_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `quota_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `attainment_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_lead_sources`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `crm_lead_sources_tenant_id_is_active_index` (Unique: No)
  - `sqlite_autoindex_crm_lead_sources_2` (Unique: Yes)
  - `sqlite_autoindex_crm_lead_sources_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_leads`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `lead_source_id` -> `crm_lead_sources(id)`
  - `campaign_id` -> `crm_campaigns(id)`
  - `converted_contact_id` -> `contacts(id)`
  - `converted_account_id` -> `crm_accounts(id)`
- **Indexes & Constraints**:
  - `crm_leads_tenant_id_status_score_index` (Unique: No)
  - `crm_leads_tenant_id_company_name_email_index` (Unique: No)
  - `crm_leads_status_index` (Unique: No)
  - `crm_leads_score_index` (Unique: No)
  - `crm_leads_email_index` (Unique: No)
  - `crm_leads_duplicate_hash_index` (Unique: No)
  - `crm_leads_converted_opportunity_id_index` (Unique: No)
  - `crm_leads_assigned_user_id_index` (Unique: No)
  - `sqlite_autoindex_crm_leads_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `lead_source_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lead_source |
| `campaign_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for campaign |
| `assigned_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_user |
| `first_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `last_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `company_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `title` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `website` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'new'` | State machine status indicator |
| `disqualification_reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `score` | `INTEGER` | No | `0` | Operational entity attribute |
| `rating` | `VARCHAR(255)` | No | `'cold'` | Operational entity attribute |
| `estimated_budget` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `converted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `converted_contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for converted_contact |
| `converted_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for converted_account |
| `converted_opportunity_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for converted_opportunity |
| `duplicate_hash` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `tags` | `TEXT` | Yes | NULL | Operational entity attribute |
| `custom_fields` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_opportunities`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `account_id` -> `crm_accounts(id)`
  - `contact_id` -> `contacts(id)`
  - `lead_id` -> `crm_leads(id)`
  - `campaign_id` -> `crm_campaigns(id)`
  - `stage_id` -> `crm_opportunity_stages(id)`
  - `sales_quote_id` -> `quotes(id)`
  - `project_id` -> `projects(id)`
- **Indexes & Constraints**:
  - `crm_opportunities_workflow_instance_id_index` (Unique: No)
  - `crm_opportunities_tenant_id_stage_id_status_index` (Unique: No)
  - `crm_opportunities_tenant_id_expected_close_date_index` (Unique: No)
  - `crm_opportunities_tenant_id_amount_index` (Unique: No)
  - `crm_opportunities_status_index` (Unique: No)
  - `crm_opportunities_owner_user_id_index` (Unique: No)
  - `crm_opportunities_forecast_category_index` (Unique: No)
  - `crm_opportunities_approval_status_index` (Unique: No)
  - `sqlite_autoindex_crm_opportunities_2` (Unique: Yes)
  - `sqlite_autoindex_crm_opportunities_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `lead_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lead |
| `campaign_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for campaign |
| `stage_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for stage |
| `owner_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for owner_user |
| `opportunity_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `expected_revenue` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `probability` | `NUMERIC(16, 4)` | No | `10` | Operational entity attribute |
| `forecast_category` | `VARCHAR(255)` | No | `'pipeline'` | Operational entity attribute |
| `expected_close_date` | `DATE` | No | NULL | Operational entity attribute |
| `actual_close_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `win_loss_reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `competitor` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'not_required'` | State machine status indicator |
| `sales_quote_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_quote |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `tags` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_opportunity_line_items`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `opportunity_id` -> `crm_opportunities(id)`
- **Indexes & Constraints**:
  - `crm_opportunity_line_items_tenant_id_opportunity_id_index` (Unique: No)
  - `sqlite_autoindex_crm_opportunity_line_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `opportunity_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for opportunity |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `crm_opportunity_stages`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `crm_opportunity_stages_tenant_id_sequence_index` (Unique: No)
  - `sqlite_autoindex_crm_opportunity_stages_2` (Unique: Yes)
  - `sqlite_autoindex_crm_opportunity_stages_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `sequence` | `INTEGER` | No | `10` | Operational entity attribute |
| `default_probability` | `NUMERIC(16, 4)` | No | `10` | Operational entity attribute |
| `is_won` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_lost` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `stale_days` | `INTEGER` | No | `30` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `customer_agreements`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `customer_id` -> `contacts(id)`
  - `price_list_id` -> `price_lists(id)`
  - `payment_term_id` -> `payment_terms(id)`
- **Indexes & Constraints**:
  - `customer_agreements_status_index` (Unique: No)
  - `customer_agreements_agreement_number_index` (Unique: No)
  - `sqlite_autoindex_customer_agreements_2` (Unique: Yes)
  - `sqlite_autoindex_customer_agreements_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `agreement_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `total_committed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `consumed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `price_list_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for price_list |
| `payment_term_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payment_term |
| `terms_and_conditions` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `customer_credit_profiles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `customer_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `customer_credit_profiles_is_credit_hold_index` (Unique: No)
  - `customer_credit_profiles_credit_status_index` (Unique: No)
  - `sqlite_autoindex_customer_credit_profiles_2` (Unique: Yes)
  - `sqlite_autoindex_customer_credit_profiles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `credit_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `used_credit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `pending_orders_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_exposure` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `overdue_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `overdue_invoices_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `max_overdue_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `credit_status` | `VARCHAR(255)` | No | `'good'` | State machine status indicator |
| `risk_rating` | `VARCHAR(255)` | No | `'low'` | Operational entity attribute |
| `is_credit_hold` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `hold_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `last_evaluated_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `evaluated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `customer_groups`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `price_list_id` -> `price_lists(id)`
  - `payment_term_id` -> `payment_terms(id)`
- **Indexes & Constraints**:
  - `customer_groups_code_index` (Unique: No)
  - `sqlite_autoindex_customer_groups_2` (Unique: Yes)
  - `sqlite_autoindex_customer_groups_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `price_list_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for price_list |
| `payment_term_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payment_term |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `customer_ledger`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `journal_entry_id` -> `journal_entries(id)`
- **Indexes & Constraints**:
  - `customer_ledger_tenant_id_index` (Unique: No)
  - `customer_ledger_journal_entry_id_index` (Unique: No)
  - `customer_ledger_customer_id_index` (Unique: No)
  - `customer_ledger_company_id_index` (Unique: No)
  - `sqlite_autoindex_customer_ledger_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `journal_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for journal_entry |
| `posting_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | No | NULL | Operational entity attribute |
| `original_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `open_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `dunning_level` | `INTEGER` | No | `0` | Operational entity attribute |
| `last_dunning_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `customer_ledger_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `customer_id` -> `contacts(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `customer_ledger_entries_tenant_id_status_due_date_index` (Unique: No)
  - `idx_a47dc036acd95efb_customer_ledger_entries` (Unique: No)
  - `customer_ledger_entries_status_index` (Unique: No)
  - `customer_ledger_entries_entry_type_index` (Unique: No)
  - `customer_ledger_entries_entry_number_index` (Unique: No)
  - `sqlite_autoindex_customer_ledger_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `entry_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `entry_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `entry_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `document_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `debit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `credit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `balance_after` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `exchange_rate` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `cleared_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `cleared_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

