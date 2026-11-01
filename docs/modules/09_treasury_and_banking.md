# Module Reference: Treasury, Banking & Cash Management

**Module ID**: `09_treasury_and_banking`  
**Tables Count**: `38`  
**Description**: Bank feeds, statements, cash forecasting, multi-currency FX revaluation, liquidity pools, loans, and guarantees.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `bank_account_balances` | Tenant-Scoped | `id` | None | `bank_account_balances_tenant_id_index, bank_account_balances_bank_account_id_index` |
| `bank_account_signatories` | Tenant-Scoped | `id` | None | `bank_account_signatories_user_id_index, bank_account_signatories_tenant_id_index` |
| `bank_accounts` | Shared Lookup | `id` | `undefined->tenants` | `bank_accounts_tenant_id_currency_index, bank_accounts_qr_iban_index` |
| `bank_branches` | Tenant-Scoped | `id` | None | `bank_branches_tenant_id_index, bank_branches_tenant_id_bank_name_index` |
| `bank_connections` | Tenant-Scoped | `id` | None | `bank_connections_tenant_id_index, bank_connections_company_id_index` |
| `bank_guarantees` | Tenant-Scoped | `id` | None | `bank_guarantees_tenant_id_index, bank_guarantees_project_id_index` |
| `bank_reconciliations` | Tenant-Scoped | `id` | None | `bank_reconciliations_tenant_id_index, idx_7dd7a958509d336d_bank_reconciliations` |
| `bank_statement_lines` | Shared Lookup | `id` | `undefined->bank_statements, undefined->tenants` | `bank_statement_lines_tenant_id_reconciled_index, bank_statement_lines_reference_index` |
| `bank_statements` | Shared Lookup | `id` | `undefined->tenants` | `bank_statements_tenant_id_status_index, bank_statements_tenant_id_source_format_index` |
| `bank_transactions` | Shared Lookup | `id` | `undefined->tenants, undefined->bank_accounts` | `bank_transactions_value_date_index, bank_transactions_tenant_id_booking_date_index` |
| `cash_forecast_lines` | Tenant-Scoped | `id` | None | `cash_forecast_lines_tenant_id_projected_date_flow_type_index, cash_forecast_lines_tenant_id_index` |
| `cash_forecasts` | Tenant-Scoped | `id` | None | `cash_forecasts_tenant_id_index, cash_forecasts_tenant_id_calculation_date_index` |
| `cash_pools` | Tenant-Scoped | `id` | None | `cash_pools_tenant_id_index, cash_pools_header_bank_account_id_index` |
| `currencies` | Shared Lookup | `id` | None | `currencies_tenant_id_index` |
| `exchange_rates` | System / Global | `id` | None | `exchange_rates_target_index, exchange_rates_source_index` |
| `fx_positions` | Tenant-Scoped | `id` | None | `fx_positions_tenant_id_index, fx_positions_currency_index` |
| `fx_revaluations` | Tenant-Scoped | `id` | None | `fx_revaluations_tenant_id_index, fx_revaluations_period_end_date_index` |
| `intercompany_funding` | Tenant-Scoped | `id` | None | `intercompany_funding_transfer_date_index, intercompany_funding_tenant_id_index` |
| `interest_schedules` | Tenant-Scoped | `id` | None | `interest_schedules_tenant_id_index, interest_schedules_payment_line_id_index` |
| `letters_of_credit` | Tenant-Scoped | `id` | None | `letters_of_credit_tenant_id_index, letters_of_credit_lc_reference_index` |
| `loan_agreements` | Tenant-Scoped | `id` | None | `loan_agreements_workflow_instance_id_index, loan_agreements_tenant_id_index` |
| `loan_drawdowns` | Tenant-Scoped | `id` | None | `loan_drawdowns_tenant_id_index, loan_drawdowns_loan_agreement_id_index` |
| `payment_approvals` | Tenant-Scoped | `id` | None | `payment_approvals_tenant_id_index, payment_approvals_payment_batch_id_index` |
| `payment_batches` | Shared Lookup | `id` | `undefined->tenants` | `payment_batches_workflow_instance_id_index, payment_batches_tenant_id_index` |
| `payment_executions` | Tenant-Scoped | `id` | None | `payment_executions_tenant_id_index, payment_executions_payment_batch_id_index` |
| `payment_import_lines` | Shared Lookup | `id` | `undefined->tenants, undefined->payment_imports, undefined->invoices...` | `payment_import_lines_payment_import_id_status_index` |
| `payment_imports` | Shared Lookup | `id` | `undefined->tenants` | `payment_imports_user_id_index, payment_imports_tenant_id_index` |
| `payment_lines` | Tenant-Scoped | `id` | None | `payment_lines_tenant_id_status_execution_date_index, payment_lines_tenant_id_index` |
| `payment_method_translations` | Shared Lookup | `id` | `undefined->payment_methods` | `payment_method_translations_tenant_id_index, payment_method_translations_locale_index` |
| `payment_methods` | Shared Lookup | `id` | None | `payment_methods_tenant_id_index` |
| `payment_reminders` | Shared Lookup | `id` | `undefined->tenants, undefined->invoices` | `payment_reminders_tenant_id_index, payment_reminders_invoice_id_level_index` |
| `payment_term_installments` | System / Global | `id` | `undefined->payment_terms` | `PRIMARY` |
| `payment_term_translations` | Shared Lookup | `id` | `undefined->payment_terms` | `payment_term_translations_tenant_id_index, payment_term_translations_locale_index` |
| `payment_terms` | Shared Lookup | `id` | `undefined->tenants` | `PRIMARY` |
| `payments` | Shared Lookup | `id` | `undefined->tenants, undefined->invoices` | `payments_tenant_id_paid_at_idx, payments_tenant_id_index` |
| `receivable_collections` | Tenant-Scoped | `id` | None | `receivable_collections_tenant_id_status_due_date_index, receivable_collections_tenant_id_index` |
| `treasury_alerts` | Tenant-Scoped | `id` | None | `treasury_alerts_tenant_id_severity_is_acknowledged_index, treasury_alerts_tenant_id_index` |
| `working_capital_metrics` | Tenant-Scoped | `id` | None | `working_capital_metrics_tenant_id_index, working_capital_metrics_metric_date_index` |

---

## Detailed Entity Schema & Data Dictionary

### `bank_account_balances`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_account_balances_tenant_id_index` (Unique: No)
  - `bank_account_balances_bank_account_id_index` (Unique: No)
  - `bank_account_balances_balance_date_index` (Unique: No)
  - `sqlite_autoindex_bank_account_balances_2` (Unique: Yes)
  - `sqlite_autoindex_bank_account_balances_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_account |
| `balance_date` | `DATE` | No | NULL | Operational entity attribute |
| `ledger_balance` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `available_balance` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `source` | `VARCHAR(255)` | No | `'statement'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_account_signatories`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_account_signatories_user_id_index` (Unique: No)
  - `bank_account_signatories_tenant_id_index` (Unique: No)
  - `idx_f72f1a608d757fad_bank_account_signatories` (Unique: No)
  - `bank_account_signatories_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_bank_account_signatories_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_account |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `authorization_level` | `VARCHAR(255)` | No | `'sole'` | Operational entity attribute |
| `single_transaction_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `daily_transaction_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `valid_from` | `DATE` | No | NULL | Operational entity attribute |
| `valid_until` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_accounts`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `bank_accounts_tenant_id_currency_index` (Unique: No)
  - `bank_accounts_qr_iban_index` (Unique: No)
  - `bank_accounts_iban_index` (Unique: No)
  - `bank_accounts_gl_account_id_index` (Unique: No)
  - `bank_accounts_company_id_index` (Unique: No)
  - `bank_accounts_account_number_index` (Unique: No)
  - `sqlite_autoindex_bank_accounts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `iban` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `qr_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `bic_swift` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `current_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `branch_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `account_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `account_type` | `VARCHAR(255)` | No | `'checking'` | Operational entity attribute |
| `gl_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_account |
| `overdraft_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `credit_line_limit` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `opening_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `available_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_pool_header` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |

---

### `bank_branches`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_branches_tenant_id_index` (Unique: No)
  - `bank_branches_tenant_id_bank_name_index` (Unique: No)
  - `bank_branches_company_id_index` (Unique: No)
  - `bank_branches_branch_code_index` (Unique: No)
  - `bank_branches_bic_swift_index` (Unique: No)
  - `sqlite_autoindex_bank_branches_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `bank_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `branch_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `branch_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `bic_swift` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `routing_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `city` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `country` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_connections`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_connections_tenant_id_index` (Unique: No)
  - `bank_connections_company_id_index` (Unique: No)
  - `sqlite_autoindex_bank_connections_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `protocol` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `provider_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `endpoint_url` | `TEXT` | Yes | NULL | Operational entity attribute |
| `partner_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for partner |
| `host_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for host |
| `client_certificate_encrypted` | `TEXT` | Yes | NULL | Operational entity attribute |
| `private_key_encrypted` | `TEXT` | Yes | NULL | Operational entity attribute |
| `auth_credentials_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `polling_frequency_minutes` | `INTEGER` | No | `60` | Operational entity attribute |
| `last_poll_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_guarantees`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_guarantees_tenant_id_index` (Unique: No)
  - `bank_guarantees_project_id_index` (Unique: No)
  - `bank_guarantees_issuing_bank_account_id_index` (Unique: No)
  - `bank_guarantees_guarantee_number_index` (Unique: No)
  - `bank_guarantees_expiration_date_index` (Unique: No)
  - `bank_guarantees_company_id_index` (Unique: No)
  - `sqlite_autoindex_bank_guarantees_2` (Unique: Yes)
  - `sqlite_autoindex_bank_guarantees_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `guarantee_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `issuing_bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for issuing_bank_account |
| `beneficiary_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `beneficiary_tax_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for beneficiary_tax |
| `guarantee_type` | `VARCHAR(255)` | No | `'performance_bond'` | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `commission_rate_annual` | `NUMERIC(16, 4)` | No | `0.015` | Monetary or financial decimal quantity |
| `issue_date` | `DATE` | No | NULL | Operational entity attribute |
| `expiration_date` | `DATE` | No | NULL | Operational entity attribute |
| `collateral_cash_blocked` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `status` | `VARCHAR(255)` | No | `'issued'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_reconciliations`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `bank_reconciliations_tenant_id_index` (Unique: No)
  - `idx_7dd7a958509d336d_bank_reconciliations` (Unique: No)
  - `bank_reconciliations_reconciliation_number_index` (Unique: No)
  - `bank_reconciliations_company_id_index` (Unique: No)
  - `bank_reconciliations_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_bank_reconciliations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_account |
| `reconciliation_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `period_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `bank_statement_balance` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `gl_book_balance` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `difference_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'in_progress'` | State machine status indicator |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_statement_lines`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `bank_statement_id` -> `bank_statements(id)`
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `bank_statement_lines_tenant_id_reconciled_index` (Unique: No)
  - `bank_statement_lines_reference_index` (Unique: No)
  - `bank_statement_lines_reconciliation_category_index` (Unique: No)
  - `bank_statement_lines_qr_reference_index` (Unique: No)
  - `bank_statement_lines_matched_document_id_index` (Unique: No)
  - `bank_statement_lines_customer_reference_index` (Unique: No)
  - `bank_statement_lines_counterparty_iban_index` (Unique: No)
  - `bank_statement_lines_company_id_index` (Unique: No)
  - `bank_statement_lines_bank_reference_index` (Unique: No)
  - `bank_statement_lines_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_bank_statement_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_statement_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_statement |
| `line_number` | `INTEGER` | No | `0` | Unique business identification code or document number |
| `booking_date` | `DATE` | No | NULL | Operational entity attribute |
| `value_date` | `DATE` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `fee_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `direction` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `abi_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `qr_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `counterpart_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `counterpart_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reconciled` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `matched_document_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for matched_document |
| `reconciliation_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `reconciliation_category` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `ledger_account_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `reconciliation_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_account |
| `bank_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `customer_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `counterparty_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `counterparty_iban` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `counterparty_bic` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `remittance_information` | `TEXT` | Yes | NULL | Operational entity attribute |
| `iso_bank_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `reconciled_status` | `VARCHAR(255)` | No | `'unmatched'` | State machine status indicator |
| `reconciled_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_statements`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `bank_statements_tenant_id_status_index` (Unique: No)
  - `bank_statements_tenant_id_source_format_index` (Unique: No)
  - `bank_statements_statement_number_index` (Unique: No)
  - `bank_statements_company_id_index` (Unique: No)
  - `bank_statements_bank_account_id_index` (Unique: No)
  - `bank_statements_account_iban_index` (Unique: No)
  - `sqlite_autoindex_bank_statements_2` (Unique: Yes)
  - `sqlite_autoindex_bank_statements_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `source_format` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `account_iban` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `statement_date` | `DATE` | No | NULL | Operational entity attribute |
| `opening_balance` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `closing_balance` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `total_entries` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `content_hash` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_account |
| `statement_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `format` | `VARCHAR(255)` | No | `'CAMT_053'` | Operational entity attribute |
| `raw_file_storage_path` | `TEXT` | Yes | NULL | Operational entity attribute |
| `file_sha256` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `total_debits` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_credits` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `lines_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `reconciliation_status` | `VARCHAR(255)` | No | `'unreconciled'` | State machine status indicator |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `bank_transactions`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `bank_account_id` -> `bank_accounts(id)`
- **Indexes & Constraints**:
  - `bank_transactions_value_date_index` (Unique: No)
  - `bank_transactions_tenant_id_booking_date_index` (Unique: No)
  - `bank_transactions_status_index` (Unique: No)
  - `bank_transactions_reference_index` (Unique: No)
  - `bank_transactions_matched_invoice_id_index` (Unique: No)
  - `bank_transactions_gl_journal_entry_id_index` (Unique: No)
  - `bank_transactions_company_id_index` (Unique: No)
  - `bank_transactions_booking_date_index` (Unique: No)
  - `sqlite_autoindex_bank_transactions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for bank_account |
| `booking_date` | `DATE` | No | NULL | Operational entity attribute |
| `value_date` | `DATE` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `matched_invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for matched_invoice |
| `status` | `VARCHAR(255)` | No | `'unmatched'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `transaction_type` | `VARCHAR(255)` | No | `'transfer'` | Operational entity attribute |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |

---

### `cash_forecast_lines`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `cash_forecast_lines_tenant_id_projected_date_flow_type_index` (Unique: No)
  - `cash_forecast_lines_tenant_id_index` (Unique: No)
  - `cash_forecast_lines_source_entity_id_index` (Unique: No)
  - `cash_forecast_lines_projected_date_index` (Unique: No)
  - `cash_forecast_lines_company_id_index` (Unique: No)
  - `cash_forecast_lines_cash_forecast_id_index` (Unique: No)
  - `sqlite_autoindex_cash_forecast_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `cash_forecast_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for cash_forecast |
| `projected_date` | `DATE` | No | NULL | Operational entity attribute |
| `source_category` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `flow_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `confidence_weight` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `expected_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `weighted_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `source_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `source_entity_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for source_entity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `cash_forecasts`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `cash_forecasts_tenant_id_index` (Unique: No)
  - `cash_forecasts_tenant_id_calculation_date_index` (Unique: No)
  - `cash_forecasts_forecast_scenario_id_index` (Unique: No)
  - `cash_forecasts_forecast_number_index` (Unique: No)
  - `cash_forecasts_company_id_index` (Unique: No)
  - `cash_forecasts_calculation_date_index` (Unique: No)
  - `sqlite_autoindex_cash_forecasts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `forecast_scenario_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for forecast_scenario |
| `forecast_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `calculation_date` | `DATE` | No | NULL | Operational entity attribute |
| `horizon_days` | `INTEGER` | No | `90` | Operational entity attribute |
| `opening_cash_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `projected_inflows` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `projected_outflows` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `closing_cash_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `min_liquidity_threshold` | `NUMERIC(16, 4)` | No | `50000` | Operational entity attribute |
| `deficit_detected` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `deficit_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `cash_pools`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `cash_pools_tenant_id_index` (Unique: No)
  - `cash_pools_header_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_cash_pools_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `pool_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `pool_structure` | `VARCHAR(255)` | No | `'zero_balance_account'` | Operational entity attribute |
| `header_bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for header_bank_account |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `sweeping_frequency` | `VARCHAR(255)` | No | `'daily'` | Operational entity attribute |
| `target_balance_floor` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `target_balance_ceiling` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `currencies`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `currencies_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_currencies_2` (Unique: Yes)
  - `sqlite_autoindex_currencies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `symbol` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `precision` | `INTEGER` | No | `2` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `exchange_rates`

- **Operational Scope**: System / Global
- **Indexes & Constraints**:
  - `exchange_rates_target_index` (Unique: No)
  - `exchange_rates_source_index` (Unique: No)
  - `exchange_rates_effective_date_index` (Unique: No)
  - `sqlite_autoindex_exchange_rates_2` (Unique: Yes)
  - `sqlite_autoindex_exchange_rates_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `source` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `target` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `effective_date` | `DATE` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `fx_positions`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `fx_positions_tenant_id_index` (Unique: No)
  - `fx_positions_currency_index` (Unique: No)
  - `fx_positions_company_id_index` (Unique: No)
  - `fx_positions_as_of_date_index` (Unique: No)
  - `sqlite_autoindex_fx_positions_2` (Unique: Yes)
  - `sqlite_autoindex_fx_positions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `currency` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `total_cash_holdings` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `open_ar_exposure` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `open_ap_exposure` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `net_exposure` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `base_currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `latest_spot_rate` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `var_95_daily` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `as_of_date` | `DATE` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `fx_revaluations`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `fx_revaluations_tenant_id_index` (Unique: No)
  - `fx_revaluations_period_end_date_index` (Unique: No)
  - `fx_revaluations_gl_journal_entry_id_index` (Unique: No)
  - `fx_revaluations_currency_index` (Unique: No)
  - `fx_revaluations_company_id_index` (Unique: No)
  - `sqlite_autoindex_fx_revaluations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `period_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `foreign_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `book_value_base` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `revalued_market_base` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unrealized_gain_loss` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `intercompany_funding`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `intercompany_funding_transfer_date_index` (Unique: No)
  - `intercompany_funding_tenant_id_index` (Unique: No)
  - `intercompany_funding_source_bank_account_id_index` (Unique: No)
  - `intercompany_funding_gl_journal_entry_id_index` (Unique: No)
  - `intercompany_funding_destination_bank_account_id_index` (Unique: No)
  - `intercompany_funding_cash_pool_id_index` (Unique: No)
  - `sqlite_autoindex_intercompany_funding_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `cash_pool_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cash_pool |
| `source_bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for source_bank_account |
| `destination_bank_account_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for destination_bank_account |
| `transfer_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `transfer_date` | `DATE` | No | NULL | Operational entity attribute |
| `intercompany_interest_rate` | `NUMERIC(16, 4)` | No | `0.025` | Monetary or financial decimal quantity |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `status` | `VARCHAR(255)` | No | `'executed'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `interest_schedules`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `interest_schedules_tenant_id_index` (Unique: No)
  - `interest_schedules_payment_line_id_index` (Unique: No)
  - `interest_schedules_loan_agreement_id_index` (Unique: No)
  - `interest_schedules_due_date_index` (Unique: No)
  - `sqlite_autoindex_interest_schedules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `loan_agreement_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for loan_agreement |
| `period_start_date` | `DATE` | No | NULL | Operational entity attribute |
| `period_end_date` | `DATE` | No | NULL | Operational entity attribute |
| `due_date` | `DATE` | No | NULL | Operational entity attribute |
| `principal_due` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `interest_due` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_due` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `remaining_balance` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'accrued'` | State machine status indicator |
| `payment_line_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payment_line |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `letters_of_credit`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `letters_of_credit_tenant_id_index` (Unique: No)
  - `letters_of_credit_lc_reference_index` (Unique: No)
  - `letters_of_credit_expiry_date_index` (Unique: No)
  - `letters_of_credit_company_id_index` (Unique: No)
  - `sqlite_autoindex_letters_of_credit_2` (Unique: Yes)
  - `sqlite_autoindex_letters_of_credit_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `lc_reference` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `type` | `VARCHAR(255)` | No | `'import_documentary'` | Operational entity attribute |
| `issuing_bank` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `advising_bank` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `applicant_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `beneficiary_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `issue_date` | `DATE` | No | NULL | Operational entity attribute |
| `expiry_date` | `DATE` | No | NULL | Operational entity attribute |
| `incoterms` | `VARCHAR(255)` | No | `'FOB'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'opened'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `loan_agreements`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `loan_agreements_workflow_instance_id_index` (Unique: No)
  - `loan_agreements_tenant_id_index` (Unique: No)
  - `loan_agreements_loan_reference_index` (Unique: No)
  - `loan_agreements_lender_bank_account_id_index` (Unique: No)
  - `loan_agreements_company_id_index` (Unique: No)
  - `sqlite_autoindex_loan_agreements_2` (Unique: Yes)
  - `sqlite_autoindex_loan_agreements_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `loan_reference` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `lender_bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lender_bank_account |
| `loan_type` | `VARCHAR(255)` | No | `'term_loan'` | Operational entity attribute |
| `principal_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `interest_rate_type` | `VARCHAR(255)` | No | `'fixed'` | Monetary or financial decimal quantity |
| `nominal_rate` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `spread_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `origination_date` | `DATE` | No | NULL | Operational entity attribute |
| `maturity_date` | `DATE` | No | NULL | Operational entity attribute |
| `repayment_structure` | `VARCHAR(255)` | No | `'french_amortization'` | Operational entity attribute |
| `covenant_clause_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `loan_drawdowns`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `loan_drawdowns_tenant_id_index` (Unique: No)
  - `loan_drawdowns_loan_agreement_id_index` (Unique: No)
  - `loan_drawdowns_gl_journal_entry_id_index` (Unique: No)
  - `loan_drawdowns_drawdown_date_index` (Unique: No)
  - `loan_drawdowns_destination_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_loan_drawdowns_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `loan_agreement_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for loan_agreement |
| `drawdown_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `drawdown_date` | `DATE` | No | NULL | Operational entity attribute |
| `destination_bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for destination_bank_account |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `payment_approvals`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `payment_approvals_tenant_id_index` (Unique: No)
  - `payment_approvals_payment_batch_id_index` (Unique: No)
  - `payment_approvals_approver_user_id_index` (Unique: No)
  - `sqlite_autoindex_payment_approvals_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `payment_batch_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_batch |
| `approver_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for approver_user |
| `approval_tier` | `INTEGER` | No | `1` | Operational entity attribute |
| `signature_hash` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `ip_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `decision` | `VARCHAR(255)` | No | `'approved'` | Operational entity attribute |
| `decision_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `approved_at` | `TIMESTAMP` | No | `CURRENT_TIMESTAMP` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `payment_batches`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `payment_batches_workflow_instance_id_index` (Unique: No)
  - `payment_batches_tenant_id_index` (Unique: No)
  - `payment_batches_status_index` (Unique: No)
  - `payment_batches_created_by_index` (Unique: No)
  - `payment_batches_company_id_index` (Unique: No)
  - `payment_batches_batch_reference_index` (Unique: No)
  - `payment_batches_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_payment_batches_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `format` | `VARCHAR(255)` | No | `'sepa_pain_001_it'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `file_path` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `execution_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_account |
| `batch_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `payment_method` | `VARCHAR(255)` | No | `'sepa_credit_transfer'` | Operational entity attribute |
| `item_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `xml_message_storage_path` | `TEXT` | Yes | NULL | Operational entity attribute |
| `xml_sha256` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `payment_executions`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `payment_executions_tenant_id_index` (Unique: No)
  - `payment_executions_payment_batch_id_index` (Unique: No)
  - `payment_executions_bank_transmission_reference_index` (Unique: No)
  - `sqlite_autoindex_payment_executions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `payment_batch_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_batch |
| `protocol` | `VARCHAR(255)` | No | `'sepa_pain001'` | Operational entity attribute |
| `bank_transmission_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `pain002_status_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `clearing_timestamp` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `response_payload_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `payment_import_lines`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `payment_import_id` -> `payment_imports(id)`
  - `invoice_id` -> `invoices(id)`
  - `payment_id` -> `payments(id)`
- **Indexes & Constraints**:
  - `payment_import_lines_payment_import_id_status_index` (Unique: No)
  - `sqlite_autoindex_payment_import_lines_2` (Unique: Yes)
  - `sqlite_autoindex_payment_import_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `payment_import_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_import |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `payment_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payment |
| `entry_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `booking_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'CHF'` | Operational entity attribute |
| `reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `remittance_info` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `debtor_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'unmatched'` | State machine status indicator |
| `note` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `fee_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `reference_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |

---

### `payment_imports`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `payment_imports_user_id_index` (Unique: No)
  - `payment_imports_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_payment_imports_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `file_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `format` | `VARCHAR(255)` | No | `'camt'` | Operational entity attribute |
| `total_entries` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `matched_entries` | `INTEGER` | No | `0` | Operational entity attribute |
| `duplicate_entries` | `INTEGER` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `total_fees` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |

---

### `payment_lines`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `payment_lines_tenant_id_status_execution_date_index` (Unique: No)
  - `payment_lines_tenant_id_index` (Unique: No)
  - `payment_lines_status_index` (Unique: No)
  - `payment_lines_recipient_id_index` (Unique: No)
  - `payment_lines_recipient_iban_index` (Unique: No)
  - `payment_lines_payroll_payment_id_index` (Unique: No)
  - `payment_lines_payment_batch_id_index` (Unique: No)
  - `payment_lines_invoice_id_index` (Unique: No)
  - `payment_lines_instruction_id_index` (Unique: No)
  - `payment_lines_execution_date_index` (Unique: No)
  - `payment_lines_end_to_end_id_index` (Unique: No)
  - `payment_lines_company_id_index` (Unique: No)
  - `sqlite_autoindex_payment_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `payment_batch_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_batch |
| `line_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `recipient_type` | `VARCHAR(255)` | No | `'supplier'` | Operational entity attribute |
| `recipient_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for recipient |
| `recipient_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `recipient_iban` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `recipient_bic` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `instruction_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for instruction |
| `end_to_end_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for end_to_end |
| `remittance_reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `structured_creditor_ref` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `payroll_payment_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for payroll_payment |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `execution_date` | `DATE` | No | NULL | Operational entity attribute |
| `error_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `error_message` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `payment_method_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `payment_method_id` -> `payment_methods(id)`
- **Indexes & Constraints**:
  - `payment_method_translations_tenant_id_index` (Unique: No)
  - `payment_method_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_payment_method_translations_2` (Unique: Yes)
  - `sqlite_autoindex_payment_method_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `payment_method_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_method |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `payment_methods`

- **Operational Scope**: Shared Reference Lookup
- **Indexes & Constraints**:
  - `payment_methods_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_payment_methods_2` (Unique: Yes)
  - `sqlite_autoindex_payment_methods_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `is_electronic` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `requires_iban` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `payment_reminders`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `payment_reminders_tenant_id_index` (Unique: No)
  - `payment_reminders_invoice_id_level_index` (Unique: No)
  - `sqlite_autoindex_payment_reminders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `level` | `INTEGER` | No | NULL | Operational entity attribute |
| `channel` | `VARCHAR(255)` | No | `'email'` | Operational entity attribute |
| `recipient` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `amount_due` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'queued'` | State machine status indicator |
| `error` | `TEXT` | Yes | NULL | Operational entity attribute |
| `sent_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `payment_term_installments`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `payment_term_id` -> `payment_terms(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_payment_term_installments_2` (Unique: Yes)
  - `sqlite_autoindex_payment_term_installments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `payment_term_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_term |
| `sequence` | `INTEGER` | No | NULL | Operational entity attribute |
| `percent` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `days` | `INTEGER` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `payment_term_translations`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `payment_term_id` -> `payment_terms(id)`
- **Indexes & Constraints**:
  - `payment_term_translations_tenant_id_index` (Unique: No)
  - `payment_term_translations_locale_index` (Unique: No)
  - `sqlite_autoindex_payment_term_translations_2` (Unique: Yes)
  - `sqlite_autoindex_payment_term_translations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `payment_term_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for payment_term |
| `locale` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `invoice_clause` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |

---

### `payment_terms`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_payment_terms_2` (Unique: Yes)
  - `sqlite_autoindex_payment_terms_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `days` | `INTEGER` | No | `30` | Operational entity attribute |
| `end_of_month` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `discount_percent` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `discount_days` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `sdi_terms_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `payments`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `payments_tenant_id_paid_at_idx` (Unique: No)
  - `payments_tenant_id_index` (Unique: No)
  - `payments_invoice_id_paid_at_index` (Unique: No)
  - `payments_bank_statement_line_id_index` (Unique: No)
  - `sqlite_autoindex_payments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `paid_at` | `DATE` | No | NULL | Operational entity attribute |
| `payment_method` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `reference` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `type` | `VARCHAR(255)` | No | `'payment'` | Operational entity attribute |
| `bank_statement_line_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_statement_line |

---

### `receivable_collections`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `receivable_collections_tenant_id_status_due_date_index` (Unique: No)
  - `receivable_collections_tenant_id_index` (Unique: No)
  - `receivable_collections_status_index` (Unique: No)
  - `receivable_collections_invoice_id_index` (Unique: No)
  - `receivable_collections_due_date_index` (Unique: No)
  - `receivable_collections_customer_id_index` (Unique: No)
  - `receivable_collections_company_id_index` (Unique: No)
  - `receivable_collections_collection_date_index` (Unique: No)
  - `sqlite_autoindex_receivable_collections_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `expected_amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `collected_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `due_date` | `DATE` | No | NULL | Operational entity attribute |
| `collection_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `payment_method` | `VARCHAR(255)` | No | `'bank_transfer'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `aging_bucket` | `VARCHAR(255)` | No | `'current'` | Operational entity attribute |
| `dunning_level` | `INTEGER` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `treasury_alerts`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `treasury_alerts_tenant_id_severity_is_acknowledged_index` (Unique: No)
  - `treasury_alerts_tenant_id_index` (Unique: No)
  - `treasury_alerts_is_acknowledged_index` (Unique: No)
  - `treasury_alerts_company_id_index` (Unique: No)
  - `treasury_alerts_alert_type_index` (Unique: No)
  - `sqlite_autoindex_treasury_alerts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `alert_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `severity` | `VARCHAR(255)` | No | `'warning'` | Operational entity attribute |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `message` | `TEXT` | No | NULL | Operational entity attribute |
| `threshold_value` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `actual_value` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `is_acknowledged` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `acknowledged_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `acknowledged_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `payload_json` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `working_capital_metrics`

- **Operational Scope**: Tenant-Scoped
- **Indexes & Constraints**:
  - `working_capital_metrics_tenant_id_index` (Unique: No)
  - `working_capital_metrics_metric_date_index` (Unique: No)
  - `working_capital_metrics_company_id_index` (Unique: No)
  - `sqlite_autoindex_working_capital_metrics_2` (Unique: Yes)
  - `sqlite_autoindex_working_capital_metrics_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `metric_date` | `DATE` | No | NULL | Operational entity attribute |
| `accounts_receivable_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `accounts_payable_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `inventory_valuation_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `trailing_12m_revenue` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `trailing_12m_cogs` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `dso_days` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `dpo_days` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `dio_days` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `cash_conversion_cycle_days` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `current_ratio` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `quick_ratio` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

