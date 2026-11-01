# Module Reference: Subscription Management & Recurring Billing

**Module ID**: `15_subscriptions_and_recurring`  
**Tables Count**: `26`  
**Description**: SaaS plans, tiered pricing, subscription lifecycles, usage-based metering, dunning, churn prediction, and ASC 606 revenue recognition.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `billing_schedule_items` | System / Global | `id` | `undefined->billing_schedules, undefined->invoices` | `billing_schedule_items_status_index` |
| `billing_schedules` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts, undefined->sales_orders...` | `billing_schedules_status_index, billing_schedules_schedule_number_index` |
| `sub_billing_runs` | Tenant-Scoped | `id` | `undefined->tenants` | `sub_billing_runs_status_index, sub_billing_runs_run_number_index` |
| `sub_churn_predictions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_churn_predictions_risk_tier_index` |
| `sub_dunning_policies` | Tenant-Scoped | `id` | `undefined->tenants` | `sub_dunning_policies_company_id_index` |
| `sub_dunning_records` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_dunning_records_status_index, sub_dunning_records_invoice_id_index` |
| `sub_invoice_schedules` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_invoice_schedules_status_index, sub_invoice_schedules_scheduled_billing_date_index` |
| `sub_partner_commissions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_partner_commissions_status_index, sub_partner_commissions_partner_id_index` |
| `sub_performance_obligations` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_revenue_contracts` | `sub_performance_obligations_status_index, sub_performance_obligations_pob_code_index` |
| `sub_plan_features` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_plans` | `sub_plan_features_feature_code_index` |
| `sub_plans` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_products` | `sub_plans_plan_code_index, sub_plans_company_id_index` |
| `sub_price_books` | Tenant-Scoped | `id` | `undefined->tenants` | `sub_price_books_company_id_index, sub_price_books_code_index` |
| `sub_pricing_tiers` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_plans` | `sub_pricing_tiers_plan_id_tier_number_index` |
| `sub_products` | Tenant-Scoped | `id` | `undefined->tenants` | `sub_products_product_code_index, sub_products_company_id_index` |
| `sub_revenue_contracts` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_revenue_contracts_status_index, sub_revenue_contracts_contract_number_index` |
| `sub_revenue_recognition_entries` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_performance_obligations` | `sub_revenue_recognition_entries_recognition_date_index, sub_revenue_recognition_entries_gl_journal_entry_id_index` |
| `sub_revenue_schedules` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_performance_obligations` | `sub_revenue_schedules_period_date_index, sub_revenue_schedules_journal_entry_id_index` |
| `sub_subscription_items` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions, undefined->sub_plans...` | `sub_subscription_items_subscription_id_item_type_index` |
| `sub_subscription_versions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions` | `sub_subscription_versions_actor_user_id_index` |
| `sub_subscriptions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_plans` | `sub_subscriptions_workflow_instance_id_index, sub_subscriptions_subscription_number_index` |
| `sub_usage_aggregations` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscription_items` | `sub_usage_aggregations_is_billed_index` |
| `sub_usage_events` | Tenant-Scoped | `id` | `undefined->tenants, undefined->sub_subscriptions, undefined->sub_subscription_items` | `sub_usage_events_metric_code_index, sub_usage_events_is_processed_index` |
| `sub_usage_metrics` | Tenant-Scoped | `id` | `undefined->tenants` | `sub_usage_metrics_metric_code_index, sub_usage_metrics_company_id_index` |
| `subscription_items` | System / Global | `id` | `undefined->subscriptions` | `subscription_items_product_id_index` |
| `subscription_runs` | Shared Lookup | `id` | `undefined->tenants, undefined->subscriptions, undefined->invoices` | `subscription_runs_tenant_id_index` |
| `subscriptions` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts` | `subscriptions_status_next_billing_date_index` |

---

## Detailed Entity Schema & Data Dictionary

### `billing_schedule_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `billing_schedule_id` -> `billing_schedules(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `billing_schedule_items_status_index` (Unique: No)
  - `sqlite_autoindex_billing_schedule_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `billing_schedule_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for billing_schedule |
| `milestone_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `milestone_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for milestone |
| `percentage` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `target_date` | `DATE` | No | NULL | Operational entity attribute |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `invoiced_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `billing_schedules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `customer_id` -> `contacts(id)`
  - `sales_order_id` -> `sales_orders(id)`
  - `customer_agreement_id` -> `customer_agreements(id)`
- **Indexes & Constraints**:
  - `billing_schedules_status_index` (Unique: No)
  - `billing_schedules_schedule_number_index` (Unique: No)
  - `sqlite_autoindex_billing_schedules_2` (Unique: Yes)
  - `sqlite_autoindex_billing_schedules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `sales_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for sales_order |
| `customer_agreement_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for customer_agreement |
| `schedule_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `schedule_type` | `VARCHAR(255)` | No | `'milestone'` | Operational entity attribute |
| `frequency` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `billed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `remaining_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `next_billing_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_billing_runs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sub_billing_runs_status_index` (Unique: No)
  - `sub_billing_runs_run_number_index` (Unique: No)
  - `sub_billing_runs_executed_by_index` (Unique: No)
  - `sub_billing_runs_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_billing_runs_2` (Unique: Yes)
  - `sqlite_autoindex_sub_billing_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `run_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `period_start` | `DATE` | No | NULL | Operational entity attribute |
| `period_end` | `DATE` | No | NULL | Operational entity attribute |
| `execution_date` | `DATE` | No | NULL | Operational entity attribute |
| `total_subscriptions_evaluated` | `INTEGER` | No | `0` | Monetary or financial decimal quantity |
| `successful_invoices_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `failed_invoices_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `total_invoiced_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `errors_log` | `TEXT` | Yes | NULL | Operational entity attribute |
| `executed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_churn_predictions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_churn_predictions_risk_tier_index` (Unique: No)
  - `sqlite_autoindex_sub_churn_predictions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `churn_probability_score` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `risk_tier` | `VARCHAR(255)` | No | `'low'` | Operational entity attribute |
| `primary_churn_factor` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `ai_mitigation_recommendation` | `TEXT` | Yes | NULL | Operational entity attribute |
| `analyzed_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_dunning_policies`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sub_dunning_policies_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_dunning_policies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `policy_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `soft_reminder_days` | `INTEGER` | No | `3` | Operational entity attribute |
| `formal_notice_days` | `INTEGER` | No | `10` | Operational entity attribute |
| `suspension_days` | `INTEGER` | No | `25` | Operational entity attribute |
| `termination_days` | `INTEGER` | No | `45` | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_dunning_records`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_dunning_records_status_index` (Unique: No)
  - `sub_dunning_records_invoice_id_index` (Unique: No)
  - `sqlite_autoindex_sub_dunning_records_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `invoice_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for invoice |
| `dunning_level` | `INTEGER` | No | `1` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `action_taken` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `communications_log` | `TEXT` | Yes | NULL | Operational entity attribute |
| `resolved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_invoice_schedules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_invoice_schedules_status_index` (Unique: No)
  - `sub_invoice_schedules_scheduled_billing_date_index` (Unique: No)
  - `sub_invoice_schedules_invoice_id_index` (Unique: No)
  - `sub_invoice_schedules_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_invoice_schedules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `scheduled_billing_date` | `DATE` | No | NULL | Operational entity attribute |
| `service_period_start` | `DATE` | No | NULL | Operational entity attribute |
| `service_period_end` | `DATE` | No | NULL | Operational entity attribute |
| `estimated_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'scheduled'` | State machine status indicator |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_partner_commissions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_partner_commissions_status_index` (Unique: No)
  - `sub_partner_commissions_partner_id_index` (Unique: No)
  - `sub_partner_commissions_invoice_id_index` (Unique: No)
  - `sqlite_autoindex_sub_partner_commissions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `partner_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for partner |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `commission_rate` | `NUMERIC(16, 4)` | No | `0.1` | Monetary or financial decimal quantity |
| `gross_billed_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `commission_earned` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'accrued'` | State machine status indicator |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_performance_obligations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `revenue_contract_id` -> `sub_revenue_contracts(id)`
- **Indexes & Constraints**:
  - `sub_performance_obligations_status_index` (Unique: No)
  - `sub_performance_obligations_pob_code_index` (Unique: No)
  - `sub_performance_obligations_gl_revenue_account_id_index` (Unique: No)
  - `sub_performance_obligations_gl_deferred_account_id_index` (Unique: No)
  - `sqlite_autoindex_sub_performance_obligations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `revenue_contract_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for revenue_contract |
| `pob_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `standalone_selling_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `allocated_transaction_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `recognition_method` | `VARCHAR(255)` | No | `'straight_line_over_time'` | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `recognized_revenue_to_date` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `deferred_revenue_balance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `gl_revenue_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_revenue_account |
| `gl_deferred_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_deferred_account |
| `status` | `VARCHAR(255)` | No | `'in_progress'` | State machine status indicator |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_plan_features`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `plan_id` -> `sub_plans(id)`
- **Indexes & Constraints**:
  - `sub_plan_features_feature_code_index` (Unique: No)
  - `sqlite_autoindex_sub_plan_features_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `plan_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for plan |
| `feature_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `metric_type` | `VARCHAR(255)` | No | `'metered_quota'` | Operational entity attribute |
| `included_quantity` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `overage_unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_plans`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `product_id` -> `sub_products(id)`
- **Indexes & Constraints**:
  - `sub_plans_plan_code_index` (Unique: No)
  - `sub_plans_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_plans_2` (Unique: Yes)
  - `sqlite_autoindex_sub_plans_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `plan_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `billing_interval` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `interval_count` | `INTEGER` | No | `1` | Operational entity attribute |
| `pricing_model` | `VARCHAR(255)` | No | `'flat_fee'` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `setup_fee` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `base_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `trial_period_days` | `INTEGER` | No | `0` | Operational entity attribute |
| `min_commitment_cycles` | `INTEGER` | No | `1` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `terms_conditions` | `TEXT` | Yes | NULL | Operational entity attribute |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_price_books`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sub_price_books_company_id_index` (Unique: No)
  - `sub_price_books_code_index` (Unique: No)
  - `sqlite_autoindex_sub_price_books_2` (Unique: Yes)
  - `sqlite_autoindex_sub_price_books_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `is_default` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `valid_from` | `DATE` | Yes | NULL | Operational entity attribute |
| `valid_to` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `rate_overrides` | `TEXT` | Yes | NULL | Monetary or financial decimal quantity |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_pricing_tiers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `plan_id` -> `sub_plans(id)`
- **Indexes & Constraints**:
  - `sub_pricing_tiers_plan_id_tier_number_index` (Unique: No)
  - `sqlite_autoindex_sub_pricing_tiers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `plan_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for plan |
| `tier_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `from_quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `to_quantity` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `flat_fee` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_products`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sub_products_product_code_index` (Unique: No)
  - `sub_products_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_products_2` (Unique: Yes)
  - `sqlite_autoindex_sub_products_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `product_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `product_type` | `VARCHAR(255)` | No | `'saas_license'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_revenue_contracts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_revenue_contracts_status_index` (Unique: No)
  - `sub_revenue_contracts_contract_number_index` (Unique: No)
  - `sub_revenue_contracts_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_revenue_contracts_2` (Unique: Yes)
  - `sqlite_autoindex_sub_revenue_contracts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `contract_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `total_transaction_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `inception_date` | `DATE` | No | NULL | Operational entity attribute |
| `termination_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_revenue_recognition_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `performance_obligation_id` -> `sub_performance_obligations(id)`
- **Indexes & Constraints**:
  - `sub_revenue_recognition_entries_recognition_date_index` (Unique: No)
  - `sub_revenue_recognition_entries_gl_journal_entry_id_index` (Unique: No)
  - `sub_revenue_recognition_entries_company_id_index` (Unique: No)
  - `sub_revenue_recognition_entries_audit_hash_index` (Unique: No)
  - `sqlite_autoindex_sub_revenue_recognition_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `performance_obligation_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for performance_obligation |
| `recognition_date` | `DATE` | No | NULL | Operational entity attribute |
| `amount` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `gl_journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for gl_journal_entry |
| `audit_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_revenue_schedules`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `performance_obligation_id` -> `sub_performance_obligations(id)`
- **Indexes & Constraints**:
  - `sub_revenue_schedules_period_date_index` (Unique: No)
  - `sub_revenue_schedules_journal_entry_id_index` (Unique: No)
  - `sub_revenue_schedules_is_recognized_index` (Unique: No)
  - `sqlite_autoindex_sub_revenue_schedules_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `performance_obligation_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for performance_obligation |
| `period_date` | `DATE` | No | NULL | Operational entity attribute |
| `scheduled_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `recognized_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_recognized` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `recognized_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `journal_entry_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for journal_entry |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_subscription_items`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
  - `plan_id` -> `sub_plans(id)`
  - `product_id` -> `sub_products(id)`
  - `metric_id` -> `sub_usage_metrics(id)`
- **Indexes & Constraints**:
  - `sub_subscription_items_subscription_id_item_type_index` (Unique: No)
  - `sqlite_autoindex_sub_subscription_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `plan_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for plan |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `item_type` | `VARCHAR(255)` | No | `'plan'` | Operational entity attribute |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `subtotal_recurring` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `metric_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for metric |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_subscription_versions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
- **Indexes & Constraints**:
  - `sub_subscription_versions_actor_user_id_index` (Unique: No)
  - `sqlite_autoindex_sub_subscription_versions_2` (Unique: Yes)
  - `sqlite_autoindex_sub_subscription_versions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `version_number` | `INTEGER` | No | `1` | Unique business identification code or document number |
| `effective_date` | `DATE` | No | NULL | Operational entity attribute |
| `change_type` | `VARCHAR(255)` | No | `'initial'` | Operational entity attribute |
| `mrr_before` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `mrr_after` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `mrr_delta` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `proration_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `snapshot_payload` | `TEXT` | No | NULL | Operational entity attribute |
| `change_reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `actor_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for actor_user |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_subscriptions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `plan_id` -> `sub_plans(id)`
- **Indexes & Constraints**:
  - `sub_subscriptions_workflow_instance_id_index` (Unique: No)
  - `sub_subscriptions_subscription_number_index` (Unique: No)
  - `sub_subscriptions_status_index` (Unique: No)
  - `sub_subscriptions_customer_id_index` (Unique: No)
  - `sub_subscriptions_company_id_index` (Unique: No)
  - `sub_subscriptions_bank_account_id_index` (Unique: No)
  - `sqlite_autoindex_sub_subscriptions_2` (Unique: Yes)
  - `sqlite_autoindex_sub_subscriptions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `subscription_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `plan_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for plan |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `current_period_start` | `DATE` | No | NULL | Operational entity attribute |
| `current_period_end` | `DATE` | No | NULL | Operational entity attribute |
| `renewal_type` | `VARCHAR(255)` | No | `'evergreen'` | Operational entity attribute |
| `contract_term_months` | `INTEGER` | No | `12` | Operational entity attribute |
| `auto_renew` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `cancellation_notice_days` | `INTEGER` | No | `30` | Operational entity attribute |
| `cancelled_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `cancellation_reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `billing_day_of_month` | `INTEGER` | No | `1` | Operational entity attribute |
| `payment_terms_days` | `INTEGER` | No | `30` | Operational entity attribute |
| `payment_method` | `VARCHAR(255)` | No | `'sepa_direct_debit'` | Operational entity attribute |
| `bank_account_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for bank_account |
| `mrr` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `arr` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `terms` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `sub_usage_aggregations`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_item_id` -> `sub_subscription_items(id)`
- **Indexes & Constraints**:
  - `sub_usage_aggregations_is_billed_index` (Unique: No)
  - `sqlite_autoindex_sub_usage_aggregations_2` (Unique: Yes)
  - `sqlite_autoindex_sub_usage_aggregations_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription_item |
| `period_start` | `DATE` | No | NULL | Operational entity attribute |
| `period_end` | `DATE` | No | NULL | Operational entity attribute |
| `total_consumed` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `included_allowance` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `billable_overage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `billable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_billed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `billed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_usage_events`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `sub_subscriptions(id)`
  - `subscription_item_id` -> `sub_subscription_items(id)`
- **Indexes & Constraints**:
  - `sub_usage_events_metric_code_index` (Unique: No)
  - `sub_usage_events_is_processed_index` (Unique: No)
  - `sub_usage_events_idempotency_key_index` (Unique: No)
  - `sub_usage_events_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_usage_events_2` (Unique: Yes)
  - `sqlite_autoindex_sub_usage_events_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `subscription_item_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription_item |
| `metric_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `idempotency_key` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `event_timestamp` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `is_processed` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `processed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `sub_usage_metrics`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `sub_usage_metrics_metric_code_index` (Unique: No)
  - `sub_usage_metrics_company_id_index` (Unique: No)
  - `sqlite_autoindex_sub_usage_metrics_2` (Unique: Yes)
  - `sqlite_autoindex_sub_usage_metrics_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `metric_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `aggregation_type` | `VARCHAR(255)` | No | `'sum'` | Operational entity attribute |
| `unit_of_measure` | `VARCHAR(255)` | No | `'unit'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `subscription_items`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `subscription_id` -> `subscriptions(id)`
- **Indexes & Constraints**:
  - `subscription_items_product_id_index` (Unique: No)
  - `sqlite_autoindex_subscription_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percentage` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `subscription_runs`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `subscription_id` -> `subscriptions(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `subscription_runs_tenant_id_index` (Unique: No)
  - `sqlite_autoindex_subscription_runs_2` (Unique: Yes)
  - `sqlite_autoindex_subscription_runs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `subscription_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for subscription |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `period_start` | `DATE` | No | NULL | Operational entity attribute |
| `period_end` | `DATE` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | NULL | State machine status indicator |
| `error` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `subscriptions`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `subscriptions_status_next_billing_date_index` (Unique: No)
  - `sqlite_autoindex_subscriptions_2` (Unique: Yes)
  - `sqlite_autoindex_subscriptions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `subscription_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `interval` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `interval_count` | `INTEGER` | No | `1` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `next_billing_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `last_billed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `auto_renew` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `notify_days_before` | `INTEGER` | No | `30` | Operational entity attribute |
| `renewal_notified_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

