# Module Reference: General Ledger, Chart of Accounts & Fiscal Compliance

**Module ID**: `08_general_ledger_and_fiscal`  
**Tables Count**: `22`  
**Description**: Double-entry bookkeeping, chart of accounts, journal entries, VAT settlements, tax ledgers, and fiscal closures.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `accounting_anomalies` | Tenant-Scoped | `id` | `undefined->journal_entries` | `accounting_anomalies_tenant_id_index, accounting_anomalies_journal_entry_id_index` |
| `accrual_entries` | Tenant-Scoped | `id` | `undefined->chart_of_accounts, undefined->chart_of_accounts` | `accrual_entries_tenant_id_index, accrual_entries_company_id_index` |
| `chart_of_accounts` | Shared Lookup | `id` | `undefined->tenants` | `chart_of_accounts_type_index, chart_of_accounts_standard_index` |
| `cost_centers` | Tenant-Scoped | `id` | None | `cost_centers_tenant_id_index, cost_centers_company_id_index` |
| `financial_closing_runs` | Tenant-Scoped | `id` | `undefined->fiscal_periods` | `financial_closing_runs_tenant_id_index, financial_closing_runs_fiscal_period_id_index` |
| `fiscal_periods` | Tenant-Scoped | `id` | `undefined->fiscal_years` | `fiscal_periods_tenant_id_index, fiscal_periods_fiscal_year_id_index` |
| `fiscal_years` | Tenant-Scoped | `id` | None | `fiscal_years_tenant_id_index, fiscal_years_company_id_index` |
| `general_ledger_entries` | Shared Lookup | `id` | `undefined->tenants` | `general_ledger_entries_reference_type_reference_id_index, general_ledger_entries_entry_number_index` |
| `general_ledger_lines` | System / Global | `id` | `undefined->general_ledger_entries, undefined->chart_of_accounts` | `PRIMARY` |
| `journal_batches` | Tenant-Scoped | `id` | None | `journal_batches_tenant_id_index, journal_batches_company_id_index` |
| `journal_entries` | Tenant-Scoped | `id` | `undefined->journal_batches, undefined->fiscal_periods` | `journal_entries_tenant_id_index, journal_entries_source_document_id_index` |
| `journal_lines` | Tenant-Scoped | `id` | `undefined->journal_entries, undefined->chart_of_accounts, undefined->cost_centers...` | `journal_lines_tenant_id_index, journal_lines_project_id_index` |
| `period_locks` | Tenant-Scoped | `id` | `undefined->fiscal_periods` | `period_locks_tenant_id_index, period_locks_fiscal_period_id_index` |
| `posting_templates` | Tenant-Scoped | `id` | None | `posting_templates_tenant_id_index, posting_templates_company_id_index` |
| `profit_centers` | Tenant-Scoped | `id` | None | `profit_centers_tenant_id_index, profit_centers_company_id_index` |
| `reconciliation_items` | Tenant-Scoped | `id` | `undefined->reconciliation_runs` | `reconciliation_items_tenant_id_index, reconciliation_items_reconciliation_run_id_index` |
| `reconciliation_matches` | Tenant-Scoped | `id` | None | `reconciliation_matches_tenant_id_index, reconciliation_matches_matched_entity_id_index` |
| `reconciliation_runs` | Tenant-Scoped | `id` | `undefined->chart_of_accounts` | `reconciliation_runs_tenant_id_index, reconciliation_runs_period_id_index` |
| `vat_code_translations` | Shared Lookup | `id` | `undefined->vat_codes` | `vat_code_translations_tenant_id_index, vat_code_translations_locale_index` |
| `vat_codes` | Shared Lookup | `id` | None | `vat_codes_tenant_id_index, vat_codes_country_iso_index` |
| `vat_registers` | Tenant-Scoped | `id` | None | `vat_registers_tenant_id_index, vat_registers_company_id_index` |
| `vat_settlements` | Shared Lookup | `id` | `undefined->tenants` | `vat_settlements_year_index, vat_settlements_period_index` |

---

## Detailed Entity Schema & Data Dictionary

### `accounting_anomalies`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `journal_entry_id` -> `journal_entries(id)`
- **Indexes & Constraints**:
  - `accounting_anomalies_tenant_id_index` (Unique: No)
  - `accounting_anomalies_journal_entry_id_index` (Unique: No)
  - `accounting_anomalies_company_id_index` (Unique: No)
  - `sqlite_autoindex_accounting_anomalies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `journal_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for journal_entry |
| `anomaly_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `severity` | `VARCHAR(255)` | No | `'warning'` | Operational entity attribute |
| `confidence_score` | `NUMERIC(16, 4)` | No | `90` | Operational entity attribute |
| `explanation` | `TEXT` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `detected_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `accrual_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `debit_account_id` -> `chart_of_accounts(id)`
  - `credit_account_id` -> `chart_of_accounts(id)`
- **Indexes & Constraints**:
  - `accrual_entries_tenant_id_index` (Unique: No)
  - `accrual_entries_company_id_index` (Unique: No)
  - `sqlite_autoindex_accrual_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `accrual_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `total_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `periods_count` | `INTEGER` | No | NULL | Operational entity attribute |
| `monthly_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `debit_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for debit_account |
| `credit_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for credit_account |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `chart_of_accounts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `chart_of_accounts_type_index` (Unique: No)
  - `chart_of_accounts_standard_index` (Unique: No)
  - `chart_of_accounts_company_id_index` (Unique: No)
  - `chart_of_accounts_code_index` (Unique: No)
  - `chart_of_accounts_account_code_index` (Unique: No)
  - `sqlite_autoindex_chart_of_accounts_2` (Unique: Yes)
  - `sqlite_autoindex_chart_of_accounts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `standard` | `VARCHAR(255)` | No | `'it_general_ledger'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `parent_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent_account |
| `account_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `account_class` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `account_type` | `VARCHAR(255)` | No | `'asset'` | Operational entity attribute |
| `normal_balance` | `VARCHAR(255)` | No | `'debit'` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `is_reconciliation_account` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `reconciliation_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `allows_manual_posting` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `is_cost_center_mandatory` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |

---

### `cost_centers`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `cost_centers_tenant_id_index` (Unique: No)
  - `cost_centers_company_id_index` (Unique: No)
  - `sqlite_autoindex_cost_centers_2` (Unique: Yes)
  - `sqlite_autoindex_cost_centers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `financial_closing_runs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `fiscal_period_id` -> `fiscal_periods(id)`
- **Indexes & Constraints**:
  - `financial_closing_runs_tenant_id_index` (Unique: No)
  - `financial_closing_runs_fiscal_period_id_index` (Unique: No)
  - `financial_closing_runs_company_id_index` (Unique: No)
  - `sqlite_autoindex_financial_closing_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `fiscal_period_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for fiscal_period |
| `closing_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'completed'` | State machine status indicator |
| `closing_journal_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for closing_journal |
| `retained_earnings_journal_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for retained_earnings_journal |
| `net_income_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `executed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `executed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `fiscal_periods`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `fiscal_year_id` -> `fiscal_years(id)`
- **Indexes & Constraints**:
  - `fiscal_periods_tenant_id_index` (Unique: No)
  - `fiscal_periods_fiscal_year_id_index` (Unique: No)
  - `fiscal_periods_company_id_index` (Unique: No)
  - `sqlite_autoindex_fiscal_periods_2` (Unique: Yes)
  - `sqlite_autoindex_fiscal_periods_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `fiscal_year_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for fiscal_year |
| `period_number` | `INTEGER` | No | NULL | Unique business identification code or document number |
| `period_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `fiscal_years`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `fiscal_years_tenant_id_index` (Unique: No)
  - `fiscal_years_company_id_index` (Unique: No)
  - `sqlite_autoindex_fiscal_years_2` (Unique: Yes)
  - `sqlite_autoindex_fiscal_years_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `year_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `closed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `closed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `general_ledger_entries`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `general_ledger_entries_reference_type_reference_id_index` (Unique: No)
  - `general_ledger_entries_entry_number_index` (Unique: No)
  - `general_ledger_entries_date_index` (Unique: No)
  - `sqlite_autoindex_general_ledger_entries_2` (Unique: Yes)
  - `sqlite_autoindex_general_ledger_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `entry_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `reference_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reference_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for reference |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `general_ledger_lines`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `general_ledger_entry_id` -> `general_ledger_entries(id)`
  - `account_id` -> `chart_of_accounts(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_general_ledger_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `general_ledger_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for general_ledger_entry |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `line_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `debit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `credit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `journal_batches`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `journal_batches_tenant_id_index` (Unique: No)
  - `journal_batches_company_id_index` (Unique: No)
  - `sqlite_autoindex_journal_batches_2` (Unique: Yes)
  - `sqlite_autoindex_journal_batches_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `batch_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `source_module` | `VARCHAR(255)` | No | `'MANUAL'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `total_debit` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_credit` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `posted_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `journal_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `batch_id` -> `journal_batches(id)`
  - `fiscal_period_id` -> `fiscal_periods(id)`
- **Indexes & Constraints**:
  - `journal_entries_tenant_id_index` (Unique: No)
  - `journal_entries_source_document_id_index` (Unique: No)
  - `journal_entries_posting_date_index` (Unique: No)
  - `journal_entries_fiscal_period_id_index` (Unique: No)
  - `journal_entries_company_id_index` (Unique: No)
  - `journal_entries_batch_id_index` (Unique: No)
  - `sqlite_autoindex_journal_entries_2` (Unique: Yes)
  - `sqlite_autoindex_journal_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `batch_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for batch |
| `fiscal_period_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for fiscal_period |
| `entry_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `posting_date` | `DATE` | No | NULL | Operational entity attribute |
| `document_date` | `DATE` | No | NULL | Operational entity attribute |
| `ledger_type` | `VARCHAR(255)` | No | `'statutory'` | Operational entity attribute |
| `journal_type` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `reversal_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `reversal_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for reversal_journal_entry |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `source_document_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `source_document_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for source_document |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `posted_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `posted_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reversed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `reversed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `journal_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `journal_entry_id` -> `journal_entries(id)`
  - `account_id` -> `chart_of_accounts(id)`
  - `cost_center_id` -> `cost_centers(id)`
  - `profit_center_id` -> `profit_centers(id)`
  - `vat_code_id` -> `vat_codes(id)`
- **Indexes & Constraints**:
  - `journal_lines_tenant_id_index` (Unique: No)
  - `journal_lines_project_id_index` (Unique: No)
  - `journal_lines_profit_center_id_index` (Unique: No)
  - `journal_lines_posting_date_index` (Unique: No)
  - `journal_lines_partner_id_index` (Unique: No)
  - `journal_lines_journal_entry_id_index` (Unique: No)
  - `journal_lines_cost_center_id_index` (Unique: No)
  - `journal_lines_account_id_index` (Unique: No)
  - `sqlite_autoindex_journal_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `journal_entry_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for journal_entry |
| `posting_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `line_number` | `INTEGER` | No | NULL | Unique business identification code or document number |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `profit_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for profit_center |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `partner_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `partner_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for partner |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `debit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `credit_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `exchange_rate` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `amount_in_functional_currency` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `vat_code_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for vat_code |
| `vat_base_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `vat_tax_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_cleared` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `clearing_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `period_locks`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `fiscal_period_id` -> `fiscal_periods(id)`
- **Indexes & Constraints**:
  - `period_locks_tenant_id_index` (Unique: No)
  - `period_locks_fiscal_period_id_index` (Unique: No)
  - `sqlite_autoindex_period_locks_2` (Unique: Yes)
  - `sqlite_autoindex_period_locks_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `fiscal_period_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for fiscal_period |
| `subledger_module` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_locked` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `locked_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `locked_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `posting_templates`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `posting_templates_tenant_id_index` (Unique: No)
  - `posting_templates_company_id_index` (Unique: No)
  - `sqlite_autoindex_posting_templates_2` (Unique: Yes)
  - `sqlite_autoindex_posting_templates_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `source_event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `template_payload` | `TEXT` | No | `'[]'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `profit_centers`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `profit_centers_tenant_id_index` (Unique: No)
  - `profit_centers_company_id_index` (Unique: No)
  - `sqlite_autoindex_profit_centers_2` (Unique: Yes)
  - `sqlite_autoindex_profit_centers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `reconciliation_items`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `reconciliation_run_id` -> `reconciliation_runs(id)`
- **Indexes & Constraints**:
  - `reconciliation_items_tenant_id_index` (Unique: No)
  - `reconciliation_items_reconciliation_run_id_index` (Unique: No)
  - `sqlite_autoindex_reconciliation_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `reconciliation_run_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for reconciliation_run |
| `item_reference` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `gl_line_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_line |
| `subledger_item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for subledger_item |
| `item_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `variance_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_matched` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `match_type` | `VARCHAR(255)` | No | `'automatic'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `reconciliation_matches`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `reconciliation_matches_tenant_id_index` (Unique: No)
  - `reconciliation_matches_matched_entity_id_index` (Unique: No)
  - `reconciliation_matches_journal_entry_id_index` (Unique: No)
  - `reconciliation_matches_bank_statement_line_id_index` (Unique: No)
  - `reconciliation_matches_bank_reconciliation_id_index` (Unique: No)
  - `sqlite_autoindex_reconciliation_matches_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_reconciliation_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_reconciliation |
| `bank_statement_line_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_statement_line |
| `matched_entity_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `matched_entity_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for matched_entity |
| `match_type` | `VARCHAR(255)` | No | `'exact_ref'` | Operational entity attribute |
| `allocated_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `confidence_score` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `reconciled_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `reconciliation_runs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `account_id` -> `chart_of_accounts(id)`
- **Indexes & Constraints**:
  - `reconciliation_runs_tenant_id_index` (Unique: No)
  - `reconciliation_runs_period_id_index` (Unique: No)
  - `reconciliation_runs_company_id_index` (Unique: No)
  - `reconciliation_runs_account_id_index` (Unique: No)
  - `sqlite_autoindex_reconciliation_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `reconciliation_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `period_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for period |
| `account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for account |
| `status` | `VARCHAR(255)` | No | `'reconciled'` | State machine status indicator |
| `gl_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `subledger_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `variance_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `reconciled_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reconciled_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `vat_code_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `vat_code_id` -> `vat_codes(id)`
- **Indexes & Constraints**:
  - `vat_code_translations_tenant_id_index` (Unique: No)
  - `vat_code_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_vat_code_translations_2` (Unique: Yes)
  - `sqlite_autoindex_vat_code_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `vat_code_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for vat_code |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `legal_description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `vat_codes`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `vat_codes_tenant_id_index` (Unique: No)
  - `vat_codes_country_iso_index` (Unique: No)
  - `vat_codes_company_id_index` (Unique: No)
  - `sqlite_autoindex_vat_codes_2` (Unique: Yes)
  - `sqlite_autoindex_vat_codes_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `country_iso` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `nature` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_split_payment` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_reverse_charge` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `description` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `tax_rate_percent` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `country` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_non_deductible` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `non_deductible_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `gl_sales_tax_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_sales_tax_account |
| `gl_purchase_tax_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_purchase_tax_account |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `vat_registers`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `vat_registers_tenant_id_index` (Unique: No)
  - `vat_registers_company_id_index` (Unique: No)
  - `sqlite_autoindex_vat_registers_2` (Unique: Yes)
  - `sqlite_autoindex_vat_registers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `register_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `progressive_protocol_year` | `INTEGER` | No | NULL | Operational entity attribute |
| `last_protocol_number` | `INTEGER` | No | `0` | Unique business identification code or document number |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `vat_settlements`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `vat_settlements_year_index` (Unique: No)
  - `vat_settlements_period_index` (Unique: No)
  - `vat_settlements_fiscal_period_id_index` (Unique: No)
  - `vat_settlements_company_id_index` (Unique: No)
  - `sqlite_autoindex_vat_settlements_2` (Unique: Yes)
  - `sqlite_autoindex_vat_settlements_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `period_type` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `year` | `INTEGER` | No | NULL | Operational entity attribute |
| `period` | `INTEGER` | No | NULL | Operational entity attribute |
| `total_debit_vat` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_credit_vat` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `payable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_paid` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `payment_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `fiscal_period_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for fiscal_period |
| `settlement_period` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `output_vat_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `input_vat_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `prior_credit_used` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `net_vat_payable` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `net_vat_credit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'calculated'` | State machine status indicator |
| `settlement_journal_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for settlement_journal |
| `calculated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

