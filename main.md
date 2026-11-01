classDiagram
direction BT
class accounting_anomalies {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) journal_entry_id
   varchar(255) anomaly_type
   varchar(255) severity
   numeric(16,4) confidence_score
   text explanation
   varchar(255) status
   timestamp detected_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class accrual_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) title
   varchar(255) accrual_type
   numeric(16,4) total_amount
   date start_date
   date end_date
   integer periods_count
   numeric(16,4) monthly_amount
   varchar(36) debit_account_id
   varchar(36) credit_account_id
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class alerts {
   varchar(36) tenant_id
   varchar(255) alertable_type
   varchar(36) alertable_id
   varchar(255) created_by
   varchar(255) title
   text message
   varchar(255) severity
   timestamp starts_at
   timestamp ends_at
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class appointment_attendees {
   varchar(36) tenant_id
   varchar(36) appointment_id
   varchar(36) user_id
   varchar(255) role
   boolean is_organizer
   varchar(255) status
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class appointments {
   varchar(36) tenant_id
   varchar(255) appointment_number
   varchar(36) status_id
   varchar(36) contact_id
   varchar(36) ticket_id
   varchar(36) service_report_id
   varchar(255) title
   text description
   timestamp starts_at
   timestamp ends_at
   boolean all_day
   varchar(255) address
   numeric(16,4) latitude
   numeric(16,4) longitude
   integer estimated_travel_minutes
   integer estimated_duration_minutes
   text technician_notes
   text customer_notes
   boolean is_portal_visible
   timestamp reminder_sent_at
   timestamp confirmed_at
   timestamp cancelled_at
   varchar(255) cancellation_reason
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class approval_decisions {
   varchar(36) tenant_id
   varchar(36) workflow_instance_step_id
   varchar(36) user_id
   varchar(36) effective_user_id
   varchar(255) decision
   text comment
   varchar(255) ip_address
   varchar(255) user_agent
   text signature_payload
   timestamp decided_at
   timestamp created_at
   timestamp updated_at
   varchar(255) idempotency_key
   varchar(36) approval_token_id
   timestamp deleted_at
   varchar(36) id
}
class approval_matrix_rules {
   varchar(36) tenant_id
   varchar(36) approval_matrix_id
   varchar(255) field_name
   varchar(255) operator
   text value_string
   numeric(16,4) value_numeric
   text value_json
   timestamp created_at
   timestamp updated_at
   varchar(36) cost_center_id
   timestamp deleted_at
   varchar(36) id
}
class approval_matrix_tiers {
   varchar(36) tenant_id
   varchar(36) approval_matrix_id
   integer tier_level
   varchar(255) approver_type
   varchar(255) approver_value
   varchar(255) approval_type
   numeric(16,4) threshold_min
   numeric(16,4) threshold_max
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class approval_matrixes {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) target_entity_type
   boolean is_active
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class approval_status_translations {
   varchar(36) approval_status_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class approval_statuses {
   varchar(255) code
   varchar(255) color_badge
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class approval_tokens {
   varchar(36) tenant_id
   varchar(36) workflow_instance_step_id
   varchar(255) token_hash
   varchar(255) action_type
   varchar(36) authorized_user_id
   timestamp expires_at
   timestamp used_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class attachments {
   varchar(36) tenant_id
   varchar(255) attachable_type
   varchar(36) attachable_id
   varchar(255) uploaded_by
   varchar(255) original_name
   varchar(255) path
   varchar(255) mime_type
   integer size
   timestamp created_at
   timestamp updated_at
   varchar(255) disk
   varchar(36) id
}
class audit_logs {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) event
   varchar(255) auditable_type
   varchar(36) auditable_id
   text old_values
   text new_values
   varchar(255) ip_address
   text user_agent
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class bank_account_balances {
   varchar(36) tenant_id
   varchar(36) bank_account_id
   date balance_date
   numeric(16,4) ledger_balance
   numeric(16,4) available_balance
   varchar(255) currency
   varchar(255) source
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_account_signatories {
   varchar(36) tenant_id
   varchar(36) bank_account_id
   varchar(36) user_id
   varchar(255) authorization_level
   numeric(16,4) single_transaction_limit
   numeric(16,4) daily_transaction_limit
   date valid_from
   date valid_until
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_accounts {
   varchar(36) tenant_id
   varchar(255) bank_name
   varchar(255) iban
   varchar(255) qr_iban
   varchar(255) bic_swift
   varchar(255) currency
   numeric(16,4) current_balance
   boolean is_default
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(255) branch_name
   varchar(255) account_number
   varchar(255) account_type
   varchar(36) gl_account_id
   numeric(16,4) overdraft_limit
   numeric(16,4) credit_line_limit
   numeric(16,4) opening_balance
   numeric(16,4) available_balance
   boolean is_active
   boolean is_pool_header
   varchar(36) id
}
class bank_branches {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) bank_name
   varchar(255) branch_code
   varchar(255) branch_name
   varchar(255) bic_swift
   varchar(255) routing_number
   varchar(255) address
   varchar(255) city
   varchar(255) country
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_connections {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) protocol
   varchar(255) provider_name
   text endpoint_url
   varchar(36) partner_id
   varchar(36) host_id
   text client_certificate_encrypted
   text private_key_encrypted
   text auth_credentials_json
   integer polling_frequency_minutes
   timestamp last_poll_at
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_guarantees {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) guarantee_number
   varchar(36) issuing_bank_account_id
   varchar(255) beneficiary_name
   varchar(36) beneficiary_tax_id
   varchar(255) guarantee_type
   numeric(16,4) amount
   varchar(255) currency
   numeric(16,4) commission_rate_annual
   date issue_date
   date expiration_date
   numeric(16,4) collateral_cash_blocked
   varchar(36) project_id
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_reconciliations {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) bank_account_id
   varchar(255) reconciliation_number
   date period_start_date
   date period_end_date
   numeric(16,4) bank_statement_balance
   numeric(16,4) gl_book_balance
   numeric(16,4) difference_amount
   varchar(255) status
   varchar(255) approved_by
   timestamp approved_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bank_statement_lines {
   varchar(36) tenant_id
   varchar(36) bank_statement_id
   integer line_number
   date booking_date
   date value_date
   numeric(16,4) amount
   numeric(16,4) fee_amount
   varchar(255) direction
   varchar(255) abi_code
   varchar(255) reference
   varchar(255) qr_reference
   text description
   varchar(255) counterpart_name
   varchar(255) counterpart_iban
   boolean reconciled
   varchar(36) matched_document_id
   varchar(255) reconciliation_type
   timestamp created_at
   timestamp updated_at
   varchar(255) reconciliation_category
   varchar(255) ledger_account_code
   text reconciliation_notes
   varchar(36) company_id
   varchar(36) bank_account_id
   varchar(255) bank_reference
   varchar(255) customer_reference
   varchar(255) counterparty_name
   varchar(255) counterparty_iban
   varchar(255) counterparty_bic
   text remittance_information
   varchar(255) iso_bank_code
   varchar(255) reconciled_status
   numeric(16,4) reconciled_amount
   timestamp deleted_at
   varchar(36) id
}
class bank_statements {
   varchar(36) tenant_id
   varchar(255) source_format
   varchar(255) account_iban
   date statement_date
   numeric(16,4) opening_balance
   numeric(16,4) closing_balance
   varchar(255) currency
   integer total_entries
   varchar(255) status
   varchar(255) content_hash
   timestamp created_at
   timestamp updated_at
   varchar(36) company_id
   varchar(36) bank_account_id
   varchar(255) statement_number
   varchar(255) format
   text raw_file_storage_path
   varchar(255) file_sha256
   numeric(16,4) total_debits
   numeric(16,4) total_credits
   integer lines_count
   varchar(255) reconciliation_status
   timestamp deleted_at
   varchar(36) id
}
class bank_transactions {
   varchar(36) tenant_id
   varchar(36) bank_account_id
   date booking_date
   date value_date
   numeric(16,4) amount
   varchar(255) currency
   text description
   varchar(255) reference
   varchar(36) matched_invoice_id
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   varchar(36) company_id
   varchar(255) transaction_type
   varchar(36) gl_journal_entry_id
   varchar(36) id
}
class billable_activities {
   varchar(36) tenant_id
   varchar(36) legal_case_id
   varchar(36) user_id
   date date
   integer duration_minutes
   numeric(16,4) hourly_rate
   numeric(16,4) fee_amount
   text description
   boolean is_billed
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class billing_schedule_items {
   varchar(36) billing_schedule_id
   varchar(255) milestone_name
   varchar(36) milestone_id
   numeric(16,4) percentage
   numeric(16,4) amount
   date target_date
   varchar(36) invoice_id
   varchar(255) status
   timestamp invoiced_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class billing_schedules {
   varchar(36) tenant_id
   varchar(36) customer_id
   varchar(36) sales_order_id
   varchar(36) customer_agreement_id
   varchar(255) schedule_number
   varchar(255) schedule_type
   varchar(255) frequency
   numeric(16,4) total_amount
   numeric(16,4) billed_amount
   numeric(16,4) remaining_amount
   varchar(255) currency
   varchar(255) status
   date start_date
   date end_date
   date next_billing_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bills_of_materials {
   varchar(36) tenant_id
   varchar(36) finished_product_id
   varchar(255) version
   varchar(255) name
   text description
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class bom_items {
   varchar(36) bill_of_materials_id
   varchar(36) raw_product_id
   numeric(16,4) quantity
   numeric(16,4) scrap_percentage
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class business_calendar_holidays {
   varchar(36) tenant_id
   varchar(36) business_calendar_id
   date holiday_date
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class business_calendars {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) name
   varchar(255) timezone
   boolean work_monday
   boolean work_tuesday
   boolean work_wednesday
   boolean work_thursday
   boolean work_friday
   boolean work_saturday
   boolean work_sunday
   time work_hours_start
   time work_hours_end
   boolean is_default
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class cache {
   text value
   integer expiration
   varchar(255) key
}
class cache_locks {
   varchar(255) owner
   integer expiration
   varchar(255) key
}
class carbon_ledger {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) journal_entry_id
   varchar(255) scope
   varchar(255) emission_category
   numeric(16,4) activity_data_metric
   varchar(255) activity_uom
   numeric(16,4) emission_factor
   numeric(16,4) total_co2e_kg
   varchar(255) source_module
   date posting_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class cash_forecast_lines {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) cash_forecast_id
   date projected_date
   varchar(255) source_category
   varchar(255) flow_type
   numeric(16,4) confidence_weight
   numeric(16,4) expected_amount
   numeric(16,4) weighted_amount
   varchar(255) currency
   varchar(255) source_reference
   varchar(36) source_entity_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class cash_forecasts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) forecast_scenario_id
   varchar(255) forecast_number
   date calculation_date
   integer horizon_days
   numeric(16,4) opening_cash_balance
   numeric(16,4) projected_inflows
   numeric(16,4) projected_outflows
   numeric(16,4) closing_cash_balance
   numeric(16,4) min_liquidity_threshold
   boolean deficit_detected
   date deficit_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class cash_pools {
   varchar(36) tenant_id
   varchar(255) pool_name
   varchar(255) pool_structure
   varchar(36) header_bank_account_id
   varchar(255) currency
   varchar(255) sweeping_frequency
   numeric(16,4) target_balance_floor
   numeric(16,4) target_balance_ceiling
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class chart_of_accounts {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   varchar(255) type
   varchar(255) standard
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(36) parent_account_id
   varchar(255) account_code
   varchar(255) account_class
   varchar(255) account_type
   varchar(255) normal_balance
   varchar(255) currency
   boolean is_reconciliation_account
   varchar(255) reconciliation_type
   boolean allows_manual_posting
   boolean is_cost_center_mandatory
   varchar(36) id
}
class conformity_certificates {
   varchar(36) tenant_id
   varchar(36) construction_site_id
   varchar(255) type
   varchar(255) certificate_number
   varchar(255) inspector_name
   date certified_at
   varchar(255) document_path
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class construction_sites {
   varchar(36) tenant_id
   varchar(36) client_id
   varchar(255) code
   varchar(255) name
   varchar(255) address
   varchar(255) sia_norm_reference
   varchar(255) npk_code
   date start_date
   date estimated_end_date
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class contact_addresses {
   varchar(36) contact_id
   varchar(255) type
   varchar(255) street
   varchar(255) house_number
   varchar(255) postal_code
   varchar(255) city
   varchar(255) state_canton
   varchar(255) country
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class contact_categories {
   varchar(255) code
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class contact_category_translations {
   varchar(36) contact_category_id
   varchar(255) locale
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class contact_type_translations {
   varchar(36) contact_type_id
   varchar(255) locale
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class contact_types {
   varchar(255) code
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class contacts {
   varchar(36) tenant_id
   varchar(255) type
   varchar(255) country
   varchar(255) company_name
   varchar(255) first_name
   varchar(255) last_name
   varchar(255) email
   varchar(255) phone
   varchar(255) vat_number
   varchar(255) fiscal_code
   varchar(255) uid_number
   varchar(255) sdi_code
   varchar(255) pec
   varchar(255) iban
   varchar(255) qr_iban
   integer payment_terms_days
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) price_list_id
   varchar(36) payment_term_id
   varchar(36) id
}
class cost_centers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(36) department_id
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class countries {
   varchar(255) iso_code_2
   varchar(255) iso_code_3
   varchar(255) numeric_code
   varchar(255) phone_prefix
   boolean is_eu_member
   boolean is_sepa_member
   varchar(255) currency_code
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class country_translations {
   varchar(36) country_id
   varchar(255) locale
   varchar(255) name
   varchar(255) nationality
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class crm_accounts {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(36) parent_account_id
   varchar(255) account_number
   varchar(255) name
   varchar(255) industry
   varchar(255) tier
   varchar(255) status
   numeric(16,4) annual_revenue
   integer employee_count
   varchar(255) website
   varchar(36) owner_user_id
   numeric(16,4) customer_health_index
   varchar(255) churn_risk
   varchar(255) lifecycle_stage
   timestamp last_activity_at
   text tags
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_activities {
   varchar(36) tenant_id
   varchar(255) subject
   varchar(255) type
   varchar(255) status
   varchar(255) priority
   timestamp due_date
   timestamp completed_at
   varchar(36) assigned_user_id
   varchar(36) created_by_user_id
   varchar(255) related_type
   varchar(36) related_id
   integer duration_minutes
   varchar(255) location
   varchar(255) outcome
   text notes
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_campaign_members {
   varchar(36) tenant_id
   varchar(36) campaign_id
   varchar(36) lead_id
   varchar(36) contact_id
   varchar(255) status
   timestamp first_associated_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_campaign_types {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_campaigns {
   varchar(36) tenant_id
   varchar(36) campaign_type_id
   varchar(255) code
   varchar(255) name
   varchar(255) status
   date start_date
   date end_date
   numeric(16,4) budgeted_cost
   numeric(16,4) actual_cost
   numeric(16,4) expected_revenue
   numeric(16,4) actual_revenue
   varchar(255) utm_source
   varchar(255) utm_medium
   varchar(255) utm_campaign
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_contact_roles {
   varchar(36) tenant_id
   varchar(36) account_id
   varchar(36) contact_id
   varchar(255) role
   boolean is_primary
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_customer_health_profiles {
   varchar(36) tenant_id
   varchar(36) account_id
   numeric(16,4) activity_score
   numeric(16,4) engagement_score
   numeric(16,4) revenue_score
   numeric(16,4) risk_score
   varchar(255) churn_risk_indicator
   numeric(16,4) health_index
   timestamp last_interaction_at
   timestamp last_invoiced_at
   numeric(16,4) open_receivable_amount
   numeric(16,4) overdue_receivable_amount
   text evaluation_metrics
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_forecasts {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) period
   varchar(255) currency
   numeric(16,4) pipeline_amount
   numeric(16,4) best_case_amount
   numeric(16,4) commit_amount
   numeric(16,4) closed_amount
   numeric(16,4) weighted_amount
   numeric(16,4) quota_amount
   numeric(16,4) attainment_percent
   varchar(255) status
   varchar(36) workflow_instance_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_lead_sources {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_leads {
   varchar(36) tenant_id
   varchar(36) lead_source_id
   varchar(36) campaign_id
   varchar(36) assigned_user_id
   varchar(255) first_name
   varchar(255) last_name
   varchar(255) company_name
   varchar(255) title
   varchar(255) email
   varchar(255) phone
   varchar(255) website
   varchar(255) country
   varchar(255) status
   varchar(255) disqualification_reason
   integer score
   varchar(255) rating
   numeric(16,4) estimated_budget
   timestamp converted_at
   varchar(36) converted_contact_id
   varchar(36) converted_account_id
   varchar(36) converted_opportunity_id
   varchar(255) duplicate_hash
   text tags
   text custom_fields
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_opportunities {
   varchar(36) tenant_id
   varchar(36) account_id
   varchar(36) contact_id
   varchar(36) lead_id
   varchar(36) campaign_id
   varchar(36) stage_id
   varchar(36) owner_user_id
   varchar(255) opportunity_number
   varchar(255) name
   numeric(16,4) amount
   numeric(16,4) expected_revenue
   varchar(255) currency
   numeric(16,4) probability
   varchar(255) forecast_category
   date expected_close_date
   date actual_close_date
   varchar(255) win_loss_reason
   varchar(255) competitor
   varchar(255) status
   numeric(16,4) discount_percentage
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   varchar(36) sales_quote_id
   varchar(36) project_id
   text tags
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_opportunity_line_items {
   varchar(36) tenant_id
   varchar(36) opportunity_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) total_price
   numeric(16,4) discount_percent
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class crm_opportunity_stages {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   integer sequence
   numeric(16,4) default_probability
   boolean is_won
   boolean is_lost
   integer stale_days
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class currencies {
   varchar(255) code
   varchar(255) name
   varchar(255) symbol
   integer precision
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class currency_translations {
   varchar(36) currency_id
   varchar(255) locale
   varchar(255) name
   varchar(255) subunit_name
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class customer_agreements {
   varchar(36) tenant_id
   varchar(36) customer_id
   varchar(255) agreement_number
   varchar(255) title
   date start_date
   date end_date
   numeric(16,4) total_committed_amount
   numeric(16,4) consumed_amount
   varchar(255) currency
   varchar(255) status
   varchar(36) price_list_id
   varchar(36) payment_term_id
   text terms_and_conditions
   timestamp signed_at
   varchar(255) created_by
   varchar(255) approved_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class customer_credit_profiles {
   varchar(36) tenant_id
   varchar(36) customer_id
   numeric(16,4) credit_limit
   numeric(16,4) used_credit
   numeric(16,4) pending_orders_amount
   numeric(16,4) total_exposure
   numeric(16,4) overdue_amount
   integer overdue_invoices_count
   integer max_overdue_days
   varchar(255) credit_status
   varchar(255) risk_rating
   boolean is_credit_hold
   text hold_reason
   timestamp last_evaluated_at
   varchar(255) evaluated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class customer_groups {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   text description
   numeric(16,4) discount_percentage
   varchar(36) price_list_id
   varchar(36) payment_term_id
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class customer_ledger {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) customer_id
   varchar(36) journal_entry_id
   date posting_date
   date due_date
   numeric(16,4) original_amount
   numeric(16,4) open_amount
   varchar(255) currency
   varchar(255) status
   integer dunning_level
   date last_dunning_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class customer_ledger_entries {
   varchar(36) tenant_id
   varchar(36) customer_id
   varchar(36) invoice_id
   varchar(255) entry_number
   date entry_date
   date due_date
   varchar(255) entry_type
   varchar(255) document_reference
   numeric(16,4) debit_amount
   numeric(16,4) credit_amount
   numeric(16,4) balance_after
   varchar(255) currency
   numeric(16,4) exchange_rate
   varchar(255) status
   numeric(16,4) cleared_amount
   timestamp cleared_at
   varchar(36) gl_journal_entry_id
   text notes
   varchar(255) created_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class customs_declarations {
   varchar(36) tenant_id
   varchar(36) ddt_id
   varchar(255) declaration_number
   varchar(255) mrn_number
   varchar(255) type
   varchar(255) customs_office
   varchar(255) customs_agent
   numeric(16,4) declared_value
   varchar(255) currency
   varchar(255) incoterms
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class damage_inspections {
   varchar(36) tenant_id
   varchar(36) rental_booking_id
   varchar(255) type
   integer mileage
   varchar(255) fuel_level
   text damage_markers
   text photos
   varchar(36) inspected_by_user_id
   timestamp inspected_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class dashboard_layouts {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) name
   boolean is_default
   text widgets_layout
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class delivery_note_items {
   varchar(36) delivery_note_id
   varchar(36) sales_order_item_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(255) batch_number
   varchar(255) serial_number
   varchar(36) warehouse_location_id
   timestamp deleted_at
   varchar(36) id
}
class delivery_notes {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) ddt_number
   date date
   varchar(255) transport_reason
   varchar(255) goods_appearance
   integer packages_count
   numeric(16,4) gross_weight_kg
   varchar(255) carrier_name
   varchar(255) carrier_license_plate
   timestamp departure_time
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) sales_order_id
   text shipping_address
   varchar(255) courier
   boolean show_prices
   varchar(255) status
   varchar(36) warehouse_id
   varchar(255) shipping_status
   timestamp shipped_at
   timestamp delivered_at
   varchar(255) tracking_number
   varchar(255) created_by
   varchar(36) id
}
class discount_policies {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   varchar(255) discount_type
   numeric(16,4) value
   numeric(16,4) min_order_amount
   numeric(16,4) min_quantity
   date valid_from
   date valid_to
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class discount_policy_rules {
   varchar(36) discount_policy_id
   varchar(36) product_id
   varchar(36) customer_group_id
   numeric(16,4) min_threshold
   numeric(16,4) discount_percent
   numeric(16,4) discount_fixed_amount
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class document_emails {
   varchar(36) tenant_id
   varchar(255) emailable_type
   varchar(36) emailable_id
   varchar(36) user_id
   varchar(255) recipient
   varchar(255) subject
   text message
   varchar(255) status
   text error
   timestamp sent_at
   timestamp created_at
   timestamp updated_at
   varchar(255) attachment_name
   varchar(36) id
}
class document_events {
   varchar(36) tenant_id
   varchar(255) eventable_type
   varchar(36) eventable_id
   varchar(36) user_id
   varchar(255) event
   text payload
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class document_sequences {
   varchar(36) tenant_id
   varchar(255) document_type
   integer fiscal_year
   varchar(255) prefix
   integer last_number
   integer padding
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class document_status_translations {
   varchar(36) document_status_id
   varchar(255) locale
   varchar(255) label
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class document_statuses {
   varchar(255) scope
   varchar(255) code
   varchar(255) color_badge
   integer sort_order
   boolean is_terminal
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class eam_asset_assignments {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) asset_id
   varchar(255) assignment_number
   varchar(255) assignee_type
   varchar(36) assignee_id
   varchar(255) assignee_name
   varchar(36) department_id
   varchar(36) project_id
   varchar(36) location_id
   date assigned_at
   date expected_return_at
   date returned_at
   varchar(255) condition_on_assignment
   varchar(255) condition_on_return
   varchar(255) status
   varchar(255) assigned_by
   text notes
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_categories {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) parent_id
   varchar(255) code
   varchar(255) name
   varchar(255) asset_type
   varchar(255) depreciation_method
   integer useful_life_years
   integer useful_life_months
   numeric(16,4) statutory_rate_percent
   numeric(16,4) salvage_value_percent
   varchar(255) gl_asset_account_code
   varchar(255) gl_accumulated_depreciation_code
   varchar(255) gl_depreciation_expense_code
   varchar(255) gl_impairment_account_code
   varchar(255) gl_revaluation_reserve_code
   varchar(255) gl_disposal_gain_loss_code
   varchar(255) gl_clearing_account_code
   boolean is_depreciable
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_classes {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   varchar(255) criticality
   integer default_maintenance_interval_days
   boolean requires_custodian
   boolean requires_calibration
   boolean is_active
   text translations
   text technical_schema
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_components {
   varchar(36) tenant_id
   varchar(36) parent_asset_id
   varchar(36) component_asset_id
   varchar(255) component_code
   varchar(255) name
   varchar(255) serial_number
   numeric(16,4) cost_allocation
   integer useful_life_months
   varchar(255) condition
   varchar(255) status
   date installed_date
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_custodians {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(36) custodian_user_id
   varchar(36) assigned_by_user_id
   varchar(255) department
   timestamp assigned_at
   timestamp expected_return_at
   timestamp returned_at
   varchar(255) condition_on_checkout
   varchar(255) condition_on_return
   varchar(255) status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_disposals {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(255) disposal_number
   varchar(255) disposal_type
   date disposal_date
   numeric(16,4) asset_cost_at_disposal
   numeric(16,4) accumulated_depreciation_at_disposal
   numeric(16,4) carrying_amount_at_disposal
   numeric(16,4) proceeds_amount
   numeric(16,4) disposal_costs
   numeric(16,4) gain_loss_amount
   varchar(36) buyer_contact_id
   varchar(255) status
   varchar(36) workflow_instance_id
   varchar(36) journal_entry_id
   boolean is_locked
   text reason
   varchar(36) initiated_by_user_id
   timestamp completed_at
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_documents {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(255) document_type
   varchar(255) title
   varchar(255) document_number
   varchar(255) file_path
   date issue_date
   date expiry_date
   varchar(36) uploaded_by_user_id
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_locations {
   varchar(36) tenant_id
   varchar(36) parent_id
   varchar(36) warehouse_id
   varchar(255) code
   varchar(255) name
   varchar(255) location_type
   varchar(255) address
   varchar(255) city
   varchar(255) country
   numeric(16,4) latitude
   numeric(16,4) longitude
   boolean is_active
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_relationships {
   varchar(36) tenant_id
   varchar(36) source_asset_id
   varchar(36) target_asset_id
   varchar(255) relationship_type
   boolean is_critical_dependency
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_asset_transfers {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(255) transfer_number
   varchar(36) from_location_id
   varchar(36) to_location_id
   varchar(36) from_custodian_id
   varchar(36) to_custodian_id
   varchar(36) from_project_id
   varchar(36) to_project_id
   date transfer_date
   varchar(255) status
   varchar(36) workflow_instance_id
   boolean is_locked
   text reason
   varchar(36) initiated_by_user_id
   timestamp completed_at
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   timestamp locked_by_workflow_at
   varchar(36) id
}
class eam_asset_valuations {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(255) valuation_number
   varchar(255) valuation_type
   date valuation_date
   numeric(16,4) carrying_amount_before
   numeric(16,4) fair_value
   numeric(16,4) value_in_use
   numeric(16,4) recoverable_amount
   numeric(16,4) adjustment_amount
   numeric(16,4) revaluation_reserve_delta
   numeric(16,4) impairment_loss_amount
   numeric(16,4) carrying_amount_after
   varchar(255) status
   varchar(36) workflow_instance_id
   varchar(36) journal_entry_id
   boolean is_locked
   varchar(255) appraiser_name
   text reason
   varchar(36) created_by_user_id
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_depreciation_runs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) run_number
   varchar(255) period_code
   varchar(255) period_type
   varchar(255) ledger_type
   integer assets_processed_count
   numeric(16,4) total_depreciation_amount
   varchar(255) status
   varchar(36) fiscal_period_id
   varchar(36) executed_by_user_id
   timestamp executed_at
   timestamp posted_at
   text summary_metrics
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_depreciation_schedules {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(36) run_id
   varchar(255) ledger_type
   varchar(255) period_code
   varchar(255) period_type
   varchar(255) depreciation_method
   numeric(16,4) opening_book_value
   numeric(16,4) depreciation_amount
   numeric(16,4) closing_book_value
   numeric(16,4) accumulated_depreciation
   numeric(16,4) units_produced
   varchar(255) status
   varchar(36) journal_entry_id
   timestamp calculated_at
   timestamp posted_at
   text calculation_snapshot
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_fixed_assets {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) category_id
   varchar(36) asset_class_id
   varchar(36) location_id
   varchar(36) parent_asset_id
   varchar(36) custodian_user_id
   varchar(36) project_id
   varchar(36) supplier_id
   varchar(36) purchase_order_id
   varchar(36) purchase_receipt_id
   varchar(36) inventory_item_id
   varchar(255) asset_number
   varchar(255) barcode_tag
   varchar(255) serial_number
   varchar(255) name
   text description
   varchar(255) status
   varchar(255) condition
   varchar(255) acquisition_type
   date acquisition_date
   date capitalization_date
   date commissioning_date
   date in_service_date
   date warranty_expiry_date
   date retirement_date
   date disposal_date
   varchar(255) currency
   numeric(16,4) acquisition_cost
   numeric(16,4) capitalized_cost
   numeric(16,4) salvage_value
   numeric(16,4) depreciable_base
   numeric(16,4) accumulated_depreciation
   numeric(16,4) impairment_loss_total
   numeric(16,4) revaluation_surplus_total
   numeric(16,4) carrying_amount
   numeric(16,4) replacement_cost
   varchar(255) depreciation_method
   integer useful_life_years
   integer useful_life_months
   numeric(16,4) depreciation_rate_percent
   numeric(16,4) total_expected_units
   numeric(16,4) consumed_units
   date last_depreciation_date
   boolean is_depreciable
   boolean is_fully_depreciated
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   boolean is_locked
   text specifications
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_maintenance_activities {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) work_order_id
   varchar(36) asset_id
   varchar(255) activity_code
   varchar(255) activity_type
   varchar(255) description
   varchar(255) performed_by
   numeric(16,4) duration_hours
   numeric(16,4) labor_cost
   numeric(16,4) spare_parts_cost
   text spare_parts_consumed
   varchar(255) status
   timestamp completed_at
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_maintenance_plans {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(36) asset_class_id
   varchar(255) plan_code
   varchar(255) name
   varchar(255) maintenance_type
   integer frequency_days
   numeric(16,4) meter_interval_units
   numeric(16,4) estimated_duration_hours
   numeric(16,4) estimated_cost
   date last_executed_date
   date next_due_date
   boolean is_active
   text checklist
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class eam_maintenance_work_orders {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(36) plan_id
   varchar(255) work_order_number
   varchar(255) maintenance_type
   varchar(255) priority
   varchar(255) status
   date scheduled_date
   timestamp started_at
   timestamp completed_at
   numeric(16,4) downtime_hours
   numeric(16,4) labor_cost
   numeric(16,4) parts_cost
   numeric(16,4) external_service_cost
   numeric(16,4) total_cost
   boolean capitalize_as_upgrade
   varchar(255) condition_after_maintenance
   varchar(36) assigned_technician_id
   varchar(36) workflow_instance_id
   boolean is_locked
   text problem_description
   text resolution_notes
   text parts_consumed
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(255) approval_status
   timestamp locked_by_workflow_at
   varchar(36) id
}
class eam_project_asset_allocations {
   varchar(36) tenant_id
   varchar(36) asset_id
   varchar(36) project_id
   date allocated_from
   date allocated_to
   numeric(16,4) hourly_rate
   numeric(16,4) daily_rate
   numeric(16,4) utilized_hours
   numeric(16,4) utilized_days
   numeric(16,4) attributed_cost
   varchar(255) status
   varchar(36) allocated_by_user_id
   timestamp released_at
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class ecommerce_channels {
   varchar(36) tenant_id
   varchar(255) name
   varchar(255) driver
   varchar(255) api_url
   text credentials
   text webhook_secret
   boolean is_active
   boolean sync_stock_enabled
   boolean sync_orders_enabled
   timestamp last_sync_at
   text settings
   timestamp created_at
   timestamp updated_at
   text last_sync_summary
   varchar(36) id
}
class ecommerce_mappings {
   varchar(36) tenant_id
   varchar(36) channel_id
   varchar(255) entity_type
   varchar(36) local_id
   varchar(36) remote_id
   varchar(255) remote_sku
   text extra_data
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class ei_inbound_logs {
   varchar(36) tenant_id
   varchar(36) invoice_id
   varchar(255) provider
   varchar(255) event_type
   varchar(255) sdi_uuid
   varchar(255) fingerprint
   text payload
   varchar(255) status
   text error
   timestamp processed_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class ei_outbound_logs {
   varchar(36) tenant_id
   varchar(36) invoice_id
   varchar(255) provider
   varchar(255) action
   varchar(255) status
   varchar(255) sdi_uuid
   varchar(255) file_name
   text response
   text error
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class employee_profiles {
   varchar(36) tenant_id
   varchar(36) user_id
   boolean is_cross_border_commuter
   varchar(255) social_security_number
   numeric(16,4) swiss_cantonal_tax_rate
   varchar(255) inps_code
   varchar(255) job_title
   varchar(255) department
   date hire_date
   date termination_date
   numeric(16,4) base_salary
   varchar(255) currency
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class enterprise_audit_ledger {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) module_code
   varchar(255) action
   varchar(255) resource_type
   varchar(36) resource_id
   varchar(36) actor_user_id
   varchar(255) actor_type
   text payload_before
   text payload_after
   text diff_json
   varchar(255) ip_address
   text user_agent
   varchar(255) record_hash
   varchar(255) previous_hash
   varchar(36) id
   timestamp event_timestamp
}
class enterprise_feature_flags {
   varchar(255) feature_key
   varchar(36) tenant_id
   varchar(36) user_id
   boolean is_enabled
   text payload_config
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class esm_business_hours_calendars {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) timezone
   text weekly_schedule
   text holidays
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_change_requests {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) problem_id
   varchar(36) ticket_id
   varchar(255) change_number
   varchar(255) change_type
   varchar(255) title
   text description
   varchar(255) risk_level
   text impact_assessment
   text implementation_plan
   text rollback_plan
   timestamp scheduled_start_at
   timestamp scheduled_end_at
   timestamp implemented_at
   timestamp validated_at
   varchar(255) status
   varchar(255) cab_decision
   text cab_notes
   varchar(36) workflow_instance_id
   boolean is_locked
   text cab_reviewers
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_csat_surveys {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) ticket_id
   varchar(36) work_order_id
   varchar(36) customer_id
   integer score
   varchar(255) sentiment
   text feedback
   timestamp responded_at
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_incidents {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) ticket_id
   varchar(36) asset_id
   varchar(255) incident_number
   varchar(255) severity
   varchar(255) impact
   varchar(255) urgency
   varchar(255) priority
   varchar(255) status
   varchar(255) title
   text summary
   timestamp reported_at
   timestamp contained_at
   timestamp resolved_at
   timestamp closed_at
   text workaround
   text post_mortem_summary
   boolean post_mortem_completed
   varchar(36) workflow_instance_id
   boolean is_locked
   text timeline
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_knowledge_articles {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) category_id
   varchar(255) article_number
   varchar(255) title
   text summary
   text content
   text tags
   boolean is_published
   integer views_count
   integer helpful_count
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_parts_consumptions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) work_order_id
   varchar(36) product_id
   varchar(36) warehouse_id
   numeric(16,4) quantity
   numeric(16,4) unit_cost
   numeric(16,4) total_cost
   varchar(255) lot_number
   text serial_numbers
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_problems {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) category_id
   varchar(255) problem_number
   varchar(255) title
   text description
   varchar(255) status
   text root_cause
   text workaround
   text permanent_solution
   boolean is_known_error
   timestamp resolved_at
   timestamp closed_at
   text linked_incident_ids
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_appointments {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) appointment_number
   varchar(36) work_order_id
   varchar(36) technician_id
   varchar(36) customer_id
   timestamp start_time
   timestamp end_time
   varchar(255) status
   integer route_order
   text notes
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_categories {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_contracts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) customer_id
   varchar(36) support_plan_id
   varchar(255) contract_number
   varchar(255) title
   date start_date
   date end_date
   date renewal_date
   numeric(16,4) annual_value
   varchar(255) currency
   varchar(255) status
   boolean auto_renew
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   boolean is_locked
   text terms
   text entitlements
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_teams {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(36) lead_user_id
   varchar(36) department_id
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_technicians {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) user_id
   varchar(36) employee_id
   varchar(36) team_id
   varchar(255) technician_number
   varchar(255) first_name
   varchar(255) last_name
   varchar(255) email
   varchar(255) phone
   varchar(255) skill_level
   numeric(16,4) hourly_cost_rate
   numeric(16,4) hourly_billable_rate
   boolean is_available
   varchar(255) current_status
   text skills
   text certifications
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_service_visits {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) appointment_id
   varchar(36) work_order_id
   varchar(36) technician_id
   timestamp check_in_at
   timestamp check_out_at
   integer duration_minutes
   boolean customer_present
   boolean is_successful
   text visit_summary
   text location_check_in
   text location_check_out
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_sla_policies {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) service_category_id
   varchar(36) support_plan_id
   varchar(255) code
   varchar(255) name
   varchar(255) priority
   integer response_time_minutes
   integer resolution_time_minutes
   integer escalation_time_minutes
   boolean business_hours_only
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_support_plans {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) tier
   numeric(16,4) response_time_hours
   numeric(16,4) resolution_time_hours
   numeric(16,4) price
   varchar(255) currency
   varchar(255) billing_cycle
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_ticket_time_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) ticket_id
   varchar(36) technician_id
   date work_date
   numeric(16,4) hours
   numeric(16,4) hourly_cost
   numeric(16,4) hourly_rate
   numeric(16,4) total_cost
   numeric(16,4) total_charge
   boolean is_billable
   text description
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_tickets {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) customer_id
   varchar(36) contact_id
   varchar(36) service_contract_id
   varchar(36) asset_id
   varchar(36) project_id
   varchar(36) category_id
   varchar(255) ticket_number
   varchar(255) type
   varchar(255) priority
   varchar(255) status
   varchar(255) source
   varchar(255) subject
   text description
   varchar(36) assigned_team_id
   varchar(36) assigned_technician_id
   timestamp response_due_at
   timestamp resolution_due_at
   timestamp first_responded_at
   timestamp resolved_at
   timestamp closed_at
   boolean is_escalated
   integer escalation_level
   text resolution_summary
   text root_cause
   varchar(36) knowledge_article_id
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   boolean is_locked
   integer csat_score
   text custom_fields
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_work_order_items {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) work_order_id
   varchar(255) item_type
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_cost
   numeric(16,4) unit_price
   numeric(16,4) total_cost
   numeric(16,4) total_price
   boolean is_billable
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class esm_work_orders {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) ticket_id
   varchar(36) customer_id
   varchar(36) asset_id
   varchar(36) project_id
   varchar(36) service_team_id
   varchar(36) assigned_technician_id
   varchar(255) work_order_number
   varchar(255) title
   text description
   varchar(255) work_type
   varchar(255) priority
   varchar(255) status
   timestamp scheduled_start
   timestamp scheduled_end
   timestamp actual_start
   timestamp actual_end
   numeric(16,4) labor_cost
   numeric(16,4) material_cost
   numeric(16,4) expense_cost
   numeric(16,4) total_cost
   numeric(16,4) total_billable_amount
   varchar(255) currency
   boolean is_billable
   boolean is_invoiced
   varchar(36) invoice_id
   boolean customer_signed
   varchar(255) signed_by_name
   text signature_data
   timestamp signed_at
   varchar(36) workflow_instance_id
   boolean is_locked
   text resolution_notes
   text location
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class exchange_rates {
   varchar(255) source
   varchar(255) target
   numeric(16,4) rate
   date effective_date
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class expense_attachments {
   varchar(36) tenant_id
   varchar(36) expense_id
   varchar(36) attachment_id
   varchar(255) disk
   varchar(255) path
   varchar(255) original_name
   varchar(255) mime_type
   integer size
   boolean is_receipt
   text ocr_raw_text
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class expense_categories {
   varchar(255) code
   boolean requires_receipt
   varchar(255) suggested_account_code
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class expense_category_translations {
   varchar(36) expense_category_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class expense_items {
   varchar(36) expense_report_id
   date date
   numeric(16,4) amount
   varchar(255) currency
   varchar(255) category
   varchar(255) receipt_path
   boolean is_mileage
   numeric(16,4) kilometers
   numeric(16,4) vat_amount
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class expense_reports {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) title
   date date
   numeric(16,4) total_amount
   varchar(255) currency
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class expenses {
   varchar(36) tenant_id
   varchar(255) expense_number
   varchar(36) category_id
   date date
   numeric(16,4) amount_net
   numeric(16,4) tax_rate
   numeric(16,4) tax_amount
   numeric(16,4) amount_gross
   varchar(255) currency
   varchar(255) merchant_name
   varchar(255) payment_method
   varchar(255) status
   boolean is_billable
   boolean is_reimbursable
   text notes
   timestamp accounting_exported_at
   varchar(36) contact_id
   varchar(36) user_id
   varchar(36) project_id
   varchar(36) ticket_id
   varchar(36) service_report_id
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class failed_jobs {
   varchar(255) uuid
   varchar(255) connection
   varchar(255) queue
   text payload
   text exception
   timestamp failed_at
   varchar(36) id
}
class fee_notes {
   varchar(36) tenant_id
   varchar(36) legal_case_id
   varchar(36) client_id
   varchar(255) note_number
   date date
   numeric(16,4) taxable_fees
   numeric(16,4) cassa_previdenza_amount
   numeric(16,4) ritenuta_acconto_amount
   numeric(16,4) vat_amount
   numeric(16,4) net_payable
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class financial_closing_runs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) fiscal_period_id
   varchar(255) closing_type
   varchar(255) status
   varchar(36) closing_journal_id
   varchar(36) retained_earnings_journal_id
   numeric(16,4) net_income_amount
   varchar(255) executed_by
   timestamp executed_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class fiscal_periods {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) fiscal_year_id
   integer period_number
   varchar(255) period_name
   date start_date
   date end_date
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class fiscal_years {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) year_code
   date start_date
   date end_date
   varchar(255) status
   boolean is_locked
   timestamp closed_at
   varchar(255) closed_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class forecast_scenarios {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   boolean is_baseline
   integer collection_delay_days
   integer disbursement_acceleration_days
   numeric(16,4) sales_growth_factor
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class fx_positions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) currency
   numeric(16,4) total_cash_holdings
   numeric(16,4) open_ar_exposure
   numeric(16,4) open_ap_exposure
   numeric(16,4) net_exposure
   varchar(255) base_currency
   numeric(16,4) latest_spot_rate
   numeric(16,4) var_95_daily
   date as_of_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class fx_revaluations {
   varchar(36) tenant_id
   varchar(36) company_id
   date period_end_date
   varchar(255) currency
   numeric(16,4) foreign_amount
   numeric(16,4) book_value_base
   numeric(16,4) revalued_market_base
   numeric(16,4) unrealized_gain_loss
   varchar(36) gl_journal_entry_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class general_ledger_entries {
   varchar(36) tenant_id
   varchar(255) entry_number
   date date
   text description
   varchar(255) reference_type
   varchar(36) reference_id
   boolean is_locked
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class general_ledger_lines {
   varchar(36) general_ledger_entry_id
   varchar(36) account_id
   integer line_number
   numeric(16,4) debit
   numeric(16,4) credit
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class goods_receipt_items {
   varchar(36) goods_receipt_id
   varchar(36) purchase_order_item_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_cost
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class goods_receipts {
   varchar(36) tenant_id
   varchar(36) supplier_id
   varchar(36) purchase_order_id
   varchar(255) receipt_number
   date date
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_attendance_records {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   date work_date
   timestamp clock_in_at
   timestamp clock_out_at
   integer break_minutes
   numeric(16,4) regular_hours
   numeric(16,4) overtime_hours
   numeric(16,4) night_hours
   numeric(16,4) holiday_hours
   varchar(255) status
   varchar(255) source
   varchar(36) project_id
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_business_units {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(36) head_employee_id
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_certifications {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) course_id
   varchar(255) code
   varchar(255) name
   varchar(255) certificate_number
   varchar(255) issuing_authority
   date issue_date
   date expiry_date
   varchar(255) status
   boolean is_mandatory
   timestamp renewal_alert_sent_at
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_cost_centers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) business_unit_id
   varchar(255) code
   varchar(255) name
   varchar(255) gl_expense_account_code
   varchar(255) gl_accrual_account_code
   numeric(16,4) annual_budget
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_departments {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) parent_id
   varchar(36) business_unit_id
   varchar(36) cost_center_id
   varchar(36) manager_employee_id
   varchar(255) code
   varchar(255) name
   boolean is_active
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_employee_documents {
   varchar(36) tenant_id
   varchar(36) employee_id
   varchar(255) document_type
   varchar(255) title
   varchar(255) file_path
   date issue_date
   date expiry_date
   boolean is_confidential
   varchar(255) status
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_employee_lifecycle_events {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(255) event_type
   date effective_date
   varchar(255) from_status
   varchar(255) to_status
   varchar(36) from_department_id
   varchar(36) to_department_id
   varchar(36) from_position_id
   varchar(36) to_position_id
   varchar(36) from_job_grade_id
   varchar(36) to_job_grade_id
   numeric(16,4) from_salary
   numeric(16,4) to_salary
   text reason
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   boolean is_locked
   varchar(36) initiated_by_user_id
   varchar(36) approved_by_user_id
   text snapshot
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_employee_skills {
   varchar(36) tenant_id
   varchar(36) employee_id
   varchar(36) skill_id
   integer proficiency_level
   varchar(36) verified_by_user_id
   timestamp verified_at
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_employees {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) user_id
   varchar(255) employee_number
   varchar(255) first_name
   varchar(255) last_name
   varchar(255) full_name
   varchar(255) work_email
   varchar(255) personal_email
   varchar(255) phone
   date birth_date
   varchar(255) gender
   varchar(255) nationality
   varchar(255) tax_code
   varchar(255) social_security_number
   varchar(36) department_id
   varchar(36) team_id
   varchar(36) business_unit_id
   varchar(36) cost_center_id
   varchar(36) position_id
   varchar(36) job_grade_id
   varchar(36) manager_id
   varchar(255) employment_status
   varchar(255) employment_type
   date hire_date
   date probation_end_date
   date confirmation_date
   date termination_date
   text termination_reason
   date rehire_date
   numeric(16,4) base_annual_salary
   numeric(16,4) hourly_cost_rate
   varchar(255) currency
   numeric(16,4) fte_ratio
   varchar(255) work_schedule_code
   varchar(36) workflow_instance_id
   varchar(255) approval_status
   boolean is_locked
   text emergency_contact
   text equipment_assigned
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_employment_contracts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(255) contract_number
   varchar(255) contract_type
   varchar(255) collective_agreement
   varchar(255) job_title
   varchar(36) job_grade_id
   date start_date
   date end_date
   date probation_end_date
   numeric(16,4) weekly_hours
   numeric(16,4) fte_percentage
   numeric(16,4) base_annual_salary
   numeric(16,4) hourly_rate
   numeric(16,4) loaded_hourly_cost
   varchar(255) currency
   varchar(255) status
   boolean is_active
   varchar(36) workflow_instance_id
   boolean is_locked
   text terms
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_holiday_calendars {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) country_code
   varchar(255) region_code
   integer year
   numeric(16,4) daily_standard_hours
   text working_days
   text holidays
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_job_grades {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   integer level_rank
   numeric(16,4) min_salary
   numeric(16,4) midpoint_salary
   numeric(16,4) max_salary
   varchar(255) currency
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_leave_balances {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) leave_type_id
   integer fiscal_year
   numeric(16,4) entitlement_hours
   numeric(16,4) carryover_hours
   numeric(16,4) accrued_hours
   numeric(16,4) used_hours
   numeric(16,4) pending_hours
   numeric(16,4) available_hours
   timestamp last_accrued_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_leave_requests {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) leave_type_id
   varchar(255) request_number
   date start_date
   date end_date
   numeric(16,4) total_hours
   numeric(16,4) total_days
   varchar(255) status
   text reason
   varchar(255) medical_certificate_ref
   varchar(36) workflow_instance_id
   boolean is_locked
   varchar(36) approved_by_user_id
   timestamp approved_at
   text rejection_reason
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_leave_types {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) category
   boolean is_paid
   boolean requires_approval
   boolean requires_attachment
   numeric(16,4) annual_entitlement_hours
   varchar(255) accrual_frequency
   numeric(16,4) max_carryover_hours
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_performance_reviews {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) reviewer_employee_id
   varchar(255) review_number
   varchar(255) review_period
   varchar(255) review_type
   date review_date
   numeric(16,4) overall_rating
   numeric(16,4) goals_score
   numeric(16,4) competencies_score
   varchar(255) status
   boolean promotion_recommended
   varchar(36) recommended_job_grade_id
   numeric(16,4) recommended_salary_increase_percent
   text career_path_notes
   varchar(255) successor_readiness
   text goals
   text competencies
   text strengths
   text improvement_areas
   varchar(36) workflow_instance_id
   boolean is_locked
   timestamp completed_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_positions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) department_id
   varchar(36) job_grade_id
   varchar(36) reports_to_position_id
   varchar(255) code
   varchar(255) title
   integer headcount_budget
   boolean is_critical_role
   varchar(36) successor_employee_id
   varchar(255) readiness_level
   boolean is_active
   text translations
   text competencies_required
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_skills {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) category
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_teams {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) department_id
   varchar(36) lead_employee_id
   varchar(255) code
   varchar(255) name
   boolean is_active
   text translations
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_timesheets {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) project_id
   varchar(36) task_id
   varchar(36) cost_center_id
   varchar(255) timesheet_number
   date work_date
   numeric(16,4) regular_hours
   numeric(16,4) overtime_hours
   numeric(16,4) total_hours
   numeric(16,4) billable_hours
   numeric(16,4) hourly_cost_rate
   numeric(16,4) total_labor_cost
   varchar(255) status
   varchar(36) workflow_instance_id
   boolean is_locked
   varchar(36) approved_by_user_id
   text description
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_training_courses {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) course_code
   varchar(255) title
   varchar(255) category
   varchar(255) provider
   numeric(16,4) duration_hours
   numeric(16,4) cost_per_participant
   varchar(255) currency
   integer validity_months
   boolean is_mandatory_compliance
   boolean is_active
   text translations
   text syllabus
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class hr_training_records {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) employee_id
   varchar(36) course_id
   varchar(255) enrollment_number
   varchar(255) status
   date assigned_date
   date scheduled_date
   date completed_date
   numeric(16,4) score
   numeric(16,4) cost_amount
   varchar(255) currency
   varchar(36) workflow_instance_id
   boolean is_locked
   boolean certificate_issued
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class intercompany_funding {
   varchar(36) tenant_id
   varchar(36) cash_pool_id
   varchar(36) source_bank_account_id
   varchar(36) destination_bank_account_id
   numeric(16,4) transfer_amount
   date transfer_date
   numeric(16,4) intercompany_interest_rate
   varchar(36) gl_journal_entry_id
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class interest_schedules {
   varchar(36) tenant_id
   varchar(36) loan_agreement_id
   date period_start_date
   date period_end_date
   date due_date
   numeric(16,4) principal_due
   numeric(16,4) interest_due
   numeric(16,4) total_due
   numeric(16,4) remaining_balance
   varchar(255) status
   varchar(36) payment_line_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class inventory_adjustments {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_id
   varchar(255) adjustment_number
   varchar(255) reason
   varchar(255) status
   numeric(16,4) net_valuation_change
   boolean is_locked
   varchar(255) created_by
   varchar(255) approved_by
   timestamp approved_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class inventory_audit_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) stock_item_id
   varchar(36) movement_id
   varchar(36) actor_user_id
   varchar(255) event_type
   numeric(16,4) quantity_change
   numeric(16,4) valuation_impact
   varchar(255) source_location_desc
   varchar(255) dest_location_desc
   varchar(255) reason_code
   varchar(255) ip_address
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class inventory_count_lines {
   varchar(36) tenant_id
   varchar(36) inventory_count_session_id
   varchar(36) warehouse_bin_id
   varchar(36) stock_item_id
   varchar(36) lot_id
   numeric(16,4) system_quantity
   numeric(16,4) counted_quantity
   numeric(16,4) discrepancy_quantity
   numeric(16,4) discrepancy_valuation
   varchar(36) counted_by_user_id
   timestamp counted_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class inventory_count_sessions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_id
   varchar(255) session_number
   varchar(255) count_type
   varchar(255) status
   date scheduled_date
   boolean is_locked
   timestamp completed_at
   varchar(255) created_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class inventory_movement_type_translations {
   varchar(36) movement_type_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class inventory_movement_types {
   varchar(255) code
   varchar(255) direction
   boolean affects_cogs
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class invoice_credit_applications {
   varchar(36) tenant_id
   varchar(36) credit_note_id
   varchar(36) original_invoice_id
   numeric(16,4) applied_amount
   date application_date
   text notes
   varchar(255) applied_by
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class invoice_items {
   varchar(36) invoice_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) discount_percentage
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) sales_order_item_id
   varchar(36) delivery_note_item_id
   varchar(36) revenue_account_id
   varchar(36) tax_account_id
   varchar(36) tax_code_id
   varchar(255) uom
   text notes
   timestamp deleted_at
   varchar(36) id
}
class invoice_qr_bill_data {
   varchar(36) invoice_id
   varchar(255) qr_iban
   varchar(255) scor_reference
   text creditor_info
   text debtor_info
   text qr_bill_svg
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class invoice_sdi_metadata {
   varchar(36) invoice_id
   varchar(255) transmission_format
   varchar(255) sdi_identifier
   varchar(255) sdi_status
   varchar(255) file_name
   text xml_content
   timestamp sent_at
   timestamp delivered_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class invoice_service_reports {
   varchar(36) tenant_id
   varchar(36) invoice_id
   varchar(36) service_report_id
   boolean is_consolidated
   numeric(16,4) invoiced_net_amount
   varchar(255) created_by
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class invoices {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) invoice_type
   varchar(255) invoice_number
   date date
   date due_date
   varchar(255) currency
   numeric(16,4) exchange_rate
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   numeric(16,4) rounding_amount
   varchar(255) payment_status
   varchar(255) jurisdiction
   boolean split_payment
   boolean reverse_charge
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   integer fiscal_year
   integer sequential_number
   numeric(16,4) total_paid
   varchar(36) proforma_id
   varchar(36) sales_order_id
   varchar(36) related_invoice_id
   varchar(255) payment_method
   varchar(255) payment_terms
   varchar(255) bank_name
   varchar(255) bank_iban
   varchar(255) vat_payability
   boolean withholding_tax_enabled
   numeric(16,4) withholding_tax_percent
   numeric(16,4) withholding_tax_amount
   boolean stamp_duty_applied
   numeric(16,4) stamp_duty_amount
   boolean fund_enabled
   varchar(255) fund_type
   numeric(16,4) fund_percent
   numeric(16,4) fund_amount
   varchar(36) delivery_note_id
   varchar(36) subscription_id
   boolean is_deposit
   varchar(36) quote_id
   varchar(255) status
   numeric(16,4) subtotal
   numeric(16,4) discount_amount
   varchar(36) workflow_instance_id
   varchar(36) gl_journal_entry_id
   timestamp posted_at
   varchar(255) posted_by
   numeric(16,4) receivable_amount
   varchar(36) customer_agreement_id
   varchar(36) project_id
   varchar(36) project_milestone_id
   varchar(36) sales_rep_id
   varchar(255) created_by
   varchar(36) id
}
class job_batches {
   varchar(255) name
   integer total_jobs
   integer pending_jobs
   integer failed_jobs
   text failed_job_ids
   text options
   integer cancelled_at
   integer created_at
   integer finished_at
   varchar(36) id
}
class jobs {
   varchar(255) queue
   text payload
   integer attempts
   integer reserved_at
   integer available_at
   integer created_at
   varchar(36) id
}
class journal_batches {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) batch_number
   varchar(255) description
   varchar(255) source_module
   varchar(255) status
   numeric(16,4) total_debit
   numeric(16,4) total_credit
   varchar(255) created_by
   timestamp posted_at
   varchar(255) posted_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class journal_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) batch_id
   varchar(36) fiscal_period_id
   varchar(255) entry_number
   date posting_date
   date document_date
   varchar(255) ledger_type
   varchar(255) journal_type
   date reversal_date
   varchar(36) reversal_journal_entry_id
   text description
   varchar(255) source_document_type
   varchar(36) source_document_id
   varchar(36) workflow_instance_id
   varchar(255) status
   numeric(16,4) total_amount
   varchar(255) created_by
   timestamp posted_at
   varchar(255) posted_by
   timestamp reversed_at
   varchar(255) reversed_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class journal_lines {
   varchar(36) tenant_id
   varchar(36) journal_entry_id
   date posting_date
   integer line_number
   varchar(36) account_id
   varchar(36) cost_center_id
   varchar(36) profit_center_id
   varchar(36) project_id
   varchar(255) partner_type
   varchar(36) partner_id
   varchar(255) description
   numeric(16,4) debit_amount
   numeric(16,4) credit_amount
   varchar(255) currency
   numeric(16,4) exchange_rate
   numeric(16,4) amount_in_functional_currency
   varchar(36) vat_code_id
   numeric(16,4) vat_base_amount
   numeric(16,4) vat_tax_amount
   boolean is_cleared
   varchar(255) clearing_reference
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class leave_balances {
   varchar(36) tenant_id
   varchar(36) user_id
   integer year
   numeric(16,4) vacation_accrued
   numeric(16,4) vacation_taken
   numeric(16,4) rol_accrued
   numeric(16,4) rol_taken
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class leave_requests {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) type
   date start_date
   date end_date
   numeric(16,4) hours
   varchar(255) status
   varchar(255) medical_cert_protocol
   varchar(255) approved_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class legal_cases {
   varchar(36) tenant_id
   varchar(36) client_id
   varchar(255) case_number
   varchar(255) title
   text description
   boolean aml_kyc_completed
   varchar(255) status
   varchar(255) jurisdiction
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class letters_of_credit {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) lc_reference
   varchar(255) type
   varchar(255) issuing_bank
   varchar(255) advising_bank
   varchar(255) applicant_name
   varchar(255) beneficiary_name
   numeric(16,4) amount
   varchar(255) currency
   date issue_date
   date expiry_date
   varchar(255) incoterms
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class loan_agreements {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) loan_reference
   varchar(36) lender_bank_account_id
   varchar(255) loan_type
   numeric(16,4) principal_amount
   varchar(255) currency
   varchar(255) interest_rate_type
   numeric(16,4) nominal_rate
   numeric(16,4) spread_rate
   date origination_date
   date maturity_date
   varchar(255) repayment_structure
   text covenant_clause_json
   varchar(255) status
   varchar(36) workflow_instance_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class loan_drawdowns {
   varchar(36) tenant_id
   varchar(36) loan_agreement_id
   varchar(255) drawdown_number
   numeric(16,4) amount
   date drawdown_date
   varchar(36) destination_bank_account_id
   varchar(36) gl_journal_entry_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class lookup_categories {
   varchar(255) code
   varchar(255) name
   text description
   boolean is_system
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class lookup_item_translations {
   varchar(36) tenant_id
   varchar(36) lookup_item_id
   varchar(255) locale
   varchar(255) label
   varchar(255) short_label
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class lookup_items {
   varchar(36) tenant_id
   varchar(36) category_id
   varchar(255) code
   text metadata
   integer sort_order
   boolean is_active
   boolean is_default
   boolean is_system
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class loyalty_cards {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) card_number
   varchar(255) type
   numeric(16,4) balance
   varchar(255) currency
   varchar(255) status
   date expires_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class loyalty_transactions {
   varchar(36) tenant_id
   varchar(36) loyalty_card_id
   varchar(36) invoice_id
   varchar(255) type
   numeric(16,4) amount
   numeric(16,4) balance_after
   varchar(255) description
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class mfg_bom_components {
   varchar(36) tenant_id
   varchar(36) bom_id
   varchar(36) component_item_id
   integer sequence
   numeric(16,4) quantity_per
   varchar(255) uom
   numeric(16,4) scrap_percentage
   numeric(16,4) yield_percentage
   boolean is_phantom
   varchar(36) alternate_for_id
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_boms {
   varchar(36) tenant_id
   varchar(255) bom_number
   varchar(36) mfg_item_id
   varchar(255) name
   varchar(255) revision
   integer version
   varchar(255) bom_type
   varchar(255) status
   numeric(16,4) base_quantity
   varchar(255) uom
   date effective_from
   date effective_to
   boolean is_locked
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_engineering_change_orders {
   varchar(36) tenant_id
   varchar(255) eco_number
   varchar(255) title
   text reason
   text description
   varchar(255) change_type
   varchar(255) status
   date effective_date
   varchar(255) requested_by
   varchar(255) approved_by
   timestamp approved_at
   timestamp implemented_at
   text change_payload
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_items {
   varchar(36) tenant_id
   varchar(255) item_code
   varchar(255) name
   text description
   varchar(255) item_type
   varchar(36) stock_item_id
   varchar(36) default_bom_id
   varchar(36) default_routing_id
   varchar(255) uom
   numeric(16,4) standard_cost
   numeric(16,4) current_cost
   numeric(16,4) scrap_rate
   numeric(16,4) safety_stock
   numeric(16,4) min_lot_size
   numeric(16,4) max_lot_size
   integer lead_time_days
   boolean is_active
   text custom_attributes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_labor_time_logs {
   varchar(36) tenant_id
   varchar(36) execution_id
   varchar(36) operator_id
   timestamp start_time
   timestamp end_time
   numeric(16,4) duration_minutes
   numeric(16,4) hourly_rate
   numeric(16,4) labor_cost
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_machine_centers {
   varchar(36) tenant_id
   varchar(255) machine_code
   varchar(255) name
   varchar(36) work_center_id
   varchar(36) asset_id
   numeric(16,4) hourly_rate
   numeric(16,4) power_kw
   varchar(255) status
   timestamp last_serviced_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_machine_logs {
   varchar(36) tenant_id
   varchar(36) execution_id
   varchar(36) machine_id
   timestamp start_time
   timestamp end_time
   numeric(16,4) run_minutes
   numeric(16,4) downtime_minutes
   numeric(16,4) hourly_rate
   numeric(16,4) machine_cost
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_mrp_peggings {
   varchar(36) tenant_id
   varchar(36) planned_order_id
   varchar(255) demand_type
   varchar(36) demand_reference_id
   numeric(16,4) pegged_quantity
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_mrp_planned_orders {
   varchar(36) tenant_id
   varchar(255) planned_order_number
   varchar(36) mrp_run_id
   varchar(36) mfg_item_id
   varchar(255) order_type
   numeric(16,4) quantity
   varchar(255) uom
   date start_date
   date due_date
   varchar(255) status
   varchar(36) bom_id
   varchar(36) routing_id
   varchar(36) converted_order_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_mrp_runs {
   varchar(36) tenant_id
   varchar(255) run_number
   varchar(255) run_type
   varchar(255) status
   date horizon_start_date
   date horizon_end_date
   integer total_items_processed
   integer total_planned_orders
   integer total_shortages
   varchar(255) executed_by
   timestamp executed_at
   text error_message
   text parameters
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_mrp_shortages {
   varchar(36) tenant_id
   varchar(36) mrp_run_id
   varchar(36) mfg_item_id
   date required_date
   numeric(16,4) gross_requirement
   numeric(16,4) available_inventory
   numeric(16,4) scheduled_receipts
   numeric(16,4) safety_stock
   numeric(16,4) net_shortage
   varchar(255) recommended_action
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_operations {
   varchar(36) tenant_id
   varchar(36) routing_id
   integer sequence
   varchar(255) operation_code
   varchar(255) name
   varchar(36) work_center_id
   varchar(36) machine_center_id
   numeric(16,4) setup_time_minutes
   numeric(16,4) run_time_minutes_per_unit
   numeric(16,4) labor_time_minutes_per_unit
   numeric(16,4) queue_time_minutes
   numeric(16,4) wait_time_minutes
   numeric(16,4) teardown_time_minutes
   numeric(16,4) standard_labor_rate
   numeric(16,4) standard_machine_rate
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_production_costs {
   varchar(36) tenant_id
   varchar(36) production_order_id
   varchar(255) cost_type
   numeric(16,4) standard_cost
   numeric(16,4) actual_cost
   numeric(16,4) variance
   boolean is_posted_to_gl
   varchar(36) gl_journal_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_production_order_lines {
   varchar(36) tenant_id
   varchar(36) production_order_id
   varchar(36) mfg_item_id
   varchar(36) operation_id
   numeric(16,4) required_quantity
   numeric(16,4) allocated_quantity
   numeric(16,4) consumed_quantity
   numeric(16,4) scrapped_quantity
   varchar(255) uom
   numeric(16,4) unit_cost
   numeric(16,4) total_cost
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_production_order_operations {
   varchar(36) tenant_id
   varchar(36) production_order_id
   varchar(36) operation_id
   integer sequence
   varchar(36) work_center_id
   varchar(36) machine_center_id
   varchar(255) status
   numeric(16,4) planned_setup_minutes
   numeric(16,4) actual_setup_minutes
   numeric(16,4) planned_run_minutes
   numeric(16,4) actual_run_minutes
   numeric(16,4) completed_quantity
   numeric(16,4) scrapped_quantity
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_production_orders {
   varchar(36) tenant_id
   varchar(255) order_number
   varchar(36) mfg_item_id
   varchar(36) bom_id
   varchar(36) routing_id
   varchar(36) project_id
   varchar(255) status
   numeric(16,4) target_quantity
   numeric(16,4) completed_quantity
   numeric(16,4) scrapped_quantity
   varchar(255) uom
   date planned_start_date
   date planned_end_date
   timestamp actual_start_date
   timestamp actual_end_date
   numeric(16,4) standard_cost_total
   numeric(16,4) actual_cost_total
   numeric(16,4) variance_total
   integer lock_version
   boolean is_locked
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_production_versions {
   varchar(36) tenant_id
   varchar(255) version_code
   varchar(36) mfg_item_id
   varchar(36) bom_id
   varchar(36) routing_id
   date valid_from
   date valid_to
   numeric(16,4) min_lot_size
   numeric(16,4) max_lot_size
   boolean is_default
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_quality_characteristics {
   varchar(36) tenant_id
   varchar(36) quality_plan_id
   varchar(255) characteristic_name
   numeric(16,4) target_value
   numeric(16,4) min_tolerance
   numeric(16,4) max_tolerance
   varchar(255) uom
   varchar(255) inspection_method
   boolean is_critical
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_quality_inspections {
   varchar(36) tenant_id
   varchar(255) inspection_number
   varchar(36) quality_plan_id
   varchar(36) production_order_id
   varchar(36) operation_id
   varchar(36) inspector_id
   integer sample_size
   integer defect_count
   varchar(255) status
   timestamp inspected_at
   text notes
   text characteristic_results
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_quality_non_conformances {
   varchar(36) tenant_id
   varchar(255) nc_number
   varchar(36) quality_inspection_id
   varchar(36) production_order_id
   varchar(255) severity
   varchar(255) defect_type
   text description
   varchar(255) disposition
   text corrective_action
   varchar(255) status
   varchar(255) reported_by
   varchar(255) resolved_by
   timestamp resolved_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_quality_plans {
   varchar(36) tenant_id
   varchar(255) plan_code
   varchar(255) name
   varchar(255) inspection_type
   varchar(36) mfg_item_id
   text description
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_routings {
   varchar(36) tenant_id
   varchar(255) routing_number
   varchar(36) mfg_item_id
   varchar(255) name
   varchar(255) revision
   varchar(255) status
   boolean is_default
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_shop_floor_executions {
   varchar(36) tenant_id
   varchar(255) execution_number
   varchar(36) production_order_id
   varchar(36) production_order_operation_id
   varchar(36) work_center_id
   varchar(36) operator_id
   varchar(36) machine_id
   varchar(255) status
   numeric(16,4) good_units
   numeric(16,4) scrap_units
   timestamp started_at
   timestamp completed_at
   text downtime_reason
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_work_center_capacities {
   varchar(36) tenant_id
   varchar(36) work_center_id
   date calendar_date
   numeric(16,4) available_hours
   numeric(16,4) booked_hours
   numeric(16,4) utilization_rate
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class mfg_work_centers {
   varchar(36) tenant_id
   varchar(255) work_center_code
   varchar(255) name
   text description
   varchar(255) department_code
   numeric(16,4) capacity_hours_per_day
   numeric(16,4) efficiency_rate
   numeric(16,4) availability_rate
   numeric(16,4) hourly_cost_rate
   numeric(16,4) hourly_overhead_rate
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class notification_type_translations {
   varchar(36) notification_type_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class notification_types {
   varchar(255) code
   varchar(255) channel
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class passive_invoices {
   varchar(36) tenant_id
   varchar(36) supplier_id
   varchar(255) invoice_number
   date date
   date due_date
   numeric(16,4) total_amount
   varchar(255) currency
   varchar(36) sdi_lot_id
   boolean is_reconciled
   text xml_payload
   text qr_raw_payload
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(255) document_type
   numeric(16,4) total_net
   numeric(16,4) total_tax
   varchar(255) payment_status
   varchar(255) document_hash
   varchar(255) sdi_file_name
   numeric(16,4) total_paid
   varchar(36) id
}
class password_reset_tokens {
   varchar(255) token
   timestamp created_at
   varchar(255) email
}
class payment_approvals {
   varchar(36) tenant_id
   varchar(36) payment_batch_id
   varchar(36) approver_user_id
   integer approval_tier
   varchar(255) signature_hash
   varchar(255) ip_address
   varchar(255) decision
   text decision_reason
   timestamp approved_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class payment_batches {
   varchar(36) tenant_id
   varchar(255) format
   varchar(255) status
   varchar(255) file_path
   numeric(16,4) total_amount
   varchar(255) currency
   date execution_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(36) bank_account_id
   varchar(255) batch_reference
   varchar(255) payment_method
   integer item_count
   text xml_message_storage_path
   varchar(255) xml_sha256
   varchar(36) workflow_instance_id
   varchar(255) created_by
   varchar(36) id
}
class payment_executions {
   varchar(36) tenant_id
   varchar(36) payment_batch_id
   varchar(255) protocol
   varchar(255) bank_transmission_reference
   varchar(255) pain002_status_code
   timestamp clearing_timestamp
   text response_payload_json
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class payment_import_lines {
   varchar(36) tenant_id
   varchar(36) payment_import_id
   varchar(36) invoice_id
   varchar(36) payment_id
   varchar(255) entry_hash
   date booking_date
   numeric(16,4) amount
   varchar(255) currency
   varchar(255) reference
   varchar(255) remittance_info
   varchar(255) debtor_name
   varchar(255) status
   text note
   timestamp created_at
   timestamp updated_at
   numeric(16,4) fee_amount
   varchar(255) reference_type
   varchar(36) id
}
class payment_imports {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) file_name
   varchar(255) format
   integer total_entries
   integer matched_entries
   integer duplicate_entries
   timestamp created_at
   timestamp updated_at
   numeric(16,4) total_fees
   varchar(36) id
}
class payment_lines {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) payment_batch_id
   integer line_number
   varchar(255) recipient_type
   varchar(36) recipient_id
   varchar(255) recipient_name
   varchar(255) recipient_iban
   varchar(255) recipient_bic
   numeric(16,4) amount
   varchar(255) currency
   varchar(36) instruction_id
   varchar(36) end_to_end_id
   varchar(255) remittance_reference
   varchar(255) structured_creditor_ref
   varchar(36) invoice_id
   varchar(36) payroll_payment_id
   varchar(255) status
   date execution_date
   varchar(255) error_code
   text error_message
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class payment_method_translations {
   varchar(36) payment_method_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class payment_methods {
   varchar(255) code
   boolean is_electronic
   boolean requires_iban
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class payment_reminders {
   varchar(36) tenant_id
   varchar(36) invoice_id
   integer level
   varchar(255) channel
   varchar(255) recipient
   numeric(16,4) amount_due
   varchar(255) status
   text error
   timestamp sent_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class payment_term_installments {
   varchar(36) payment_term_id
   integer sequence
   numeric(16,4) percent
   integer days
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class payment_term_translations {
   varchar(36) payment_term_id
   varchar(255) locale
   varchar(255) name
   text invoice_clause
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class payment_terms {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   integer days
   boolean end_of_month
   numeric(16,4) discount_percent
   integer discount_days
   varchar(255) sdi_terms_code
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class payments {
   varchar(36) tenant_id
   varchar(36) invoice_id
   numeric(16,4) amount
   date paid_at
   varchar(255) payment_method
   varchar(255) reference
   text notes
   timestamp created_at
   timestamp updated_at
   varchar(255) type
   varchar(36) bank_statement_line_id
   varchar(36) id
}
class period_locks {
   varchar(36) tenant_id
   varchar(36) fiscal_period_id
   varchar(255) subledger_module
   boolean is_locked
   varchar(255) locked_by
   timestamp locked_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class personal_access_tokens {
   varchar(255) tokenable_type
   varchar(36) tokenable_id
   text name
   varchar(255) token
   text abilities
   timestamp last_used_at
   timestamp expires_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class portal_access_tokens {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) token_hash
   varchar(255) token_type
   varchar(255) scope_type
   varchar(36) scope_id
   timestamp expires_at
   timestamp last_accessed_at
   boolean is_single_use
   timestamp used_at
   timestamp revoked_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class portal_activity_logs {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(36) portal_access_token_id
   varchar(255) action
   varchar(255) subject_type
   varchar(36) subject_id
   varchar(255) ip_address
   text user_agent
   text metadata
   timestamp created_at
   varchar(36) id
}
class pos_sale_items {
   varchar(36) pos_sale_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class pos_sales {
   varchar(36) tenant_id
   varchar(36) pos_session_id
   varchar(255) receipt_number
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   varchar(255) payment_method
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) contact_id
   varchar(36) loyalty_card_id
   numeric(16,4) cash_amount
   numeric(16,4) card_amount
   varchar(255) status
   timestamp refunded_at
   varchar(36) id
}
class pos_sessions {
   varchar(36) tenant_id
   varchar(36) pos_terminal_id
   varchar(36) user_id
   timestamp opened_at
   timestamp closed_at
   numeric(16,4) opening_float
   numeric(16,4) closing_cash
   numeric(16,4) total_sales
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   numeric(16,4) expected_cash
   numeric(16,4) cash_difference
   varchar(36) id
}
class pos_terminals {
   varchar(36) tenant_id
   varchar(255) terminal_code
   varchar(255) name
   varchar(255) hardware_serial
   varchar(255) rt_serial_number
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class posting_templates {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) source_event_type
   text description
   text template_payload
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class price_list_items {
   varchar(36) price_list_id
   varchar(36) product_id
   numeric(16,4) price
   numeric(16,4) min_quantity
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class price_lists {
   varchar(36) tenant_id
   varchar(255) name
   varchar(255) currency
   boolean is_default
   boolean is_active
   date valid_from
   date valid_to
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class product_brands {
   varchar(36) tenant_id
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class product_categories {
   varchar(36) tenant_id
   varchar(36) parent_id
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class production_order_stages {
   varchar(36) production_order_id
   varchar(255) stage_name
   integer sequence
   numeric(16,4) planned_hours
   numeric(16,4) actual_hours
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class production_orders {
   varchar(36) tenant_id
   varchar(36) bill_of_materials_id
   varchar(255) order_number
   numeric(16,4) target_quantity
   numeric(16,4) produced_quantity
   date start_date
   date due_date
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class products {
   varchar(36) tenant_id
   varchar(255) sku
   varchar(255) barcode
   varchar(255) name
   text description
   varchar(255) unit_measure
   numeric(16,4) cost_price
   numeric(16,4) sale_price
   numeric(16,4) tax_rate
   varchar(255) hs_code
   boolean track_inventory
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) category_id
   varchar(36) brand_id
   varchar(36) unit_of_measure_id
   varchar(36) parent_id
   boolean is_variant
   text attributes
   numeric(16,4) min_stock
   varchar(36) id
}
class profit_centers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class progress_billings {
   varchar(36) tenant_id
   varchar(36) construction_site_id
   varchar(255) sal_number
   date period_start
   date period_end
   numeric(16,4) gross_certified_amount
   numeric(16,4) retention_amount
   numeric(16,4) net_payable_amount
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_audit_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) actor_user_id
   varchar(255) event_type
   text description
   text before_state
   text after_state
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_billing_events {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) event_type
   varchar(36) source_reference_id
   numeric(16,4) billing_amount
   varchar(255) status
   varchar(36) invoice_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_budget_approvals {
   varchar(36) tenant_id
   varchar(36) project_budget_id
   varchar(36) budget_version_id
   varchar(36) approver_user_id
   varchar(255) status
   text decision_notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_budget_lines {
   varchar(36) tenant_id
   varchar(36) project_budget_id
   varchar(36) project_phase_id
   varchar(255) cost_category
   varchar(255) description
   numeric(16,4) planned_quantity
   numeric(16,4) planned_unit_cost
   numeric(16,4) planned_total_cost
   numeric(16,4) planned_revenue_amount
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_budget_versions {
   varchar(36) tenant_id
   varchar(36) project_budget_id
   integer version_number
   text revision_reason
   text snapshot_payload
   numeric(16,4) total_revenue_budget
   numeric(16,4) total_cost_budget
   boolean is_baseline
   varchar(255) approved_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_budgets {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   integer current_version_number
   varchar(255) status
   numeric(16,4) total_revenue_budget
   numeric(16,4) total_cost_budget
   numeric(16,4) labour_budget
   numeric(16,4) material_budget
   numeric(16,4) supplier_budget
   numeric(16,4) fleet_budget
   numeric(16,4) expense_budget
   numeric(16,4) contingency_budget
   numeric(16,4) projected_margin_amount
   numeric(16,4) projected_margin_percentage
   varchar(255) approved_by
   timestamp approved_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_change_order_lines {
   varchar(36) tenant_id
   varchar(36) project_change_order_id
   varchar(255) cost_category
   varchar(255) description
   numeric(16,4) quantity_delta
   numeric(16,4) unit_cost_delta
   numeric(16,4) total_cost_delta
   numeric(16,4) revenue_delta
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_change_orders {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) order_number
   varchar(255) title
   text scope_description
   numeric(16,4) cost_impact_amount
   numeric(16,4) revenue_impact_amount
   integer schedule_impact_days
   varchar(255) status
   timestamp approved_by_client_at
   varchar(255) created_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_cost_allocations {
   varchar(36) tenant_id
   varchar(36) project_cost_entry_id
   varchar(36) project_task_id
   numeric(16,4) allocation_percentage
   numeric(16,4) allocated_amount
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_cost_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) project_phase_id
   varchar(36) project_task_id
   varchar(255) cost_source_type
   varchar(36) cost_source_id
   varchar(255) cost_category
   numeric(16,4) quantity
   varchar(255) uom
   numeric(16,4) unit_cost
   numeric(16,4) total_cost
   boolean is_billable
   boolean is_invoiced
   varchar(36) invoice_line_id
   date incurred_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_cost_snapshots {
   varchar(36) tenant_id
   varchar(36) project_id
   date snapshot_date
   numeric(16,4) total_material_cost
   numeric(16,4) total_labour_cost
   numeric(16,4) total_supplier_cost
   numeric(16,4) total_fleet_cost
   numeric(16,4) total_expense_cost
   numeric(16,4) cumulative_total_cost
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_documents {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) title
   varchar(255) document_category
   varchar(255) file_path
   varchar(255) file_name
   integer file_size_bytes
   varchar(255) mime_type
   integer version
   varchar(255) uploaded_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_financial_summaries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   numeric(16,4) total_contract_revenue
   numeric(16,4) total_invoiced_revenue
   numeric(16,4) total_recognized_revenue
   numeric(16,4) actual_material_cost
   numeric(16,4) actual_labour_cost
   numeric(16,4) actual_supplier_cost
   numeric(16,4) actual_fleet_cost
   numeric(16,4) actual_expense_cost
   numeric(16,4) total_actual_cost
   numeric(16,4) committed_po_cost
   numeric(16,4) gross_profit_amount
   numeric(16,4) gross_profit_percentage
   numeric(16,4) planned_value_pv
   numeric(16,4) earned_value_ev
   numeric(16,4) budget_at_completion_bac
   numeric(16,4) cost_performance_index_cpi
   numeric(16,4) schedule_performance_index_spi
   numeric(16,4) estimate_at_completion_eac
   numeric(16,4) estimate_to_complete_etc
   numeric(16,4) variance_at_completion_vac
   timestamp last_recalculated_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_invoice_links {
   varchar(36) tenant_id
   varchar(36) project_id
   varchar(36) invoice_id
   numeric(16,4) allocated_revenue
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_issues {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) code
   varchar(255) title
   varchar(255) priority
   varchar(255) severity
   varchar(255) status
   text description
   text resolution
   varchar(36) assigned_user_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_milestones {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) project_phase_id
   varchar(255) name
   date milestone_date
   numeric(16,4) billing_percentage
   numeric(16,4) billing_amount
   boolean is_completed
   timestamp completed_at
   boolean is_billed
   varchar(36) invoice_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_notes {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) author_user_id
   varchar(255) title
   text content
   boolean is_pinned
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_phases {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   integer sequence_order
   varchar(255) name
   varchar(255) status
   date planned_start_date
   date planned_end_date
   date actual_start_date
   date actual_end_date
   numeric(16,4) progress_percentage
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_portfolios {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   varchar(36) portfolio_manager_user_id
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_profitability_snapshots {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   date snapshot_date
   numeric(16,4) contract_revenue
   numeric(16,4) invoiced_revenue
   numeric(16,4) total_cost
   numeric(16,4) net_profit_amount
   numeric(16,4) profit_margin_pct
   numeric(16,4) cpi
   numeric(16,4) spi
   numeric(16,4) progress_percentage
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_resources {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) resource_type
   varchar(36) user_id
   varchar(36) contact_id
   varchar(255) name
   numeric(16,4) internal_hourly_cost
   numeric(16,4) billing_hourly_rate
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_revenue_recognition {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   date accounting_period_date
   numeric(16,4) cumulative_actual_cost
   numeric(16,4) estimated_total_cost_eac
   numeric(16,4) cost_completion_percentage
   numeric(16,4) cumulative_recognized_revenue
   numeric(16,4) period_revenue_adjustment
   boolean is_posted_to_gl
   timestamp posted_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_risks {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) code
   varchar(255) title
   varchar(255) category
   varchar(255) probability
   varchar(255) impact
   varchar(255) severity
   numeric(16,4) potential_cost_impact
   text mitigation_plan
   varchar(255) status
   varchar(36) owner_user_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_status_histories {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(255) from_status
   varchar(255) to_status
   text change_reason
   varchar(255) changed_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_status_translations {
   varchar(36) project_status_id
   varchar(255) locale
   varchar(255) label
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class project_statuses {
   varchar(255) code
   varchar(255) color_badge
   integer sort_order
   boolean is_terminal
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class project_task_assignments {
   varchar(36) tenant_id
   varchar(36) project_task_id
   varchar(36) user_id
   varchar(255) role_description
   numeric(16,4) allocated_hours
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_task_dependencies {
   varchar(36) tenant_id
   varchar(36) predecessor_task_id
   varchar(36) successor_task_id
   varchar(255) dependency_type
   integer lag_days
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_tasks {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) project_phase_id
   varchar(36) project_milestone_id
   varchar(36) parent_task_id
   varchar(255) task_number
   varchar(255) title
   text description
   varchar(255) status
   varchar(255) priority
   date planned_start_date
   date planned_end_date
   date actual_start_date
   date actual_end_date
   numeric(16,4) estimated_hours
   numeric(16,4) actual_hours
   numeric(16,4) progress_percentage
   boolean is_milestone_driver
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_templates {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   text default_wbs_structure
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_timesheets {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) project_id
   varchar(36) project_task_id
   varchar(36) user_id
   date work_date
   numeric(16,4) hours_worked
   numeric(16,4) overtime_hours
   boolean is_billable
   numeric(16,4) cost_rate
   numeric(16,4) charge_rate
   numeric(16,4) total_cost
   numeric(16,4) total_charge
   varchar(255) status
   varchar(255) approved_by
   timestamp approved_at
   text work_summary
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class project_variation_requests {
   varchar(36) tenant_id
   varchar(36) project_id
   varchar(255) variation_code
   varchar(255) title
   varchar(255) requested_by
   text request_details
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class projects {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) branch_id
   varchar(36) cost_center_id
   varchar(36) portfolio_id
   varchar(36) parent_project_id
   varchar(36) contact_id
   varchar(255) project_number
   varchar(255) name
   text description
   varchar(255) project_type
   varchar(255) status
   varchar(255) billing_method
   date planned_start_date
   date planned_end_date
   date actual_start_date
   date actual_end_date
   varchar(36) project_manager_user_id
   varchar(255) currency
   numeric(16,4) contract_value
   numeric(16,4) progress_percentage
   varchar(255) health_status
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_order_items {
   varchar(36) purchase_order_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   numeric(16,4) quantity_received
   varchar(36) id
}
class purchase_order_lines {
   varchar(36) tenant_id
   varchar(36) purchase_order_id
   integer line_number
   varchar(36) supplier_catalog_id
   varchar(255) description
   numeric(16,4) quantity_ordered
   numeric(16,4) quantity_received
   numeric(16,4) quantity_invoiced
   numeric(16,4) quantity_cancelled
   varchar(255) uom
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) line_net_amount
   numeric(16,4) line_tax_amount
   numeric(16,4) line_total_amount
   boolean is_closed
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_orders {
   varchar(36) tenant_id
   varchar(36) supplier_id
   varchar(36) purchase_request_id
   varchar(255) order_number
   date date
   date delivery_due_date
   varchar(255) status
   varchar(255) currency
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(36) branch_id
   varchar(36) department_id
   varchar(36) cost_center_id
   varchar(36) project_id
   varchar(36) supplier_contract_id
   varchar(36) purchase_requisition_id
   varchar(255) po_number
   varchar(255) order_type
   date expected_delivery_date
   numeric(16,4) exchange_rate
   numeric(16,4) net_amount
   numeric(16,4) tax_amount
   numeric(16,4) total_amount
   numeric(16,4) budget_committed_amount
   varchar(255) payment_terms_code
   varchar(255) incoterms
   text shipping_address
   boolean is_budget_encumbered
   boolean is_locked
   varchar(255) created_by
   varchar(255) updated_by
   varchar(36) id
}
class purchase_receipt_lines {
   varchar(36) tenant_id
   varchar(36) purchase_receipt_id
   varchar(36) purchase_order_line_id
   numeric(16,4) quantity_received
   numeric(16,4) quantity_accepted
   numeric(16,4) quantity_rejected
   varchar(255) lot_number
   varchar(255) serial_number
   varchar(36) warehouse_location_id
   text rejection_reason
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_receipts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) purchase_order_id
   varchar(255) receipt_number
   varchar(255) supplier_delivery_note_ref
   date received_date
   varchar(36) received_by_user_id
   varchar(36) warehouse_id
   varchar(255) inspection_status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_requests {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) request_number
   varchar(255) department
   varchar(255) status
   numeric(16,4) total_estimated
   date requested_date
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_requisition_lines {
   varchar(36) tenant_id
   varchar(36) purchase_requisition_id
   integer line_number
   varchar(36) supplier_catalog_id
   varchar(255) description
   numeric(16,4) quantity_requested
   varchar(255) uom
   numeric(16,4) estimated_unit_price
   numeric(16,4) estimated_total_price
   varchar(36) suggested_supplier_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_requisitions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) branch_id
   varchar(36) department_id
   varchar(36) cost_center_id
   varchar(36) project_id
   varchar(255) requisition_number
   varchar(255) title
   varchar(36) requestor_user_id
   varchar(255) urgency
   date required_by_date
   varchar(255) status
   numeric(16,4) total_estimated_amount
   varchar(255) currency
   text notes
   boolean is_locked
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_return_lines {
   varchar(36) tenant_id
   varchar(36) purchase_return_id
   varchar(36) purchase_order_line_id
   numeric(16,4) quantity_returned
   numeric(16,4) unit_price
   numeric(16,4) line_total
   text reason
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class purchase_returns {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) purchase_order_id
   varchar(36) purchase_receipt_id
   varchar(36) supplier_id
   varchar(255) return_number
   date return_date
   varchar(36) returned_by_user_id
   varchar(255) status
   numeric(16,4) total_amount
   varchar(255) reason
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class quote_items {
   varchar(36) quote_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) discount_percentage
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) tax_code_id
   numeric(16,4) cost_price
   numeric(16,4) margin_percentage
   varchar(255) uom
   text notes
   timestamp deleted_at
   varchar(36) id
}
class quotes {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) quote_number
   date date
   date valid_until
   varchar(255) currency
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   varchar(255) status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   text custom_text
   text signature_data
   timestamp signed_at
   varchar(255) signed_by
   numeric(16,4) subtotal
   numeric(16,4) discount_amount
   varchar(36) discount_policy_id
   varchar(36) price_list_id
   varchar(255) payment_terms
   varchar(255) shipping_terms
   integer revision_number
   varchar(36) workflow_instance_id
   varchar(255) created_by
   varchar(255) approved_by
   timestamp approved_at
   varchar(36) converted_to_order_id
   varchar(36) id
}
class receivable_collections {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) customer_id
   varchar(36) invoice_id
   numeric(16,4) expected_amount
   numeric(16,4) collected_amount
   date due_date
   date collection_date
   varchar(255) payment_method
   varchar(255) status
   varchar(255) aging_bucket
   integer dunning_level
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class reconciliation_items {
   varchar(36) tenant_id
   varchar(36) reconciliation_run_id
   varchar(255) item_reference
   varchar(36) gl_line_id
   varchar(36) subledger_item_id
   numeric(16,4) item_amount
   numeric(16,4) variance_amount
   boolean is_matched
   varchar(255) match_type
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class reconciliation_matches {
   varchar(36) tenant_id
   varchar(36) bank_reconciliation_id
   varchar(36) bank_statement_line_id
   varchar(255) matched_entity_type
   varchar(36) matched_entity_id
   varchar(255) match_type
   numeric(16,4) allocated_amount
   numeric(16,4) confidence_score
   varchar(36) journal_entry_id
   varchar(255) reconciled_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class reconciliation_runs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) reconciliation_type
   varchar(36) period_id
   varchar(36) account_id
   varchar(255) status
   numeric(16,4) gl_balance
   numeric(16,4) subledger_balance
   numeric(16,4) variance_amount
   varchar(255) reconciled_by
   timestamp reconciled_at
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class region_translations {
   varchar(36) region_id
   varchar(255) locale
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class regions {
   varchar(36) country_id
   varchar(255) code
   varchar(255) type
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class rental_bookings {
   varchar(36) tenant_id
   varchar(36) rental_vehicle_id
   varchar(36) client_id
   timestamp start_date
   timestamp end_date
   varchar(255) pickup_location
   varchar(255) return_location
   numeric(16,4) total_estimated
   numeric(16,4) deposit_amount
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class rental_contracts {
   varchar(36) tenant_id
   varchar(36) rental_booking_id
   varchar(255) contract_number
   text agreement_terms
   timestamp signed_at
   boolean is_closed
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class rental_vehicles {
   varchar(36) tenant_id
   varchar(36) vehicle_id
   varchar(255) category
   numeric(16,4) daily_rate
   varchar(255) fuel_type
   varchar(255) transmission
   boolean is_available
   integer current_mileage
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class resource_allocations {
   varchar(36) tenant_id
   varchar(36) project_id
   varchar(36) project_task_id
   varchar(36) resource_id
   date allocated_start_date
   date allocated_end_date
   numeric(16,4) allocated_hours_per_day
   numeric(16,4) total_allocated_hours
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class resource_calendars {
   varchar(36) tenant_id
   varchar(36) resource_id
   numeric(16,4) daily_available_hours
   date exception_date
   boolean is_available
   varchar(255) reason
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class resource_capacity_profiles {
   varchar(36) tenant_id
   varchar(36) resource_id
   numeric(16,4) weekly_capacity_hours
   numeric(16,4) maximum_overtime_hours
   numeric(16,4) efficiency_factor
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class rt_fiscal_receipts {
   varchar(36) pos_sale_id
   varchar(255) z_report_number
   varchar(255) fiscal_document_number
   varchar(36) xml_lot_id
   varchar(255) rt_status
   timestamp transmitted_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sales_commissions {
   varchar(36) tenant_id
   varchar(36) sales_representative_id
   varchar(36) sales_order_id
   varchar(36) invoice_id
   numeric(16,4) base_amount
   numeric(16,4) commission_rate
   numeric(16,4) commission_amount
   varchar(255) status
   timestamp paid_at
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sales_opportunities {
   varchar(36) tenant_id
   varchar(36) customer_id
   varchar(255) opportunity_number
   varchar(255) title
   varchar(255) stage
   numeric(16,4) estimated_amount
   varchar(255) currency
   numeric(16,4) probability_percent
   date expected_close_date
   varchar(36) assigned_to_user_id
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sales_order_holds {
   varchar(36) tenant_id
   varchar(36) sales_order_id
   varchar(255) hold_type
   varchar(255) status
   text hold_reason
   varchar(255) placed_by
   timestamp placed_at
   varchar(255) released_by
   timestamp released_at
   text release_notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sales_order_items {
   varchar(36) sales_order_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) discount_percentage
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   numeric(16,4) quantity_delivered
   varchar(36) tenant_id
   numeric(16,4) quantity_reserved
   numeric(16,4) quantity_invoiced
   varchar(36) tax_code_id
   numeric(16,4) cost_price
   varchar(255) uom
   text notes
   timestamp deleted_at
   varchar(36) id
}
class sales_orders {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(36) quote_id
   varchar(255) order_number
   date date
   date due_date
   varchar(255) currency
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   varchar(255) status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   numeric(16,4) subtotal
   numeric(16,4) discount_amount
   varchar(36) discount_policy_id
   varchar(36) price_list_id
   varchar(36) customer_agreement_id
   varchar(36) sales_rep_id
   varchar(36) workflow_instance_id
   varchar(255) credit_status
   text credit_hold_reason
   varchar(255) inventory_status
   varchar(255) fulfillment_status
   varchar(255) billing_status
   varchar(255) payment_terms
   varchar(255) shipping_method
   text shipping_address
   text billing_address
   timestamp confirmed_at
   varchar(255) created_by
   varchar(255) approved_by
   timestamp approved_at
   varchar(36) id
}
class sales_representatives {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) rep_code
   varchar(255) name
   varchar(255) email
   varchar(255) phone
   varchar(255) territory
   numeric(16,4) default_commission_rate
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sdi_uuid_links {
   varchar(36) tenant_id
   varchar(36) invoice_id
   varchar(255) provider
   varchar(255) sdi_uuid
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class service_report_lines {
   varchar(36) tenant_id
   varchar(36) service_report_id
   varchar(36) line_type_id
   varchar(36) item_id
   varchar(255) description
   numeric(16,4) quantity
   varchar(255) unit_of_measure
   numeric(16,4) unit_price
   numeric(16,4) discount_percent
   varchar(36) vat_code_id
   numeric(16,4) tax_rate
   numeric(16,4) line_net
   numeric(16,4) line_tax
   numeric(16,4) line_total
   boolean is_billable
   text notes
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class service_report_signatures {
   varchar(36) tenant_id
   varchar(36) service_report_id
   varchar(255) signer_type
   varchar(255) signer_name
   varchar(255) signer_role
   varchar(255) signer_email
   varchar(255) signature_path
   varchar(255) signature_hash
   varchar(255) ip_address
   text user_agent
   timestamp signed_at
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class service_reports {
   varchar(36) tenant_id
   varchar(255) report_number
   varchar(36) status_id
   varchar(36) contact_id
   varchar(36) ticket_id
   varchar(36) project_id
   varchar(36) technician_id
   date report_date
   time time_start
   time time_end
   numeric(16,4) total_hours
   numeric(16,4) travel_distance_km
   varchar(255) site_address
   text customer_notes
   text internal_notes
   numeric(16,4) total_net
   numeric(16,4) total_tax
   numeric(16,4) total_gross
   boolean is_portal_visible
   timestamp signed_at
   timestamp invoiced_at
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sessions {
   varchar(36) user_id
   varchar(255) ip_address
   text user_agent
   text payload
   integer last_activity
   varchar(36) id
}
class sqlite_master {
   text type
   text name
   text tbl_name
   int rootpage
   text sql
}
class stock_item_categories {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) parent_category_id
   varchar(255) code
   varchar(255) name
   varchar(255) valuation_method
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_items {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) category_id
   varchar(255) sku
   varchar(255) barcode_ean13
   varchar(255) barcode_custom
   varchar(255) name
   text description
   varchar(255) uom
   varchar(255) tracking_type
   numeric(16,4) standard_cost
   numeric(16,4) current_moving_average_cost
   numeric(16,4) weight_kg
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_lots {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) stock_item_id
   varchar(255) lot_number
   varchar(255) supplier_lot_number
   varchar(36) supplier_id
   date manufacturing_date
   date expiration_date
   boolean is_quarantined
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_movements {
   varchar(36) tenant_id
   varchar(36) product_id
   varchar(36) warehouse_id
   varchar(255) type
   numeric(16,4) quantity
   numeric(16,4) unit_cost
   varchar(255) reference_type
   varchar(36) reference_id
   text notes
   timestamp created_at
   timestamp updated_at
   varchar(36) stock_item_id
   varchar(36) source_location_id
   varchar(36) destination_location_id
   varchar(36) lot_id
   varchar(36) serial_number_id
   varchar(255) uom
   numeric(16,4) total_valuation
   varchar(255) movement_type
   varchar(255) origin_document_type
   varchar(36) origin_document_id
   varchar(36) executed_by_user_id
   timestamp executed_at
   varchar(36) company_id
   timestamp deleted_at
   varchar(36) id
}
class stock_packing_lists {
   varchar(36) tenant_id
   varchar(36) stock_pick_list_id
   varchar(255) packing_number
   integer total_packages
   numeric(16,4) total_weight_kg
   varchar(255) shipping_carrier
   varchar(255) tracking_number
   varchar(36) packed_by_user_id
   timestamp packed_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_pick_lines {
   varchar(36) tenant_id
   varchar(36) stock_pick_list_id
   varchar(36) stock_item_id
   varchar(36) warehouse_bin_id
   varchar(36) lot_id
   numeric(16,4) quantity_to_pick
   numeric(16,4) quantity_picked
   varchar(255) status
   timestamp picked_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_pick_lists {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_id
   varchar(255) pick_list_number
   varchar(36) assigned_picker_user_id
   varchar(255) status
   varchar(255) origin_document_type
   varchar(36) origin_document_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_quants {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_bin_id
   varchar(36) stock_item_id
   varchar(36) lot_id
   numeric(16,4) quantity_on_hand
   numeric(16,4) quantity_reserved
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_reorder_rules {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_id
   varchar(36) stock_item_id
   numeric(16,4) min_stock_level
   numeric(16,4) max_stock_level
   numeric(16,4) reorder_point
   numeric(16,4) economic_order_quantity
   integer lead_time_days
   varchar(36) preferred_supplier_id
   boolean auto_trigger_requisition
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_reservations {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) stock_item_id
   varchar(36) warehouse_id
   varchar(255) reserved_for_type
   varchar(36) reserved_for_id
   numeric(16,4) quantity_reserved
   varchar(255) status
   timestamp expires_at
   varchar(255) created_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_serial_numbers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) stock_item_id
   varchar(255) serial_number
   varchar(255) status
   varchar(36) current_warehouse_bin_id
   varchar(36) lot_id
   date warranty_start_date
   date warranty_end_date
   varchar(36) customer_asset_id
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class stock_valuation_snapshots {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) warehouse_id
   varchar(36) stock_item_id
   date snapshot_date
   varchar(255) valuation_method
   numeric(16,4) quantity_on_hand
   numeric(16,4) unit_cost
   numeric(16,4) total_valuation
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_billing_runs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) run_number
   date period_start
   date period_end
   date execution_date
   integer total_subscriptions_evaluated
   integer successful_invoices_count
   integer failed_invoices_count
   numeric(16,4) total_invoiced_amount
   varchar(255) status
   text errors_log
   varchar(255) executed_by
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_churn_predictions {
   varchar(36) tenant_id
   varchar(36) subscription_id
   numeric(16,4) churn_probability_score
   varchar(255) risk_tier
   varchar(255) primary_churn_factor
   text ai_mitigation_recommendation
   timestamp analyzed_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_dunning_policies {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) policy_name
   boolean is_default
   integer soft_reminder_days
   integer formal_notice_days
   integer suspension_days
   integer termination_days
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_dunning_records {
   varchar(36) tenant_id
   varchar(36) subscription_id
   varchar(36) invoice_id
   integer dunning_level
   varchar(255) status
   varchar(255) action_taken
   text communications_log
   timestamp resolved_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_invoice_schedules {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) subscription_id
   date scheduled_billing_date
   date service_period_start
   date service_period_end
   numeric(16,4) estimated_amount
   varchar(255) status
   varchar(36) invoice_id
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_partner_commissions {
   varchar(36) tenant_id
   varchar(36) partner_id
   varchar(36) subscription_id
   varchar(36) invoice_id
   numeric(16,4) commission_rate
   numeric(16,4) gross_billed_amount
   numeric(16,4) commission_earned
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_performance_obligations {
   varchar(36) tenant_id
   varchar(36) revenue_contract_id
   varchar(255) pob_code
   varchar(255) description
   numeric(16,4) standalone_selling_price
   numeric(16,4) allocated_transaction_price
   varchar(255) recognition_method
   date start_date
   date end_date
   numeric(16,4) recognized_revenue_to_date
   numeric(16,4) deferred_revenue_balance
   varchar(36) gl_revenue_account_id
   varchar(36) gl_deferred_account_id
   varchar(255) status
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_plan_features {
   varchar(36) tenant_id
   varchar(36) plan_id
   varchar(255) feature_code
   varchar(255) name
   varchar(255) metric_type
   numeric(16,4) included_quantity
   numeric(16,4) overage_unit_price
   boolean is_active
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_plans {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) product_id
   varchar(255) plan_code
   varchar(255) name
   text description
   varchar(255) billing_interval
   integer interval_count
   varchar(255) pricing_model
   varchar(255) currency
   numeric(16,4) setup_fee
   numeric(16,4) base_price
   integer trial_period_days
   integer min_commitment_cycles
   boolean is_active
   text terms_conditions
   text translations
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_price_books {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) currency
   boolean is_default
   date valid_from
   date valid_to
   boolean is_active
   text rate_overrides
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_pricing_tiers {
   varchar(36) tenant_id
   varchar(36) plan_id
   integer tier_number
   numeric(16,4) from_quantity
   numeric(16,4) to_quantity
   numeric(16,4) unit_price
   numeric(16,4) flat_fee
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_products {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) product_code
   varchar(255) name
   text description
   varchar(255) product_type
   boolean is_active
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_revenue_contracts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) contract_number
   varchar(36) subscription_id
   numeric(16,4) total_transaction_price
   varchar(255) currency
   date inception_date
   date termination_date
   varchar(255) status
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_revenue_recognition_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) performance_obligation_id
   date recognition_date
   numeric(16,4) amount
   varchar(255) currency
   varchar(36) gl_journal_entry_id
   varchar(255) audit_hash
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_revenue_schedules {
   varchar(36) tenant_id
   varchar(36) performance_obligation_id
   date period_date
   numeric(16,4) scheduled_amount
   numeric(16,4) recognized_amount
   boolean is_recognized
   timestamp recognized_at
   varchar(36) journal_entry_id
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_subscription_items {
   varchar(36) tenant_id
   varchar(36) subscription_id
   varchar(36) plan_id
   varchar(36) product_id
   varchar(255) item_type
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) discount_percentage
   numeric(16,4) subtotal_recurring
   varchar(36) metric_id
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_subscription_versions {
   varchar(36) tenant_id
   varchar(36) subscription_id
   integer version_number
   date effective_date
   varchar(255) change_type
   numeric(16,4) mrr_before
   numeric(16,4) mrr_after
   numeric(16,4) mrr_delta
   numeric(16,4) proration_amount
   text snapshot_payload
   varchar(255) change_reason
   varchar(36) actor_user_id
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_subscriptions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) subscription_number
   varchar(36) customer_id
   varchar(36) plan_id
   varchar(255) status
   date start_date
   date current_period_start
   date current_period_end
   varchar(255) renewal_type
   integer contract_term_months
   boolean auto_renew
   integer cancellation_notice_days
   timestamp cancelled_at
   varchar(255) cancellation_reason
   varchar(255) currency
   integer billing_day_of_month
   integer payment_terms_days
   varchar(255) payment_method
   varchar(36) bank_account_id
   numeric(16,4) mrr
   numeric(16,4) arr
   varchar(36) workflow_instance_id
   boolean is_locked
   text terms
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class sub_usage_aggregations {
   varchar(36) tenant_id
   varchar(36) subscription_item_id
   date period_start
   date period_end
   numeric(16,4) total_consumed
   numeric(16,4) included_allowance
   numeric(16,4) billable_overage
   numeric(16,4) unit_price
   numeric(16,4) billable_amount
   boolean is_billed
   timestamp billed_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_usage_events {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) subscription_id
   varchar(36) subscription_item_id
   varchar(255) metric_code
   varchar(255) idempotency_key
   numeric(16,4) quantity
   timestamp event_timestamp
   boolean is_processed
   timestamp processed_at
   text metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class sub_usage_metrics {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) metric_code
   varchar(255) name
   varchar(255) aggregation_type
   varchar(255) unit_of_measure
   boolean is_active
   text metadata
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class subscription_items {
   varchar(36) subscription_id
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) discount_percentage
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class subscription_runs {
   varchar(36) tenant_id
   varchar(36) subscription_id
   varchar(36) invoice_id
   date period_start
   date period_end
   varchar(255) status
   text error
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class subscriptions {
   varchar(36) tenant_id
   varchar(36) contact_id
   varchar(255) subscription_number
   varchar(255) name
   varchar(255) status
   varchar(255) interval
   integer interval_count
   varchar(255) currency
   date start_date
   date end_date
   date next_billing_date
   timestamp last_billed_at
   boolean auto_renew
   integer notify_days_before
   timestamp renewal_notified_at
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_catalogs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) supplier_id
   varchar(255) supplier_part_number
   varchar(255) internal_sku
   varchar(255) name
   text description
   varchar(255) uom
   integer lead_time_days
   numeric(16,4) minimum_order_quantity
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_categories {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_contacts {
   varchar(36) tenant_id
   varchar(36) supplier_id
   varchar(255) name
   varchar(255) email
   varchar(255) phone
   varchar(255) role
   boolean is_primary
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_contracts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) supplier_id
   varchar(255) contract_number
   varchar(255) title
   varchar(255) contract_type
   numeric(16,4) total_committed_amount
   numeric(16,4) consumed_amount
   date starts_at
   date ends_at
   varchar(255) payment_terms_code
   varchar(255) incoterms
   varchar(255) status
   boolean is_locked
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_evaluations {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) supplier_id
   date evaluation_period_start
   date evaluation_period_end
   numeric(16,4) on_time_delivery_rate
   numeric(16,4) quality_acceptance_rate
   numeric(16,4) price_competitiveness_score
   varchar(255) overall_rating
   boolean is_approved_vendor
   varchar(36) evaluator_user_id
   text comments
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_ledger {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) supplier_id
   varchar(36) journal_entry_id
   date posting_date
   date due_date
   numeric(16,4) original_amount
   numeric(16,4) open_amount
   varchar(255) currency
   varchar(255) status
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_payments {
   varchar(36) tenant_id
   varchar(36) passive_invoice_id
   numeric(16,4) amount
   date paid_at
   varchar(255) type
   varchar(255) reference
   text notes
   varchar(36) bank_statement_line_id
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class supplier_price_lists {
   varchar(36) tenant_id
   varchar(36) supplier_catalog_id
   varchar(255) currency
   numeric(16,4) min_quantity
   numeric(16,4) unit_price
   date valid_from
   date valid_to
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class supplier_scorecards {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) supplier_id
   integer year
   integer quarter
   numeric(16,4) otif_percentage
   integer defect_ppm
   numeric(16,4) cost_savings_amount
   numeric(16,4) compliance_score
   varchar(255) risk_level
   boolean is_avl_active
   text scorecard_data
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class suppliers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) contact_id
   varchar(36) supplier_category_id
   varchar(255) supplier_code
   varchar(255) company_name
   varchar(255) vat_number
   varchar(255) fiscal_code
   varchar(255) currency
   varchar(255) payment_terms_code
   varchar(255) incoterms
   varchar(255) status
   boolean is_approved_vendor
   numeric(16,4) credit_limit
   varchar(255) rating
   boolean is_locked
   text metadata
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class task_status_translations {
   varchar(36) task_status_id
   varchar(255) locale
   varchar(255) label
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class task_statuses {
   varchar(255) code
   varchar(255) color_badge
   integer sort_order
   boolean is_terminal
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class tenant_backups {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) filename
   varchar(255) disk
   integer file_size_bytes
   varchar(255) status
   text error_message
   timestamp completed_at
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class tenant_user {
   varchar(36) tenant_id
   varchar(36) user_id
   varchar(255) role
   text permissions
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class tenants {
   varchar(255) name
   varchar(255) legal_name
   varchar(255) fiscal_code
   varchar(255) vat_number
   varchar(255) uid_number
   varchar(255) country
   varchar(255) default_currency
   varchar(255) iban
   varchar(255) qr_iban
   varchar(255) sdi_code
   varchar(255) pec_email
   text settings
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   boolean is_maintenance
   varchar(36) id
}
class three_way_match_logs {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) purchase_order_id
   varchar(36) purchase_receipt_id
   varchar(36) passive_invoice_id
   varchar(255) match_status
   numeric(16,4) po_total_amount
   numeric(16,4) grn_total_amount
   numeric(16,4) invoice_total_amount
   numeric(16,4) variance_amount
   numeric(16,4) variance_percentage
   text discrepancy_details
   timestamp evaluated_at
   varchar(255) approved_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class ticket_messages {
   varchar(36) tenant_id
   varchar(36) ticket_id
   varchar(255) author_type
   varchar(36) author_id
   varchar(255) author_name
   text message
   boolean is_internal
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class tickets {
   varchar(36) tenant_id
   varchar(36) client_id
   varchar(255) subject
   text description
   varchar(255) priority
   varchar(255) status
   varchar(36) assigned_to_user_id
   timestamp sla_due_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class time_entries {
   varchar(36) tenant_id
   varchar(36) user_id
   timestamp clock_in
   timestamp clock_out
   numeric(16,4) clock_in_lat
   numeric(16,4) clock_in_lng
   boolean is_simplified_record
   integer break_minutes
   varchar(255) approved_by
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class tire_hotel_records {
   varchar(36) tenant_id
   varchar(36) vehicle_id
   varchar(255) season
   varchar(255) brand
   varchar(255) model
   varchar(255) size
   varchar(255) dot
   numeric(16,4) front_left_tread_mm
   numeric(16,4) front_right_tread_mm
   numeric(16,4) rear_left_tread_mm
   numeric(16,4) rear_right_tread_mm
   varchar(255) warehouse_shelf_location
   varchar(255) status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class transactional_inbox {
   varchar(36) tenant_id
   varchar(36) message_id
   varchar(255) event_type
   text payload_json
   timestamp received_at
   timestamp processed_at
   varchar(255) status
   varchar(36) id
}
class transactional_outbox {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) event_type
   varchar(255) aggregate_type
   varchar(36) aggregate_id
   text payload_json
   timestamp occurred_at
   timestamp processed_at
   integer retry_count
   varchar(255) status
   text error_message
   timestamp retry_after
   varchar(36) id
}
class transactional_outbox_archive {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) event_type
   varchar(255) aggregate_type
   varchar(36) aggregate_id
   text payload_json
   timestamp occurred_at
   timestamp processed_at
   integer retry_count
   varchar(255) status
   text error_message
   timestamp retry_after
   timestamp archived_at
   varchar(36) id
}
class translations {
   varchar(36) tenant_id
   varchar(255) locale
   varchar(255) group
   varchar(255) key
   text value
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class treasury_alerts {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) alert_type
   varchar(255) severity
   varchar(255) title
   text message
   numeric(16,4) threshold_value
   numeric(16,4) actual_value
   boolean is_acknowledged
   varchar(255) acknowledged_by
   timestamp acknowledged_at
   text payload_json
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class units_of_measure {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class users {
   varchar(255) name
   varchar(255) email
   varchar(255) password
   varchar(255) phone
   varchar(255) locale
   boolean is_active
   timestamp email_verified_at
   varchar(255) remember_token
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class vat_code_translations {
   varchar(36) vat_code_id
   varchar(255) locale
   varchar(255) name
   text legal_description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class vat_codes {
   varchar(255) code
   varchar(255) country_iso
   numeric(16,4) rate
   varchar(255) nature
   boolean is_split_payment
   boolean is_reverse_charge
   boolean is_active
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) description
   numeric(16,4) tax_rate_percent
   varchar(255) country
   boolean is_non_deductible
   numeric(16,4) non_deductible_percentage
   varchar(36) gl_sales_tax_account_id
   varchar(36) gl_purchase_tax_account_id
   timestamp deleted_at
   varchar(36) id
}
class vat_registers {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   varchar(255) register_type
   integer progressive_protocol_year
   integer last_protocol_number
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class vat_settlements {
   varchar(36) tenant_id
   varchar(255) period_type
   integer year
   integer period
   numeric(16,4) total_debit_vat
   numeric(16,4) total_credit_vat
   numeric(16,4) payable_amount
   boolean is_paid
   date payment_date
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(36) fiscal_period_id
   varchar(255) settlement_period
   numeric(16,4) output_vat_amount
   numeric(16,4) input_vat_amount
   numeric(16,4) prior_credit_used
   numeric(16,4) net_vat_payable
   numeric(16,4) net_vat_credit
   varchar(255) status
   varchar(36) settlement_journal_id
   varchar(255) calculated_by
   varchar(36) id
}
class vehicle_inspections {
   varchar(36) tenant_id
   varchar(36) vehicle_id
   varchar(255) type
   date scheduled_date
   date passed_date
   varchar(255) result
   varchar(255) certificate_number
   text inspector_notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class vehicles {
   varchar(36) tenant_id
   varchar(36) client_id
   varchar(255) license_plate
   varchar(255) vin_chassis
   varchar(255) make
   varchar(255) model
   integer year
   date registration_date
   integer mileage_km
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class warehouse_aisles {
   varchar(36) tenant_id
   varchar(36) warehouse_zone_id
   varchar(255) code
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class warehouse_bins {
   varchar(36) tenant_id
   varchar(36) warehouse_rack_id
   varchar(255) code
   varchar(255) barcode
   numeric(16,4) max_weight_kg
   numeric(16,4) max_volume_cbm
   boolean is_locked
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class warehouse_racks {
   varchar(36) tenant_id
   varchar(36) warehouse_aisle_id
   varchar(255) code
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class warehouse_zones {
   varchar(36) tenant_id
   varchar(36) warehouse_id
   varchar(255) code
   varchar(255) name
   varchar(255) zone_type
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class warehouses {
   varchar(36) tenant_id
   varchar(255) code
   varchar(255) name
   varchar(255) address
   boolean is_primary
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) company_id
   varchar(255) warehouse_type
   varchar(36) assigned_user_id
   boolean is_active
   varchar(36) id
}
class work_order_lines {
   varchar(36) work_order_id
   varchar(255) type
   varchar(36) product_id
   varchar(255) description
   numeric(16,4) quantity
   numeric(16,4) unit_price
   numeric(16,4) tax_rate
   numeric(16,4) line_total
   timestamp created_at
   timestamp updated_at
   varchar(36) id
}
class work_orders {
   varchar(36) tenant_id
   varchar(36) ticket_id
   varchar(36) client_id
   varchar(36) technician_user_id
   varchar(255) work_order_number
   date date
   numeric(16,4) labor_hours
   numeric(16,4) hourly_rate
   numeric(16,4) parts_total
   numeric(16,4) total_amount
   varchar(255) client_signature_path
   varchar(255) client_signed_by
   timestamp signed_at
   varchar(255) status
   text notes
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   timestamp started_at
   timestamp ended_at
   varchar(255) intervention_address
   varchar(36) invoice_id
   varchar(36) id
}
class workflow_audit_entries {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) workflow_instance_id
   varchar(36) workflow_instance_step_id
   varchar(255) event_type
   text event_payload
   varchar(36) actor_user_id
   varchar(255) ip_address
   varchar(255) user_agent
   varchar(255) hmac_signature
   timestamp created_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_comments {
   varchar(36) tenant_id
   varchar(36) workflow_instance_id
   varchar(36) workflow_instance_step_id
   varchar(36) user_id
   text comment
   boolean is_internal_only
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_definitions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) code
   varchar(255) name
   text description
   varchar(255) target_entity_type
   integer version
   varchar(255) status
   boolean is_active
   text configuration
   timestamp published_at
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_delegations {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) delegator_user_id
   varchar(36) delegate_user_id
   varchar(255) scope
   timestamp starts_at
   timestamp ends_at
   text reason
   boolean is_active
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_delivery_attempts {
   varchar(36) tenant_id
   varchar(36) subscription_id
   varchar(36) outbound_event_id
   integer attempt_number
   integer http_status
   text response_body
   integer latency_ms
   varchar(255) status
   timestamp next_retry_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_escalation_rules {
   varchar(36) tenant_id
   varchar(255) name
   integer reminder_hours
   integer escalation_hours
   varchar(255) escalate_to_type
   varchar(36) escalate_to_id
   varchar(255) auto_action
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_instance_steps {
   varchar(36) tenant_id
   varchar(36) workflow_instance_id
   varchar(36) workflow_node_id
   varchar(36) assigned_user_id
   varchar(255) assigned_role
   varchar(255) status
   integer tier_level
   timestamp due_at
   timestamp reminded_at
   timestamp escalated_at
   timestamp completed_at
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_instances {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(36) workflow_definition_id
   varchar(255) approvable_type
   varchar(36) approvable_id
   varchar(36) current_node_id
   varchar(255) status
   text context_snapshot
   timestamp started_at
   timestamp completed_at
   varchar(255) created_by
   varchar(255) updated_by
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   integer workflow_definition_version
   text workflow_definition_snapshot
   boolean locked_fiscal_document
   varchar(36) id
}
class workflow_nodes {
   varchar(36) tenant_id
   varchar(36) workflow_definition_id
   varchar(255) node_key
   varchar(255) name
   varchar(255) node_type
   varchar(255) approval_type
   varchar(255) assignee_type
   varchar(36) assignee_id
   integer timeout_hours
   varchar(36) escalation_rule_id
   text ui_metadata
   timestamp created_at
   timestamp updated_at
   varchar(36) business_calendar_id
   numeric(16,4) voting_threshold_percentage
   integer minimum_votes_required
   boolean locks_approvable_on_completion
   timestamp deleted_at
   varchar(36) id
}
class workflow_outbound_events {
   varchar(36) tenant_id
   varchar(255) event_name
   text event_payload
   timestamp created_at
   timestamp deleted_at
   varchar(36) id
}
class workflow_state_translations {
   varchar(36) workflow_state_id
   varchar(255) locale
   varchar(255) name
   text description
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class workflow_states {
   varchar(255) scope
   varchar(255) code
   boolean is_initial
   boolean is_final
   timestamp created_at
   timestamp updated_at
   varchar(36) tenant_id
   varchar(36) id
}
class workflow_transitions {
   varchar(36) tenant_id
   varchar(36) workflow_definition_id
   varchar(36) from_node_id
   varchar(36) to_node_id
   varchar(255) action_trigger
   text condition_rules
   integer priority
   timestamp created_at
   timestamp updated_at
   varchar(255) idempotency_key
   timestamp deleted_at
   varchar(36) id
}
class workflow_webhook_subscriptions {
   varchar(36) tenant_id
   varchar(36) company_id
   varchar(255) name
   varchar(255) target_url
   varchar(255) secret_key
   text subscribed_events
   boolean is_active
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}
class working_capital_metrics {
   varchar(36) tenant_id
   varchar(36) company_id
   date metric_date
   numeric(16,4) accounts_receivable_total
   numeric(16,4) accounts_payable_total
   numeric(16,4) inventory_valuation_total
   numeric(16,4) trailing_12m_revenue
   numeric(16,4) trailing_12m_cogs
   numeric(16,4) dso_days
   numeric(16,4) dpo_days
   numeric(16,4) dio_days
   numeric(16,4) cash_conversion_cycle_days
   numeric(16,4) current_ratio
   numeric(16,4) quick_ratio
   timestamp created_at
   timestamp updated_at
   timestamp deleted_at
   varchar(36) id
}

accounting_anomalies  -->  journal_entries : journal_entry_id:id
accounting_anomalies  -->  tenants : tenant_id:id
accrual_entries  -->  chart_of_accounts : debit_account_id:id
accrual_entries  -->  chart_of_accounts : credit_account_id:id
accrual_entries  -->  tenants : tenant_id:id
alerts  -->  tenants : tenant_id:id
appointment_attendees  -->  appointments : appointment_id:id
appointment_attendees  -->  tenants : tenant_id:id
appointment_attendees  -->  users : updated_by:id
appointment_attendees  -->  users : created_by:id
appointment_attendees  -->  users : user_id:id
appointments  -->  contacts : contact_id:id
appointments  -->  lookup_items : status_id:id
appointments  -->  service_reports : service_report_id:id
appointments  -->  tenants : tenant_id:id
appointments  -->  tickets : ticket_id:id
appointments  -->  users : created_by:id
appointments  -->  users : updated_by:id
approval_decisions  -->  approval_tokens : approval_token_id:id
approval_decisions  -->  tenants : tenant_id:id
approval_decisions  -->  users : user_id:id
approval_decisions  -->  workflow_instance_steps : workflow_instance_step_id:id
approval_matrix_rules  -->  approval_matrixes : approval_matrix_id:id
approval_matrix_rules  -->  cost_centers : cost_center_id:id
approval_matrix_rules  -->  tenants : tenant_id:id
approval_matrix_tiers  -->  approval_matrixes : approval_matrix_id:id
approval_matrix_tiers  -->  tenants : tenant_id:id
approval_matrixes  -->  tenants : tenant_id:id
approval_status_translations  -->  approval_statuses : approval_status_id:id
approval_status_translations  -->  tenants : tenant_id:id
approval_statuses  -->  tenants : tenant_id:id
approval_tokens  -->  tenants : tenant_id:id
approval_tokens  -->  workflow_instance_steps : workflow_instance_step_id:id
attachments  -->  tenants : tenant_id:id
audit_logs  -->  tenants : tenant_id:id
audit_logs  -->  users : user_id:id
bank_account_balances  -->  bank_accounts : bank_account_id:id
bank_account_balances  -->  tenants : tenant_id:id
bank_account_signatories  -->  bank_accounts : bank_account_id:id
bank_account_signatories  -->  tenants : tenant_id:id
bank_account_signatories  -->  users : user_id:id
bank_accounts  -->  tenants : tenant_id:id
bank_branches  -->  tenants : tenant_id:id
bank_connections  -->  tenants : tenant_id:id
bank_guarantees  -->  projects : project_id:id
bank_guarantees  -->  tenants : tenant_id:id
bank_reconciliations  -->  bank_accounts : bank_account_id:id
bank_reconciliations  -->  tenants : tenant_id:id
bank_statement_lines  -->  bank_accounts : bank_account_id:id
bank_statement_lines  -->  bank_statements : bank_statement_id:id
bank_statement_lines  -->  tenants : tenant_id:id
bank_statements  -->  bank_accounts : bank_account_id:id
bank_statements  -->  tenants : tenant_id:id
bank_transactions  -->  bank_accounts : bank_account_id:id
bank_transactions  -->  tenants : tenant_id:id
billable_activities  -->  legal_cases : legal_case_id:id
billable_activities  -->  tenants : tenant_id:id
billable_activities  -->  users : user_id:id
billing_schedule_items  -->  billing_schedules : billing_schedule_id:id
billing_schedule_items  -->  invoices : invoice_id:id
billing_schedules  -->  contacts : customer_id:id
billing_schedules  -->  customer_agreements : customer_agreement_id:id
billing_schedules  -->  sales_orders : sales_order_id:id
billing_schedules  -->  tenants : tenant_id:id
bills_of_materials  -->  products : finished_product_id:id
bills_of_materials  -->  tenants : tenant_id:id
bom_items  -->  bills_of_materials : bill_of_materials_id:id
bom_items  -->  products : raw_product_id:id
business_calendar_holidays  -->  business_calendars : business_calendar_id:id
business_calendar_holidays  -->  tenants : tenant_id:id
business_calendars  -->  tenants : tenant_id:id
carbon_ledger  -->  journal_entries : journal_entry_id:id
carbon_ledger  -->  tenants : tenant_id:id
cash_forecast_lines  -->  cash_forecasts : cash_forecast_id:id
cash_forecast_lines  -->  tenants : tenant_id:id
cash_forecasts  -->  forecast_scenarios : forecast_scenario_id:id
cash_forecasts  -->  tenants : tenant_id:id
cash_pools  -->  tenants : tenant_id:id
chart_of_accounts  -->  tenants : tenant_id:id
conformity_certificates  -->  construction_sites : construction_site_id:id
conformity_certificates  -->  tenants : tenant_id:id
construction_sites  -->  contacts : client_id:id
construction_sites  -->  tenants : tenant_id:id
contact_addresses  -->  contacts : contact_id:id
contact_categories  -->  tenants : tenant_id:id
contact_category_translations  -->  contact_categories : contact_category_id:id
contact_category_translations  -->  tenants : tenant_id:id
contact_type_translations  -->  contact_types : contact_type_id:id
contact_type_translations  -->  tenants : tenant_id:id
contact_types  -->  tenants : tenant_id:id
contacts  -->  payment_terms : payment_term_id:id
contacts  -->  price_lists : price_list_id:id
contacts  -->  tenants : tenant_id:id
cost_centers  -->  tenants : tenant_id:id
countries  -->  tenants : tenant_id:id
country_translations  -->  countries : country_id:id
country_translations  -->  tenants : tenant_id:id
crm_accounts  -->  contacts : contact_id:id
crm_accounts  -->  crm_accounts : parent_account_id:id
crm_accounts  -->  tenants : tenant_id:id
crm_activities  -->  tenants : tenant_id:id
crm_campaign_members  -->  contacts : contact_id:id
crm_campaign_members  -->  crm_campaigns : campaign_id:id
crm_campaign_members  -->  crm_leads : lead_id:id
crm_campaign_members  -->  tenants : tenant_id:id
crm_campaign_types  -->  tenants : tenant_id:id
crm_campaigns  -->  crm_campaign_types : campaign_type_id:id
crm_campaigns  -->  tenants : tenant_id:id
crm_contact_roles  -->  contacts : contact_id:id
crm_contact_roles  -->  crm_accounts : account_id:id
crm_contact_roles  -->  tenants : tenant_id:id
crm_customer_health_profiles  -->  crm_accounts : account_id:id
crm_customer_health_profiles  -->  tenants : tenant_id:id
crm_forecasts  -->  tenants : tenant_id:id
crm_forecasts  -->  users : user_id:id
crm_forecasts  -->  workflow_instances : workflow_instance_id:id
crm_lead_sources  -->  tenants : tenant_id:id
crm_leads  -->  contacts : converted_contact_id:id
crm_leads  -->  crm_accounts : converted_account_id:id
crm_leads  -->  crm_campaigns : campaign_id:id
crm_leads  -->  crm_lead_sources : lead_source_id:id
crm_leads  -->  tenants : tenant_id:id
crm_opportunities  -->  contacts : contact_id:id
crm_opportunities  -->  crm_accounts : account_id:id
crm_opportunities  -->  crm_campaigns : campaign_id:id
crm_opportunities  -->  crm_leads : lead_id:id
crm_opportunities  -->  crm_opportunity_stages : stage_id:id
crm_opportunities  -->  projects : project_id:id
crm_opportunities  -->  quotes : sales_quote_id:id
crm_opportunities  -->  tenants : tenant_id:id
crm_opportunities  -->  workflow_instances : workflow_instance_id:id
crm_opportunity_line_items  -->  crm_opportunities : opportunity_id:id
crm_opportunity_line_items  -->  products : product_id:id
crm_opportunity_line_items  -->  tenants : tenant_id:id
crm_opportunity_stages  -->  tenants : tenant_id:id
currencies  -->  tenants : tenant_id:id
currency_translations  -->  currencies : currency_id:id
currency_translations  -->  tenants : tenant_id:id
customer_agreements  -->  contacts : customer_id:id
customer_agreements  -->  payment_terms : payment_term_id:id
customer_agreements  -->  price_lists : price_list_id:id
customer_agreements  -->  tenants : tenant_id:id
customer_credit_profiles  -->  contacts : customer_id:id
customer_credit_profiles  -->  tenants : tenant_id:id
customer_groups  -->  payment_terms : payment_term_id:id
customer_groups  -->  price_lists : price_list_id:id
customer_groups  -->  tenants : tenant_id:id
customer_ledger  -->  journal_entries : journal_entry_id:id
customer_ledger  -->  tenants : tenant_id:id
customer_ledger_entries  -->  contacts : customer_id:id
customer_ledger_entries  -->  invoices : invoice_id:id
customer_ledger_entries  -->  tenants : tenant_id:id
customs_declarations  -->  delivery_notes : ddt_id:id
customs_declarations  -->  tenants : tenant_id:id
damage_inspections  -->  rental_bookings : rental_booking_id:id
damage_inspections  -->  tenants : tenant_id:id
damage_inspections  -->  users : inspected_by_user_id:id
dashboard_layouts  -->  tenants : tenant_id:id
dashboard_layouts  -->  users : user_id:id
delivery_note_items  -->  delivery_notes : delivery_note_id:id
delivery_note_items  -->  products : product_id:id
delivery_note_items  -->  sales_order_items : sales_order_item_id:id
delivery_note_items  -->  tenants : tenant_id:id
delivery_notes  -->  contacts : contact_id:id
delivery_notes  -->  sales_orders : sales_order_id:id
delivery_notes  -->  tenants : tenant_id:id
delivery_notes  -->  warehouses : warehouse_id:id
discount_policies  -->  tenants : tenant_id:id
discount_policy_rules  -->  customer_groups : customer_group_id:id
discount_policy_rules  -->  discount_policies : discount_policy_id:id
discount_policy_rules  -->  products : product_id:id
document_emails  -->  tenants : tenant_id:id
document_emails  -->  users : user_id:id
document_events  -->  tenants : tenant_id:id
document_events  -->  users : user_id:id
document_sequences  -->  tenants : tenant_id:id
document_status_translations  -->  document_statuses : document_status_id:id
document_status_translations  -->  tenants : tenant_id:id
document_statuses  -->  tenants : tenant_id:id
eam_asset_assignments  -->  eam_fixed_assets : asset_id:id
eam_asset_assignments  -->  projects : project_id:id
eam_asset_assignments  -->  tenants : tenant_id:id
eam_asset_categories  -->  eam_asset_categories : parent_id:id
eam_asset_categories  -->  tenants : tenant_id:id
eam_asset_classes  -->  tenants : tenant_id:id
eam_asset_components  -->  eam_fixed_assets : parent_asset_id:id
eam_asset_components  -->  eam_fixed_assets : component_asset_id:id
eam_asset_components  -->  tenants : tenant_id:id
eam_asset_custodians  -->  eam_fixed_assets : asset_id:id
eam_asset_custodians  -->  tenants : tenant_id:id
eam_asset_custodians  -->  users : assigned_by_user_id:id
eam_asset_custodians  -->  users : custodian_user_id:id
eam_asset_disposals  -->  eam_fixed_assets : asset_id:id
eam_asset_disposals  -->  journal_entries : journal_entry_id:id
eam_asset_disposals  -->  tenants : tenant_id:id
eam_asset_disposals  -->  users : initiated_by_user_id:id
eam_asset_disposals  -->  workflow_instances : workflow_instance_id:id
eam_asset_documents  -->  eam_fixed_assets : asset_id:id
eam_asset_documents  -->  tenants : tenant_id:id
eam_asset_documents  -->  users : uploaded_by_user_id:id
eam_asset_locations  -->  eam_asset_locations : parent_id:id
eam_asset_locations  -->  tenants : tenant_id:id
eam_asset_locations  -->  warehouses : warehouse_id:id
eam_asset_relationships  -->  eam_fixed_assets : source_asset_id:id
eam_asset_relationships  -->  eam_fixed_assets : target_asset_id:id
eam_asset_relationships  -->  tenants : tenant_id:id
eam_asset_transfers  -->  eam_asset_locations : from_location_id:id
eam_asset_transfers  -->  eam_asset_locations : to_location_id:id
eam_asset_transfers  -->  eam_fixed_assets : asset_id:id
eam_asset_transfers  -->  tenants : tenant_id:id
eam_asset_transfers  -->  users : from_custodian_id:id
eam_asset_transfers  -->  users : initiated_by_user_id:id
eam_asset_transfers  -->  users : to_custodian_id:id
eam_asset_transfers  -->  workflow_instances : workflow_instance_id:id
eam_asset_valuations  -->  eam_fixed_assets : asset_id:id
eam_asset_valuations  -->  journal_entries : journal_entry_id:id
eam_asset_valuations  -->  tenants : tenant_id:id
eam_asset_valuations  -->  users : created_by_user_id:id
eam_asset_valuations  -->  workflow_instances : workflow_instance_id:id
eam_depreciation_runs  -->  fiscal_periods : fiscal_period_id:id
eam_depreciation_runs  -->  tenants : tenant_id:id
eam_depreciation_runs  -->  users : executed_by_user_id:id
eam_depreciation_schedules  -->  eam_depreciation_runs : run_id:id
eam_depreciation_schedules  -->  eam_fixed_assets : asset_id:id
eam_depreciation_schedules  -->  journal_entries : journal_entry_id:id
eam_depreciation_schedules  -->  tenants : tenant_id:id
eam_fixed_assets  -->  eam_asset_categories : category_id:id
eam_fixed_assets  -->  eam_asset_classes : asset_class_id:id
eam_fixed_assets  -->  eam_asset_locations : location_id:id
eam_fixed_assets  -->  eam_fixed_assets : parent_asset_id:id
eam_fixed_assets  -->  projects : project_id:id
eam_fixed_assets  -->  purchase_orders : purchase_order_id:id
eam_fixed_assets  -->  purchase_receipts : purchase_receipt_id:id
eam_fixed_assets  -->  suppliers : supplier_id:id
eam_fixed_assets  -->  tenants : tenant_id:id
eam_fixed_assets  -->  users : custodian_user_id:id
eam_fixed_assets  -->  workflow_instances : workflow_instance_id:id
eam_maintenance_activities  -->  eam_fixed_assets : asset_id:id
eam_maintenance_activities  -->  eam_maintenance_work_orders : work_order_id:id
eam_maintenance_activities  -->  tenants : tenant_id:id
eam_maintenance_activities  -->  work_orders : work_order_id:id
eam_maintenance_plans  -->  eam_asset_classes : asset_class_id:id
eam_maintenance_plans  -->  eam_fixed_assets : asset_id:id
eam_maintenance_plans  -->  tenants : tenant_id:id
eam_maintenance_work_orders  -->  eam_fixed_assets : asset_id:id
eam_maintenance_work_orders  -->  eam_maintenance_plans : plan_id:id
eam_maintenance_work_orders  -->  tenants : tenant_id:id
eam_maintenance_work_orders  -->  users : assigned_technician_id:id
eam_maintenance_work_orders  -->  workflow_instances : workflow_instance_id:id
eam_project_asset_allocations  -->  eam_fixed_assets : asset_id:id
eam_project_asset_allocations  -->  projects : project_id:id
eam_project_asset_allocations  -->  tenants : tenant_id:id
eam_project_asset_allocations  -->  users : allocated_by_user_id:id
ecommerce_channels  -->  tenants : tenant_id:id
ecommerce_mappings  -->  ecommerce_channels : channel_id:id
ecommerce_mappings  -->  tenants : tenant_id:id
ei_inbound_logs  -->  invoices : invoice_id:id
ei_inbound_logs  -->  tenants : tenant_id:id
ei_outbound_logs  -->  invoices : invoice_id:id
ei_outbound_logs  -->  tenants : tenant_id:id
employee_profiles  -->  tenants : tenant_id:id
employee_profiles  -->  users : user_id:id
enterprise_audit_ledger  -->  tenants : tenant_id:id
enterprise_feature_flags  -->  tenants : tenant_id:id
enterprise_feature_flags  -->  users : user_id:id
esm_business_hours_calendars  -->  tenants : tenant_id:id
esm_change_requests  -->  esm_problems : problem_id:id
esm_change_requests  -->  esm_tickets : ticket_id:id
esm_change_requests  -->  tenants : tenant_id:id
esm_change_requests  -->  tickets : ticket_id:id
esm_change_requests  -->  workflow_instances : workflow_instance_id:id
esm_csat_surveys  -->  esm_tickets : ticket_id:id
esm_csat_surveys  -->  esm_work_orders : work_order_id:id
esm_csat_surveys  -->  tenants : tenant_id:id
esm_csat_surveys  -->  tickets : ticket_id:id
esm_csat_surveys  -->  work_orders : work_order_id:id
esm_incidents  -->  esm_tickets : ticket_id:id
esm_incidents  -->  tenants : tenant_id:id
esm_incidents  -->  tickets : ticket_id:id
esm_incidents  -->  workflow_instances : workflow_instance_id:id
esm_knowledge_articles  -->  esm_service_categories : category_id:id
esm_knowledge_articles  -->  tenants : tenant_id:id
esm_parts_consumptions  -->  esm_work_orders : work_order_id:id
esm_parts_consumptions  -->  products : product_id:id
esm_parts_consumptions  -->  tenants : tenant_id:id
esm_parts_consumptions  -->  warehouses : warehouse_id:id
esm_parts_consumptions  -->  work_orders : work_order_id:id
esm_problems  -->  esm_service_categories : category_id:id
esm_problems  -->  tenants : tenant_id:id
esm_service_appointments  -->  esm_service_technicians : technician_id:id
esm_service_appointments  -->  esm_work_orders : work_order_id:id
esm_service_appointments  -->  tenants : tenant_id:id
esm_service_appointments  -->  work_orders : work_order_id:id
esm_service_categories  -->  tenants : tenant_id:id
esm_service_contracts  -->  esm_support_plans : support_plan_id:id
esm_service_contracts  -->  tenants : tenant_id:id
esm_service_contracts  -->  workflow_instances : workflow_instance_id:id
esm_service_teams  -->  tenants : tenant_id:id
esm_service_technicians  -->  esm_service_teams : team_id:id
esm_service_technicians  -->  tenants : tenant_id:id
esm_service_technicians  -->  users : user_id:id
esm_service_visits  -->  appointments : appointment_id:id
esm_service_visits  -->  esm_service_appointments : appointment_id:id
esm_service_visits  -->  esm_service_technicians : technician_id:id
esm_service_visits  -->  esm_work_orders : work_order_id:id
esm_service_visits  -->  tenants : tenant_id:id
esm_service_visits  -->  work_orders : work_order_id:id
esm_sla_policies  -->  esm_service_categories : service_category_id:id
esm_sla_policies  -->  esm_support_plans : support_plan_id:id
esm_sla_policies  -->  tenants : tenant_id:id
esm_support_plans  -->  tenants : tenant_id:id
esm_ticket_time_entries  -->  esm_service_technicians : technician_id:id
esm_ticket_time_entries  -->  esm_tickets : ticket_id:id
esm_ticket_time_entries  -->  tenants : tenant_id:id
esm_ticket_time_entries  -->  tickets : ticket_id:id
esm_tickets  -->  contacts : contact_id:id
esm_tickets  -->  esm_knowledge_articles : knowledge_article_id:id
esm_tickets  -->  esm_service_categories : category_id:id
esm_tickets  -->  esm_service_contracts : service_contract_id:id
esm_tickets  -->  esm_service_teams : assigned_team_id:id
esm_tickets  -->  esm_service_technicians : assigned_technician_id:id
esm_tickets  -->  projects : project_id:id
esm_tickets  -->  tenants : tenant_id:id
esm_tickets  -->  workflow_instances : workflow_instance_id:id
esm_work_order_items  -->  esm_work_orders : work_order_id:id
esm_work_order_items  -->  products : product_id:id
esm_work_order_items  -->  tenants : tenant_id:id
esm_work_order_items  -->  work_orders : work_order_id:id
esm_work_orders  -->  esm_service_teams : service_team_id:id
esm_work_orders  -->  esm_service_technicians : assigned_technician_id:id
esm_work_orders  -->  esm_tickets : ticket_id:id
esm_work_orders  -->  invoices : invoice_id:id
esm_work_orders  -->  projects : project_id:id
esm_work_orders  -->  tenants : tenant_id:id
esm_work_orders  -->  tickets : ticket_id:id
esm_work_orders  -->  workflow_instances : workflow_instance_id:id
expense_attachments  -->  attachments : attachment_id:id
expense_attachments  -->  expenses : expense_id:id
expense_attachments  -->  tenants : tenant_id:id
expense_attachments  -->  users : updated_by:id
expense_attachments  -->  users : created_by:id
expense_categories  -->  tenants : tenant_id:id
expense_category_translations  -->  expense_categories : expense_category_id:id
expense_category_translations  -->  tenants : tenant_id:id
expense_items  -->  expense_reports : expense_report_id:id
expense_reports  -->  tenants : tenant_id:id
expense_reports  -->  users : user_id:id
expenses  -->  contacts : contact_id:id
expenses  -->  lookup_items : category_id:id
expenses  -->  projects : project_id:id
expenses  -->  service_reports : service_report_id:id
expenses  -->  tenants : tenant_id:id
expenses  -->  tickets : ticket_id:id
expenses  -->  users : created_by:id
expenses  -->  users : user_id:id
expenses  -->  users : updated_by:id
fee_notes  -->  contacts : client_id:id
fee_notes  -->  legal_cases : legal_case_id:id
fee_notes  -->  tenants : tenant_id:id
financial_closing_runs  -->  fiscal_periods : fiscal_period_id:id
financial_closing_runs  -->  tenants : tenant_id:id
fiscal_periods  -->  fiscal_years : fiscal_year_id:id
fiscal_periods  -->  tenants : tenant_id:id
fiscal_years  -->  tenants : tenant_id:id
forecast_scenarios  -->  tenants : tenant_id:id
fx_positions  -->  tenants : tenant_id:id
fx_revaluations  -->  tenants : tenant_id:id
general_ledger_entries  -->  tenants : tenant_id:id
general_ledger_lines  -->  chart_of_accounts : account_id:id
general_ledger_lines  -->  general_ledger_entries : general_ledger_entry_id:id
goods_receipt_items  -->  goods_receipts : goods_receipt_id:id
goods_receipt_items  -->  products : product_id:id
goods_receipt_items  -->  purchase_order_items : purchase_order_item_id:id
goods_receipts  -->  contacts : supplier_id:id
goods_receipts  -->  purchase_orders : purchase_order_id:id
goods_receipts  -->  suppliers : supplier_id:id
goods_receipts  -->  tenants : tenant_id:id
hr_attendance_records  -->  hr_employees : employee_id:id
hr_attendance_records  -->  projects : project_id:id
hr_attendance_records  -->  tenants : tenant_id:id
hr_business_units  -->  tenants : tenant_id:id
hr_certifications  -->  hr_employees : employee_id:id
hr_certifications  -->  tenants : tenant_id:id
hr_cost_centers  -->  tenants : tenant_id:id
hr_departments  -->  cost_centers : cost_center_id:id
hr_departments  -->  tenants : tenant_id:id
hr_employee_documents  -->  hr_employees : employee_id:id
hr_employee_documents  -->  tenants : tenant_id:id
hr_employee_lifecycle_events  -->  hr_employees : employee_id:id
hr_employee_lifecycle_events  -->  tenants : tenant_id:id
hr_employee_lifecycle_events  -->  workflow_instances : workflow_instance_id:id
hr_employee_skills  -->  hr_employees : employee_id:id
hr_employee_skills  -->  hr_skills : skill_id:id
hr_employee_skills  -->  tenants : tenant_id:id
hr_employees  -->  cost_centers : cost_center_id:id
hr_employees  -->  hr_business_units : business_unit_id:id
hr_employees  -->  hr_cost_centers : cost_center_id:id
hr_employees  -->  hr_departments : department_id:id
hr_employees  -->  hr_job_grades : job_grade_id:id
hr_employees  -->  hr_positions : position_id:id
hr_employees  -->  hr_teams : team_id:id
hr_employees  -->  tenants : tenant_id:id
hr_employees  -->  users : user_id:id
hr_employees  -->  workflow_instances : workflow_instance_id:id
hr_employment_contracts  -->  hr_employees : employee_id:id
hr_employment_contracts  -->  tenants : tenant_id:id
hr_employment_contracts  -->  workflow_instances : workflow_instance_id:id
hr_holiday_calendars  -->  tenants : tenant_id:id
hr_job_grades  -->  tenants : tenant_id:id
hr_leave_balances  -->  hr_employees : employee_id:id
hr_leave_balances  -->  hr_leave_types : leave_type_id:id
hr_leave_balances  -->  tenants : tenant_id:id
hr_leave_requests  -->  hr_employees : employee_id:id
hr_leave_requests  -->  hr_leave_types : leave_type_id:id
hr_leave_requests  -->  tenants : tenant_id:id
hr_leave_requests  -->  workflow_instances : workflow_instance_id:id
hr_leave_types  -->  tenants : tenant_id:id
hr_performance_reviews  -->  hr_employees : employee_id:id
hr_performance_reviews  -->  tenants : tenant_id:id
hr_performance_reviews  -->  workflow_instances : workflow_instance_id:id
hr_positions  -->  hr_departments : department_id:id
hr_positions  -->  hr_job_grades : job_grade_id:id
hr_positions  -->  tenants : tenant_id:id
hr_skills  -->  tenants : tenant_id:id
hr_teams  -->  hr_departments : department_id:id
hr_teams  -->  tenants : tenant_id:id
hr_timesheets  -->  cost_centers : cost_center_id:id
hr_timesheets  -->  hr_employees : employee_id:id
hr_timesheets  -->  projects : project_id:id
hr_timesheets  -->  tenants : tenant_id:id
hr_timesheets  -->  workflow_instances : workflow_instance_id:id
hr_training_courses  -->  tenants : tenant_id:id
hr_training_records  -->  hr_employees : employee_id:id
hr_training_records  -->  hr_training_courses : course_id:id
hr_training_records  -->  tenants : tenant_id:id
hr_training_records  -->  workflow_instances : workflow_instance_id:id
intercompany_funding  -->  cash_pools : cash_pool_id:id
intercompany_funding  -->  tenants : tenant_id:id
interest_schedules  -->  loan_agreements : loan_agreement_id:id
interest_schedules  -->  payment_lines : payment_line_id:id
interest_schedules  -->  tenants : tenant_id:id
inventory_adjustments  -->  tenants : tenant_id:id
inventory_adjustments  -->  warehouses : warehouse_id:id
inventory_audit_entries  -->  stock_items : stock_item_id:id
inventory_audit_entries  -->  tenants : tenant_id:id
inventory_count_lines  -->  inventory_count_sessions : inventory_count_session_id:id
inventory_count_lines  -->  stock_items : stock_item_id:id
inventory_count_lines  -->  stock_lots : lot_id:id
inventory_count_lines  -->  tenants : tenant_id:id
inventory_count_lines  -->  warehouse_bins : warehouse_bin_id:id
inventory_count_sessions  -->  tenants : tenant_id:id
inventory_count_sessions  -->  warehouses : warehouse_id:id
inventory_movement_type_translations  -->  inventory_movement_types : movement_type_id:id
inventory_movement_type_translations  -->  tenants : tenant_id:id
inventory_movement_types  -->  tenants : tenant_id:id
invoice_credit_applications  -->  invoices : credit_note_id:id
invoice_credit_applications  -->  invoices : original_invoice_id:id
invoice_credit_applications  -->  tenants : tenant_id:id
invoice_items  -->  delivery_note_items : delivery_note_item_id:id
invoice_items  -->  invoices : invoice_id:id
invoice_items  -->  products : product_id:id
invoice_items  -->  sales_order_items : sales_order_item_id:id
invoice_items  -->  tenants : tenant_id:id
invoice_qr_bill_data  -->  invoices : invoice_id:id
invoice_sdi_metadata  -->  invoices : invoice_id:id
invoice_service_reports  -->  invoices : invoice_id:id
invoice_service_reports  -->  service_reports : service_report_id:id
invoice_service_reports  -->  tenants : tenant_id:id
invoice_service_reports  -->  users : created_by:id
invoices  -->  contacts : contact_id:id
invoices  -->  customer_agreements : customer_agreement_id:id
invoices  -->  delivery_notes : delivery_note_id:id
invoices  -->  invoices : proforma_id:id
invoices  -->  invoices : related_invoice_id:id
invoices  -->  project_milestones : project_milestone_id:id
invoices  -->  projects : project_id:id
invoices  -->  quotes : quote_id:id
invoices  -->  sales_orders : sales_order_id:id
invoices  -->  subscriptions : subscription_id:id
invoices  -->  tenants : tenant_id:id
invoices  -->  workflow_instances : workflow_instance_id:id
journal_batches  -->  tenants : tenant_id:id
journal_entries  -->  fiscal_periods : fiscal_period_id:id
journal_entries  -->  journal_batches : batch_id:id
journal_entries  -->  tenants : tenant_id:id
journal_entries  -->  workflow_instances : workflow_instance_id:id
journal_lines  -->  chart_of_accounts : account_id:id
journal_lines  -->  cost_centers : cost_center_id:id
journal_lines  -->  journal_entries : journal_entry_id:id
journal_lines  -->  profit_centers : profit_center_id:id
journal_lines  -->  projects : project_id:id
journal_lines  -->  tenants : tenant_id:id
journal_lines  -->  vat_codes : vat_code_id:id
leave_balances  -->  tenants : tenant_id:id
leave_balances  -->  users : user_id:id
leave_requests  -->  tenants : tenant_id:id
leave_requests  -->  users : user_id:id
leave_requests  -->  users : approved_by:id
legal_cases  -->  contacts : client_id:id
legal_cases  -->  tenants : tenant_id:id
letters_of_credit  -->  tenants : tenant_id:id
loan_agreements  -->  tenants : tenant_id:id
loan_agreements  -->  workflow_instances : workflow_instance_id:id
loan_drawdowns  -->  loan_agreements : loan_agreement_id:id
loan_drawdowns  -->  tenants : tenant_id:id
lookup_item_translations  -->  lookup_items : lookup_item_id:id
lookup_item_translations  -->  tenants : tenant_id:id
lookup_items  -->  lookup_categories : category_id:id
lookup_items  -->  tenants : tenant_id:id
loyalty_cards  -->  contacts : contact_id:id
loyalty_cards  -->  tenants : tenant_id:id
loyalty_transactions  -->  invoices : invoice_id:id
loyalty_transactions  -->  loyalty_cards : loyalty_card_id:id
loyalty_transactions  -->  tenants : tenant_id:id
mfg_bom_components  -->  mfg_boms : bom_id:id
mfg_bom_components  -->  tenants : tenant_id:id
mfg_boms  -->  mfg_items : mfg_item_id:id
mfg_boms  -->  tenants : tenant_id:id
mfg_engineering_change_orders  -->  tenants : tenant_id:id
mfg_items  -->  stock_items : stock_item_id:id
mfg_items  -->  tenants : tenant_id:id
mfg_labor_time_logs  -->  mfg_shop_floor_executions : execution_id:id
mfg_labor_time_logs  -->  tenants : tenant_id:id
mfg_machine_centers  -->  mfg_work_centers : work_center_id:id
mfg_machine_centers  -->  tenants : tenant_id:id
mfg_machine_logs  -->  mfg_shop_floor_executions : execution_id:id
mfg_machine_logs  -->  tenants : tenant_id:id
mfg_mrp_peggings  -->  mfg_mrp_planned_orders : planned_order_id:id
mfg_mrp_peggings  -->  tenants : tenant_id:id
mfg_mrp_planned_orders  -->  mfg_items : mfg_item_id:id
mfg_mrp_planned_orders  -->  mfg_mrp_runs : mrp_run_id:id
mfg_mrp_planned_orders  -->  tenants : tenant_id:id
mfg_mrp_runs  -->  tenants : tenant_id:id
mfg_mrp_shortages  -->  mfg_items : mfg_item_id:id
mfg_mrp_shortages  -->  mfg_mrp_runs : mrp_run_id:id
mfg_mrp_shortages  -->  tenants : tenant_id:id
mfg_operations  -->  mfg_routings : routing_id:id
mfg_operations  -->  mfg_work_centers : work_center_id:id
mfg_operations  -->  tenants : tenant_id:id
mfg_production_costs  -->  mfg_production_orders : production_order_id:id
mfg_production_costs  -->  production_orders : production_order_id:id
mfg_production_costs  -->  tenants : tenant_id:id
mfg_production_order_lines  -->  mfg_items : mfg_item_id:id
mfg_production_order_lines  -->  mfg_production_orders : production_order_id:id
mfg_production_order_lines  -->  production_orders : production_order_id:id
mfg_production_order_lines  -->  tenants : tenant_id:id
mfg_production_order_operations  -->  mfg_production_orders : production_order_id:id
mfg_production_order_operations  -->  production_orders : production_order_id:id
mfg_production_order_operations  -->  tenants : tenant_id:id
mfg_production_orders  -->  mfg_items : mfg_item_id:id
mfg_production_orders  -->  projects : project_id:id
mfg_production_orders  -->  tenants : tenant_id:id
mfg_production_versions  -->  mfg_boms : bom_id:id
mfg_production_versions  -->  mfg_items : mfg_item_id:id
mfg_production_versions  -->  mfg_routings : routing_id:id
mfg_production_versions  -->  tenants : tenant_id:id
mfg_quality_characteristics  -->  mfg_quality_plans : quality_plan_id:id
mfg_quality_characteristics  -->  tenants : tenant_id:id
mfg_quality_inspections  -->  mfg_quality_plans : quality_plan_id:id
mfg_quality_inspections  -->  production_orders : production_order_id:id
mfg_quality_inspections  -->  tenants : tenant_id:id
mfg_quality_non_conformances  -->  production_orders : production_order_id:id
mfg_quality_non_conformances  -->  tenants : tenant_id:id
mfg_quality_plans  -->  mfg_items : mfg_item_id:id
mfg_quality_plans  -->  tenants : tenant_id:id
mfg_routings  -->  mfg_items : mfg_item_id:id
mfg_routings  -->  tenants : tenant_id:id
mfg_shop_floor_executions  -->  mfg_production_orders : production_order_id:id
mfg_shop_floor_executions  -->  production_orders : production_order_id:id
mfg_shop_floor_executions  -->  tenants : tenant_id:id
mfg_work_center_capacities  -->  mfg_work_centers : work_center_id:id
mfg_work_center_capacities  -->  tenants : tenant_id:id
mfg_work_centers  -->  tenants : tenant_id:id
notification_type_translations  -->  notification_types : notification_type_id:id
notification_type_translations  -->  tenants : tenant_id:id
notification_types  -->  tenants : tenant_id:id
passive_invoices  -->  contacts : supplier_id:id
passive_invoices  -->  suppliers : supplier_id:id
passive_invoices  -->  tenants : tenant_id:id
payment_approvals  -->  payment_batches : payment_batch_id:id
payment_approvals  -->  tenants : tenant_id:id
payment_batches  -->  bank_accounts : bank_account_id:id
payment_batches  -->  tenants : tenant_id:id
payment_batches  -->  workflow_instances : workflow_instance_id:id
payment_executions  -->  payment_batches : payment_batch_id:id
payment_executions  -->  tenants : tenant_id:id
payment_import_lines  -->  invoices : invoice_id:id
payment_import_lines  -->  payment_imports : payment_import_id:id
payment_import_lines  -->  payments : payment_id:id
payment_import_lines  -->  tenants : tenant_id:id
payment_imports  -->  tenants : tenant_id:id
payment_imports  -->  users : user_id:id
payment_lines  -->  invoices : invoice_id:id
payment_lines  -->  payment_batches : payment_batch_id:id
payment_lines  -->  tenants : tenant_id:id
payment_method_translations  -->  payment_methods : payment_method_id:id
payment_method_translations  -->  tenants : tenant_id:id
payment_methods  -->  tenants : tenant_id:id
payment_reminders  -->  invoices : invoice_id:id
payment_reminders  -->  tenants : tenant_id:id
payment_term_installments  -->  payment_terms : payment_term_id:id
payment_term_translations  -->  payment_terms : payment_term_id:id
payment_term_translations  -->  tenants : tenant_id:id
payment_terms  -->  tenants : tenant_id:id
payments  -->  bank_statement_lines : bank_statement_line_id:id
payments  -->  invoices : invoice_id:id
payments  -->  tenants : tenant_id:id
period_locks  -->  fiscal_periods : fiscal_period_id:id
period_locks  -->  tenants : tenant_id:id
portal_access_tokens  -->  contacts : contact_id:id
portal_access_tokens  -->  tenants : tenant_id:id
portal_activity_logs  -->  contacts : contact_id:id
portal_activity_logs  -->  portal_access_tokens : portal_access_token_id:id
portal_activity_logs  -->  tenants : tenant_id:id
pos_sale_items  -->  pos_sales : pos_sale_id:id
pos_sale_items  -->  products : product_id:id
pos_sales  -->  contacts : contact_id:id
pos_sales  -->  loyalty_cards : loyalty_card_id:id
pos_sales  -->  pos_sessions : pos_session_id:id
pos_sales  -->  tenants : tenant_id:id
pos_sessions  -->  pos_terminals : pos_terminal_id:id
pos_sessions  -->  tenants : tenant_id:id
pos_sessions  -->  users : user_id:id
pos_terminals  -->  tenants : tenant_id:id
posting_templates  -->  tenants : tenant_id:id
price_list_items  -->  price_lists : price_list_id:id
price_list_items  -->  products : product_id:id
price_lists  -->  tenants : tenant_id:id
product_brands  -->  tenants : tenant_id:id
product_categories  -->  product_categories : parent_id:id
product_categories  -->  tenants : tenant_id:id
production_order_stages  -->  production_orders : production_order_id:id
production_orders  -->  bills_of_materials : bill_of_materials_id:id
production_orders  -->  tenants : tenant_id:id
products  -->  product_brands : brand_id:id
products  -->  product_categories : category_id:id
products  -->  products : parent_id:id
products  -->  tenants : tenant_id:id
products  -->  units_of_measure : unit_of_measure_id:id
profit_centers  -->  tenants : tenant_id:id
progress_billings  -->  construction_sites : construction_site_id:id
progress_billings  -->  tenants : tenant_id:id
project_audit_entries  -->  projects : project_id:id
project_audit_entries  -->  tenants : tenant_id:id
project_billing_events  -->  invoices : invoice_id:id
project_billing_events  -->  projects : project_id:id
project_billing_events  -->  tenants : tenant_id:id
project_budget_approvals  -->  project_budget_versions : budget_version_id:id
project_budget_approvals  -->  project_budgets : project_budget_id:id
project_budget_approvals  -->  tenants : tenant_id:id
project_budget_lines  -->  project_budgets : project_budget_id:id
project_budget_lines  -->  project_phases : project_phase_id:id
project_budget_lines  -->  tenants : tenant_id:id
project_budget_versions  -->  project_budgets : project_budget_id:id
project_budget_versions  -->  tenants : tenant_id:id
project_budgets  -->  projects : project_id:id
project_budgets  -->  tenants : tenant_id:id
project_change_order_lines  -->  project_change_orders : project_change_order_id:id
project_change_order_lines  -->  tenants : tenant_id:id
project_change_orders  -->  projects : project_id:id
project_change_orders  -->  tenants : tenant_id:id
project_cost_allocations  -->  project_cost_entries : project_cost_entry_id:id
project_cost_allocations  -->  project_tasks : project_task_id:id
project_cost_allocations  -->  tenants : tenant_id:id
project_cost_entries  -->  project_phases : project_phase_id:id
project_cost_entries  -->  project_tasks : project_task_id:id
project_cost_entries  -->  projects : project_id:id
project_cost_entries  -->  tenants : tenant_id:id
project_cost_snapshots  -->  projects : project_id:id
project_cost_snapshots  -->  tenants : tenant_id:id
project_documents  -->  projects : project_id:id
project_documents  -->  tenants : tenant_id:id
project_documents  -->  users : uploaded_by:id
project_financial_summaries  -->  projects : project_id:id
project_financial_summaries  -->  tenants : tenant_id:id
project_invoice_links  -->  invoices : invoice_id:id
project_invoice_links  -->  projects : project_id:id
project_invoice_links  -->  tenants : tenant_id:id
project_issues  -->  projects : project_id:id
project_issues  -->  tenants : tenant_id:id
project_issues  -->  users : assigned_user_id:id
project_milestones  -->  invoices : invoice_id:id
project_milestones  -->  project_phases : project_phase_id:id
project_milestones  -->  projects : project_id:id
project_milestones  -->  tenants : tenant_id:id
project_notes  -->  projects : project_id:id
project_notes  -->  tenants : tenant_id:id
project_notes  -->  users : author_user_id:id
project_phases  -->  projects : project_id:id
project_phases  -->  tenants : tenant_id:id
project_portfolios  -->  tenants : tenant_id:id
project_portfolios  -->  users : portfolio_manager_user_id:id
project_profitability_snapshots  -->  projects : project_id:id
project_profitability_snapshots  -->  tenants : tenant_id:id
project_resources  -->  contacts : contact_id:id
project_resources  -->  tenants : tenant_id:id
project_resources  -->  users : user_id:id
project_revenue_recognition  -->  projects : project_id:id
project_revenue_recognition  -->  tenants : tenant_id:id
project_risks  -->  projects : project_id:id
project_risks  -->  tenants : tenant_id:id
project_risks  -->  users : owner_user_id:id
project_status_histories  -->  projects : project_id:id
project_status_histories  -->  tenants : tenant_id:id
project_status_histories  -->  users : changed_by:id
project_status_translations  -->  project_statuses : project_status_id:id
project_status_translations  -->  tenants : tenant_id:id
project_statuses  -->  tenants : tenant_id:id
project_task_assignments  -->  project_tasks : project_task_id:id
project_task_assignments  -->  tenants : tenant_id:id
project_task_assignments  -->  users : user_id:id
project_task_dependencies  -->  project_tasks : successor_task_id:id
project_task_dependencies  -->  project_tasks : predecessor_task_id:id
project_task_dependencies  -->  tenants : tenant_id:id
project_tasks  -->  project_milestones : project_milestone_id:id
project_tasks  -->  project_phases : project_phase_id:id
project_tasks  -->  project_tasks : parent_task_id:id
project_tasks  -->  projects : project_id:id
project_tasks  -->  tenants : tenant_id:id
project_templates  -->  tenants : tenant_id:id
project_timesheets  -->  project_tasks : project_task_id:id
project_timesheets  -->  projects : project_id:id
project_timesheets  -->  tenants : tenant_id:id
project_timesheets  -->  users : user_id:id
project_variation_requests  -->  projects : project_id:id
project_variation_requests  -->  tenants : tenant_id:id
projects  -->  contacts : contact_id:id
projects  -->  cost_centers : cost_center_id:id
projects  -->  project_portfolios : portfolio_id:id
projects  -->  projects : parent_project_id:id
projects  -->  tenants : tenant_id:id
projects  -->  users : project_manager_user_id:id
purchase_order_items  -->  products : product_id:id
purchase_order_items  -->  purchase_orders : purchase_order_id:id
purchase_order_lines  -->  purchase_orders : purchase_order_id:id
purchase_order_lines  -->  supplier_catalogs : supplier_catalog_id:id
purchase_order_lines  -->  tenants : tenant_id:id
purchase_orders  -->  contacts : supplier_id:id
purchase_orders  -->  cost_centers : cost_center_id:id
purchase_orders  -->  projects : project_id:id
purchase_orders  -->  purchase_requests : purchase_request_id:id
purchase_orders  -->  purchase_requisitions : purchase_requisition_id:id
purchase_orders  -->  supplier_contracts : supplier_contract_id:id
purchase_orders  -->  suppliers : supplier_id:id
purchase_orders  -->  tenants : tenant_id:id
purchase_receipt_lines  -->  purchase_order_lines : purchase_order_line_id:id
purchase_receipt_lines  -->  purchase_receipts : purchase_receipt_id:id
purchase_receipt_lines  -->  tenants : tenant_id:id
purchase_receipts  -->  purchase_orders : purchase_order_id:id
purchase_receipts  -->  tenants : tenant_id:id
purchase_receipts  -->  users : received_by_user_id:id
purchase_receipts  -->  warehouses : warehouse_id:id
purchase_requests  -->  tenants : tenant_id:id
purchase_requests  -->  users : user_id:id
purchase_requisition_lines  -->  purchase_requisitions : purchase_requisition_id:id
purchase_requisition_lines  -->  supplier_catalogs : supplier_catalog_id:id
purchase_requisition_lines  -->  suppliers : suggested_supplier_id:id
purchase_requisition_lines  -->  tenants : tenant_id:id
purchase_requisitions  -->  cost_centers : cost_center_id:id
purchase_requisitions  -->  projects : project_id:id
purchase_requisitions  -->  tenants : tenant_id:id
purchase_requisitions  -->  users : requestor_user_id:id
purchase_return_lines  -->  purchase_order_lines : purchase_order_line_id:id
purchase_return_lines  -->  purchase_returns : purchase_return_id:id
purchase_return_lines  -->  tenants : tenant_id:id
purchase_returns  -->  purchase_orders : purchase_order_id:id
purchase_returns  -->  purchase_receipts : purchase_receipt_id:id
purchase_returns  -->  suppliers : supplier_id:id
purchase_returns  -->  tenants : tenant_id:id
purchase_returns  -->  users : returned_by_user_id:id
quote_items  -->  products : product_id:id
quote_items  -->  quotes : quote_id:id
quote_items  -->  tenants : tenant_id:id
quotes  -->  contacts : contact_id:id
quotes  -->  discount_policies : discount_policy_id:id
quotes  -->  price_lists : price_list_id:id
quotes  -->  tenants : tenant_id:id
quotes  -->  workflow_instances : workflow_instance_id:id
receivable_collections  -->  invoices : invoice_id:id
receivable_collections  -->  tenants : tenant_id:id
reconciliation_items  -->  reconciliation_runs : reconciliation_run_id:id
reconciliation_items  -->  tenants : tenant_id:id
reconciliation_matches  -->  bank_reconciliations : bank_reconciliation_id:id
reconciliation_matches  -->  bank_statement_lines : bank_statement_line_id:id
reconciliation_matches  -->  journal_entries : journal_entry_id:id
reconciliation_matches  -->  tenants : tenant_id:id
reconciliation_runs  -->  chart_of_accounts : account_id:id
reconciliation_runs  -->  tenants : tenant_id:id
region_translations  -->  regions : region_id:id
region_translations  -->  tenants : tenant_id:id
regions  -->  countries : country_id:id
regions  -->  tenants : tenant_id:id
rental_bookings  -->  contacts : client_id:id
rental_bookings  -->  rental_vehicles : rental_vehicle_id:id
rental_bookings  -->  tenants : tenant_id:id
rental_contracts  -->  rental_bookings : rental_booking_id:id
rental_contracts  -->  tenants : tenant_id:id
rental_vehicles  -->  tenants : tenant_id:id
rental_vehicles  -->  vehicles : vehicle_id:id
resource_allocations  -->  project_resources : resource_id:id
resource_allocations  -->  project_tasks : project_task_id:id
resource_allocations  -->  projects : project_id:id
resource_allocations  -->  tenants : tenant_id:id
resource_calendars  -->  project_resources : resource_id:id
resource_calendars  -->  tenants : tenant_id:id
resource_capacity_profiles  -->  project_resources : resource_id:id
resource_capacity_profiles  -->  tenants : tenant_id:id
rt_fiscal_receipts  -->  pos_sales : pos_sale_id:id
sales_commissions  -->  invoices : invoice_id:id
sales_commissions  -->  sales_orders : sales_order_id:id
sales_commissions  -->  sales_representatives : sales_representative_id:id
sales_commissions  -->  tenants : tenant_id:id
sales_opportunities  -->  contacts : customer_id:id
sales_opportunities  -->  tenants : tenant_id:id
sales_order_holds  -->  sales_orders : sales_order_id:id
sales_order_holds  -->  tenants : tenant_id:id
sales_order_items  -->  products : product_id:id
sales_order_items  -->  sales_orders : sales_order_id:id
sales_order_items  -->  tenants : tenant_id:id
sales_orders  -->  contacts : contact_id:id
sales_orders  -->  customer_agreements : customer_agreement_id:id
sales_orders  -->  discount_policies : discount_policy_id:id
sales_orders  -->  price_lists : price_list_id:id
sales_orders  -->  quotes : quote_id:id
sales_orders  -->  tenants : tenant_id:id
sales_orders  -->  workflow_instances : workflow_instance_id:id
sales_representatives  -->  tenants : tenant_id:id
sales_representatives  -->  users : user_id:id
sdi_uuid_links  -->  invoices : invoice_id:id
sdi_uuid_links  -->  tenants : tenant_id:id
service_report_lines  -->  lookup_items : line_type_id:id
service_report_lines  -->  products : item_id:id
service_report_lines  -->  service_reports : service_report_id:id
service_report_lines  -->  tenants : tenant_id:id
service_report_lines  -->  users : updated_by:id
service_report_lines  -->  users : created_by:id
service_report_lines  -->  vat_codes : vat_code_id:id
service_report_signatures  -->  service_reports : service_report_id:id
service_report_signatures  -->  tenants : tenant_id:id
service_report_signatures  -->  users : updated_by:id
service_report_signatures  -->  users : created_by:id
service_reports  -->  contacts : contact_id:id
service_reports  -->  lookup_items : status_id:id
service_reports  -->  projects : project_id:id
service_reports  -->  tenants : tenant_id:id
service_reports  -->  tickets : ticket_id:id
service_reports  -->  users : updated_by:id
service_reports  -->  users : created_by:id
service_reports  -->  users : technician_id:id
sessions  -->  users : user_id:id
stock_item_categories  -->  stock_item_categories : parent_category_id:id
stock_item_categories  -->  tenants : tenant_id:id
stock_items  -->  stock_item_categories : category_id:id
stock_items  -->  tenants : tenant_id:id
stock_lots  -->  stock_items : stock_item_id:id
stock_lots  -->  suppliers : supplier_id:id
stock_lots  -->  tenants : tenant_id:id
stock_movements  -->  products : product_id:id
stock_movements  -->  stock_items : stock_item_id:id
stock_movements  -->  tenants : tenant_id:id
stock_movements  -->  warehouses : warehouse_id:id
stock_packing_lists  -->  stock_pick_lists : stock_pick_list_id:id
stock_packing_lists  -->  tenants : tenant_id:id
stock_pick_lines  -->  stock_items : stock_item_id:id
stock_pick_lines  -->  stock_lots : lot_id:id
stock_pick_lines  -->  stock_pick_lists : stock_pick_list_id:id
stock_pick_lines  -->  tenants : tenant_id:id
stock_pick_lines  -->  warehouse_bins : warehouse_bin_id:id
stock_pick_lists  -->  tenants : tenant_id:id
stock_pick_lists  -->  warehouses : warehouse_id:id
stock_quants  -->  stock_items : stock_item_id:id
stock_quants  -->  stock_lots : lot_id:id
stock_quants  -->  tenants : tenant_id:id
stock_quants  -->  warehouse_bins : warehouse_bin_id:id
stock_reorder_rules  -->  stock_items : stock_item_id:id
stock_reorder_rules  -->  tenants : tenant_id:id
stock_reorder_rules  -->  warehouses : warehouse_id:id
stock_reservations  -->  stock_items : stock_item_id:id
stock_reservations  -->  tenants : tenant_id:id
stock_reservations  -->  warehouses : warehouse_id:id
stock_serial_numbers  -->  stock_items : stock_item_id:id
stock_serial_numbers  -->  stock_lots : lot_id:id
stock_serial_numbers  -->  tenants : tenant_id:id
stock_serial_numbers  -->  warehouse_bins : current_warehouse_bin_id:id
stock_valuation_snapshots  -->  stock_items : stock_item_id:id
stock_valuation_snapshots  -->  tenants : tenant_id:id
stock_valuation_snapshots  -->  warehouses : warehouse_id:id
sub_billing_runs  -->  tenants : tenant_id:id
sub_churn_predictions  -->  sub_subscriptions : subscription_id:id
sub_churn_predictions  -->  subscriptions : subscription_id:id
sub_churn_predictions  -->  tenants : tenant_id:id
sub_dunning_policies  -->  tenants : tenant_id:id
sub_dunning_records  -->  invoices : invoice_id:id
sub_dunning_records  -->  sub_subscriptions : subscription_id:id
sub_dunning_records  -->  subscriptions : subscription_id:id
sub_dunning_records  -->  tenants : tenant_id:id
sub_invoice_schedules  -->  invoices : invoice_id:id
sub_invoice_schedules  -->  sub_subscriptions : subscription_id:id
sub_invoice_schedules  -->  subscriptions : subscription_id:id
sub_invoice_schedules  -->  tenants : tenant_id:id
sub_partner_commissions  -->  invoices : invoice_id:id
sub_partner_commissions  -->  sub_subscriptions : subscription_id:id
sub_partner_commissions  -->  subscriptions : subscription_id:id
sub_partner_commissions  -->  tenants : tenant_id:id
sub_performance_obligations  -->  sub_revenue_contracts : revenue_contract_id:id
sub_performance_obligations  -->  tenants : tenant_id:id
sub_plan_features  -->  sub_plans : plan_id:id
sub_plan_features  -->  tenants : tenant_id:id
sub_plans  -->  products : product_id:id
sub_plans  -->  sub_products : product_id:id
sub_plans  -->  tenants : tenant_id:id
sub_price_books  -->  tenants : tenant_id:id
sub_pricing_tiers  -->  sub_plans : plan_id:id
sub_pricing_tiers  -->  tenants : tenant_id:id
sub_products  -->  tenants : tenant_id:id
sub_revenue_contracts  -->  sub_subscriptions : subscription_id:id
sub_revenue_contracts  -->  subscriptions : subscription_id:id
sub_revenue_contracts  -->  tenants : tenant_id:id
sub_revenue_recognition_entries  -->  sub_performance_obligations : performance_obligation_id:id
sub_revenue_recognition_entries  -->  tenants : tenant_id:id
sub_revenue_schedules  -->  journal_entries : journal_entry_id:id
sub_revenue_schedules  -->  sub_performance_obligations : performance_obligation_id:id
sub_revenue_schedules  -->  tenants : tenant_id:id
sub_subscription_items  -->  products : product_id:id
sub_subscription_items  -->  sub_plans : plan_id:id
sub_subscription_items  -->  sub_products : product_id:id
sub_subscription_items  -->  sub_subscriptions : subscription_id:id
sub_subscription_items  -->  sub_usage_metrics : metric_id:id
sub_subscription_items  -->  subscriptions : subscription_id:id
sub_subscription_items  -->  tenants : tenant_id:id
sub_subscription_versions  -->  sub_subscriptions : subscription_id:id
sub_subscription_versions  -->  subscriptions : subscription_id:id
sub_subscription_versions  -->  tenants : tenant_id:id
sub_subscriptions  -->  bank_accounts : bank_account_id:id
sub_subscriptions  -->  sub_plans : plan_id:id
sub_subscriptions  -->  tenants : tenant_id:id
sub_subscriptions  -->  workflow_instances : workflow_instance_id:id
sub_usage_aggregations  -->  sub_subscription_items : subscription_item_id:id
sub_usage_aggregations  -->  subscription_items : subscription_item_id:id
sub_usage_aggregations  -->  tenants : tenant_id:id
sub_usage_events  -->  sub_subscription_items : subscription_item_id:id
sub_usage_events  -->  sub_subscriptions : subscription_id:id
sub_usage_events  -->  subscription_items : subscription_item_id:id
sub_usage_events  -->  subscriptions : subscription_id:id
sub_usage_events  -->  tenants : tenant_id:id
sub_usage_metrics  -->  tenants : tenant_id:id
subscription_items  -->  products : product_id:id
subscription_items  -->  subscriptions : subscription_id:id
subscription_runs  -->  invoices : invoice_id:id
subscription_runs  -->  subscriptions : subscription_id:id
subscription_runs  -->  tenants : tenant_id:id
subscriptions  -->  contacts : contact_id:id
subscriptions  -->  tenants : tenant_id:id
supplier_catalogs  -->  suppliers : supplier_id:id
supplier_catalogs  -->  tenants : tenant_id:id
supplier_categories  -->  tenants : tenant_id:id
supplier_contacts  -->  suppliers : supplier_id:id
supplier_contacts  -->  tenants : tenant_id:id
supplier_contracts  -->  suppliers : supplier_id:id
supplier_contracts  -->  tenants : tenant_id:id
supplier_evaluations  -->  suppliers : supplier_id:id
supplier_evaluations  -->  tenants : tenant_id:id
supplier_evaluations  -->  users : evaluator_user_id:id
supplier_ledger  -->  journal_entries : journal_entry_id:id
supplier_ledger  -->  suppliers : supplier_id:id
supplier_ledger  -->  tenants : tenant_id:id
supplier_payments  -->  bank_statement_lines : bank_statement_line_id:id
supplier_payments  -->  passive_invoices : passive_invoice_id:id
supplier_payments  -->  tenants : tenant_id:id
supplier_price_lists  -->  supplier_catalogs : supplier_catalog_id:id
supplier_price_lists  -->  tenants : tenant_id:id
supplier_scorecards  -->  suppliers : supplier_id:id
supplier_scorecards  -->  tenants : tenant_id:id
suppliers  -->  contacts : contact_id:id
suppliers  -->  supplier_categories : supplier_category_id:id
suppliers  -->  tenants : tenant_id:id
task_status_translations  -->  task_statuses : task_status_id:id
task_status_translations  -->  tenants : tenant_id:id
task_statuses  -->  tenants : tenant_id:id
tenant_backups  -->  tenants : tenant_id:id
tenant_backups  -->  users : user_id:id
tenant_user  -->  tenants : tenant_id:id
tenant_user  -->  users : user_id:id
three_way_match_logs  -->  passive_invoices : passive_invoice_id:id
three_way_match_logs  -->  purchase_orders : purchase_order_id:id
three_way_match_logs  -->  purchase_receipts : purchase_receipt_id:id
three_way_match_logs  -->  tenants : tenant_id:id
ticket_messages  -->  tenants : tenant_id:id
ticket_messages  -->  tickets : ticket_id:id
ticket_messages  -->  users : author_id:id
tickets  -->  contacts : client_id:id
tickets  -->  tenants : tenant_id:id
tickets  -->  users : assigned_to_user_id:id
time_entries  -->  tenants : tenant_id:id
time_entries  -->  users : user_id:id
time_entries  -->  users : approved_by:id
tire_hotel_records  -->  tenants : tenant_id:id
tire_hotel_records  -->  vehicles : vehicle_id:id
transactional_inbox  -->  tenants : tenant_id:id
transactional_outbox  -->  tenants : tenant_id:id
transactional_outbox_archive  -->  tenants : tenant_id:id
translations  -->  tenants : tenant_id:id
treasury_alerts  -->  tenants : tenant_id:id
units_of_measure  -->  tenants : tenant_id:id
vat_code_translations  -->  tenants : tenant_id:id
vat_code_translations  -->  vat_codes : vat_code_id:id
vat_codes  -->  tenants : tenant_id:id
vat_registers  -->  tenants : tenant_id:id
vat_settlements  -->  fiscal_periods : fiscal_period_id:id
vat_settlements  -->  tenants : tenant_id:id
vehicle_inspections  -->  tenants : tenant_id:id
vehicle_inspections  -->  vehicles : vehicle_id:id
vehicles  -->  contacts : client_id:id
vehicles  -->  tenants : tenant_id:id
warehouse_aisles  -->  tenants : tenant_id:id
warehouse_aisles  -->  warehouse_zones : warehouse_zone_id:id
warehouse_bins  -->  tenants : tenant_id:id
warehouse_bins  -->  warehouse_racks : warehouse_rack_id:id
warehouse_racks  -->  tenants : tenant_id:id
warehouse_racks  -->  warehouse_aisles : warehouse_aisle_id:id
warehouse_zones  -->  tenants : tenant_id:id
warehouse_zones  -->  warehouses : warehouse_id:id
warehouses  -->  tenants : tenant_id:id
work_order_lines  -->  products : product_id:id
work_order_lines  -->  work_orders : work_order_id:id
work_orders  -->  contacts : client_id:id
work_orders  -->  invoices : invoice_id:id
work_orders  -->  tenants : tenant_id:id
work_orders  -->  tickets : ticket_id:id
work_orders  -->  users : technician_user_id:id
workflow_audit_entries  -->  tenants : tenant_id:id
workflow_audit_entries  -->  workflow_instance_steps : workflow_instance_step_id:id
workflow_audit_entries  -->  workflow_instances : workflow_instance_id:id
workflow_comments  -->  tenants : tenant_id:id
workflow_comments  -->  users : user_id:id
workflow_comments  -->  workflow_instance_steps : workflow_instance_step_id:id
workflow_comments  -->  workflow_instances : workflow_instance_id:id
workflow_definitions  -->  tenants : tenant_id:id
workflow_delegations  -->  tenants : tenant_id:id
workflow_delivery_attempts  -->  subscriptions : subscription_id:id
workflow_delivery_attempts  -->  tenants : tenant_id:id
workflow_delivery_attempts  -->  workflow_outbound_events : outbound_event_id:id
workflow_delivery_attempts  -->  workflow_webhook_subscriptions : subscription_id:id
workflow_escalation_rules  -->  tenants : tenant_id:id
workflow_instance_steps  -->  tenants : tenant_id:id
workflow_instance_steps  -->  workflow_instances : workflow_instance_id:id
workflow_instance_steps  -->  workflow_nodes : workflow_node_id:id
workflow_instances  -->  tenants : tenant_id:id
workflow_instances  -->  workflow_definitions : workflow_definition_id:id
workflow_nodes  -->  business_calendars : business_calendar_id:id
workflow_nodes  -->  tenants : tenant_id:id
workflow_nodes  -->  workflow_definitions : workflow_definition_id:id
workflow_outbound_events  -->  tenants : tenant_id:id
workflow_state_translations  -->  tenants : tenant_id:id
workflow_state_translations  -->  workflow_states : workflow_state_id:id
workflow_states  -->  tenants : tenant_id:id
workflow_transitions  -->  tenants : tenant_id:id
workflow_transitions  -->  workflow_definitions : workflow_definition_id:id
workflow_transitions  -->  workflow_nodes : from_node_id:id
workflow_transitions  -->  workflow_nodes : to_node_id:id
workflow_webhook_subscriptions  -->  tenants : tenant_id:id
working_capital_metrics  -->  tenants : tenant_id:id
