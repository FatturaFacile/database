# Fattura Facile Enterprise — Complete Schema Reference Index

This index catalogs all **416 database tables** across 17 modular architectural domains in the **Fattura Facile** database.

| Module Domain | File Reference | Tables Count | Description |
| :--- | :--- | :--- | :--- |
| **Core Tenancy, Authentication & System Infrastructure** | [`01_core_tenancy_and_system.md`](./modules/01_core_tenancy_and_system.md) | 15 | Foundation services managing multi-tenant isolation, user identity, access control, worker queues, caching, and backups. |
| **Audit Logging & Event Streaming (Outbox/Inbox)** | [`02_event_streaming_and_audit.md`](./modules/02_event_streaming_and_audit.md) | 5 | Enterprise event distribution, transactional outbox/inbox guarantees, and immutable Merkle audit trails. |
| **Workflow Engine & Approval Matrix** | [`03_workflow_engine.md`](./modules/03_workflow_engine.md) | 21 | Dynamic multi-step approval workflows, state machines, business calendars, and delegation logic. |
| **CRM & Customer Lifecycle Management** | [`04_crm_customer_management.md`](./modules/04_crm_customer_management.md) | 24 | Customer master directory, pipeline tracking, opportunities, leads, activities, and contact addresses. |
| **Sales, Invoicing & Electronic Invoicing (SDI)** | [`05_sales_invoicing_and_sdi.md`](./modules/05_sales_invoicing_and_sdi.md) | 20 | Billing lifecycle, quotes, sales orders, invoices, credit notes, delivery notes, and Italian SDI / Swiss QR-Bill integrations. |
| **Procurement, Suppliers & Accounts Payable** | [`06_procurement_and_ap.md`](./modules/06_procurement_and_ap.md) | 24 | Vendor master catalogs, purchase requisitions/orders, passive invoices, three-way matching, and supplier scorecards. |
| **Inventory, Warehouses & Logistics** | [`07_inventory_and_warehouses.md`](./modules/07_inventory_and_warehouses.md) | 28 | Multi-warehouse storage, bins, stock items, lots, serial numbers, quants, reservations, and pick/pack operations. |
| **General Ledger, Chart of Accounts & Fiscal Compliance** | [`08_general_ledger_and_fiscal.md`](./modules/08_general_ledger_and_fiscal.md) | 22 | Double-entry bookkeeping, chart of accounts, journal entries, VAT settlements, tax ledgers, and fiscal closures. |
| **Treasury, Banking & Cash Management** | [`09_treasury_and_banking.md`](./modules/09_treasury_and_banking.md) | 38 | Bank feeds, statements, cash forecasting, multi-currency FX revaluation, liquidity pools, loans, and guarantees. |
| **Projects, Job Costing & Timesheets** | [`10_projects_and_job_costing.md`](./modules/10_projects_and_job_costing.md) | 42 | Project portfolios, task tracking, billable activities, resource allocations, milestone billing, and construction sites. |
| **Manufacturing, Bills of Materials & MRP** | [`11_manufacturing_and_mrp.md`](./modules/11_manufacturing_and_mrp.md) | 29 | Multi-level BOMs, work centers, routings, production orders, shop floor tracking, quality inspections, and costing. |
| **Enterprise Asset Management (EAM)** | [`12_enterprise_asset_management.md`](./modules/12_enterprise_asset_management.md) | 18 | Fixed asset registers, depreciation schedules, preventive maintenance plans, inspections, and asset lifecycle tracking. |
| **Enterprise Service Management (ESM) & Field Operations** | [`13_esm_and_field_service.md`](./modules/13_esm_and_field_service.md) | 30 | ITSM ticketing, incident management, service catalogs, SLAs, customer portal, appointments, and work orders. |
| **Human Resources (HR) & Workforce Management** | [`14_human_resources_and_workforce.md`](./modules/14_human_resources_and_workforce.md) | 25 | Employee profiles, organizational hierarchies, leave tracking, certifications, job roles, and payroll metadata. |
| **Subscription Management & Recurring Billing** | [`15_subscriptions_and_recurring.md`](./modules/15_subscriptions_and_recurring.md) | 26 | SaaS plans, tiered pricing, subscription lifecycles, usage-based metering, dunning, churn prediction, and ASC 606 revenue recognition. |
| **Retail POS, Ecommerce & Loyalty** | [`16_retail_pos_and_ecommerce.md`](./modules/16_retail_pos_and_ecommerce.md) | 8 | Point-of-sale registers, omnichannel sales, ecommerce channel sync, loyalty cards, and fiscal cash registers. |
| **Master Reference Data & Specialized Verticals** | [`17_master_data_and_verticals.md`](./modules/17_master_data_and_verticals.md) | 41 | Geographic registers, business calendars, fleet/vehicle rentals, automotive tire management, expenses, and legal tracking. |

---

## Quick Table Jump Matrix

| Table Name | Module Domain Link | Scope |
| :--- | :--- | :--- |
| `cache` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#cache) | System / Global |
| `cache_locks` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#cachelocks) | System / Global |
| `dashboard_layouts` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#dashboardlayouts) | Shared Lookup |
| `enterprise_feature_flags` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#enterprisefeatureflags) | Shared Lookup |
| `failed_jobs` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#failedjobs) | System / Global |
| `job_batches` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#jobbatches) | System / Global |
| `jobs` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#jobs) | System / Global |
| `password_reset_tokens` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#passwordresettokens) | System / Global |
| `personal_access_tokens` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#personalaccesstokens) | System / Global |
| `sessions` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#sessions) | System / Global |
| `tenant_backups` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#tenantbackups) | Shared Lookup |
| `tenant_user` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#tenantuser) | Shared Lookup |
| `tenants` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#tenants) | System / Global |
| `translations` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#translations) | Shared Lookup |
| `users` | [`Core Tenancy, Authentication & System Infrastructure`](./modules/01_core_tenancy_and_system.md#users) | System / Global |
| `audit_logs` | [`Audit Logging & Event Streaming (Outbox/Inbox)`](./modules/02_event_streaming_and_audit.md#auditlogs) | Shared Lookup |
| `enterprise_audit_ledger` | [`Audit Logging & Event Streaming (Outbox/Inbox)`](./modules/02_event_streaming_and_audit.md#enterpriseauditledger) | Tenant-Scoped |
| `transactional_inbox` | [`Audit Logging & Event Streaming (Outbox/Inbox)`](./modules/02_event_streaming_and_audit.md#transactionalinbox) | Tenant-Scoped |
| `transactional_outbox` | [`Audit Logging & Event Streaming (Outbox/Inbox)`](./modules/02_event_streaming_and_audit.md#transactionaloutbox) | Tenant-Scoped |
| `transactional_outbox_archive` | [`Audit Logging & Event Streaming (Outbox/Inbox)`](./modules/02_event_streaming_and_audit.md#transactionaloutboxarchive) | Tenant-Scoped |
| `approval_decisions` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvaldecisions) | Tenant-Scoped |
| `approval_matrix_rules` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvalmatrixrules) | Tenant-Scoped |
| `approval_matrix_tiers` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvalmatrixtiers) | Tenant-Scoped |
| `approval_matrixes` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvalmatrixes) | Tenant-Scoped |
| `approval_status_translations` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvalstatustranslations) | Shared Lookup |
| `approval_statuses` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvalstatuses) | Shared Lookup |
| `approval_tokens` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#approvaltokens) | Tenant-Scoped |
| `workflow_audit_entries` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowauditentries) | Tenant-Scoped |
| `workflow_comments` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowcomments) | Tenant-Scoped |
| `workflow_definitions` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowdefinitions) | Tenant-Scoped |
| `workflow_delegations` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowdelegations) | Tenant-Scoped |
| `workflow_delivery_attempts` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowdeliveryattempts) | Tenant-Scoped |
| `workflow_escalation_rules` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowescalationrules) | Tenant-Scoped |
| `workflow_instance_steps` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowinstancesteps) | Tenant-Scoped |
| `workflow_instances` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowinstances) | Tenant-Scoped |
| `workflow_nodes` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflownodes) | Tenant-Scoped |
| `workflow_outbound_events` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowoutboundevents) | Tenant-Scoped |
| `workflow_state_translations` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowstatetranslations) | Shared Lookup |
| `workflow_states` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowstates) | Shared Lookup |
| `workflow_transitions` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowtransitions) | Tenant-Scoped |
| `workflow_webhook_subscriptions` | [`Workflow Engine & Approval Matrix`](./modules/03_workflow_engine.md#workflowwebhooksubscriptions) | Tenant-Scoped |
| `contact_addresses` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contactaddresses) | System / Global |
| `contact_categories` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contactcategories) | Shared Lookup |
| `contact_category_translations` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contactcategorytranslations) | Shared Lookup |
| `contact_type_translations` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contacttypetranslations) | Shared Lookup |
| `contact_types` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contacttypes) | Shared Lookup |
| `contacts` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#contacts) | Shared Lookup |
| `crm_accounts` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmaccounts) | Tenant-Scoped |
| `crm_activities` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmactivities) | Tenant-Scoped |
| `crm_campaign_members` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmcampaignmembers) | Tenant-Scoped |
| `crm_campaign_types` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmcampaigntypes) | Tenant-Scoped |
| `crm_campaigns` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmcampaigns) | Tenant-Scoped |
| `crm_contact_roles` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmcontactroles) | Tenant-Scoped |
| `crm_customer_health_profiles` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmcustomerhealthprofiles) | Tenant-Scoped |
| `crm_forecasts` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmforecasts) | Tenant-Scoped |
| `crm_lead_sources` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmleadsources) | Tenant-Scoped |
| `crm_leads` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmleads) | Tenant-Scoped |
| `crm_opportunities` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmopportunities) | Tenant-Scoped |
| `crm_opportunity_line_items` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmopportunitylineitems) | Tenant-Scoped |
| `crm_opportunity_stages` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#crmopportunitystages) | Tenant-Scoped |
| `customer_agreements` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#customeragreements) | Tenant-Scoped |
| `customer_credit_profiles` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#customercreditprofiles) | Tenant-Scoped |
| `customer_groups` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#customergroups) | Tenant-Scoped |
| `customer_ledger` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#customerledger) | Tenant-Scoped |
| `customer_ledger_entries` | [`CRM & Customer Lifecycle Management`](./modules/04_crm_customer_management.md#customerledgerentries) | Tenant-Scoped |
| `delivery_note_items` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#deliverynoteitems) | Shared Lookup |
| `delivery_notes` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#deliverynotes) | Shared Lookup |
| `ei_inbound_logs` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#eiinboundlogs) | Shared Lookup |
| `ei_outbound_logs` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#eioutboundlogs) | Shared Lookup |
| `fee_notes` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#feenotes) | Shared Lookup |
| `invoice_credit_applications` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoicecreditapplications) | Tenant-Scoped |
| `invoice_items` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoiceitems) | Shared Lookup |
| `invoice_qr_bill_data` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoiceqrbilldata) | System / Global |
| `invoice_sdi_metadata` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoicesdimetadata) | System / Global |
| `invoice_service_reports` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoiceservicereports) | Tenant-Scoped |
| `invoices` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#invoices) | Shared Lookup |
| `quotes` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#quotes) | Shared Lookup |
| `rt_fiscal_receipts` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#rtfiscalreceipts) | System / Global |
| `sales_commissions` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salescommissions) | Tenant-Scoped |
| `sales_opportunities` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salesopportunities) | Tenant-Scoped |
| `sales_order_holds` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salesorderholds) | Tenant-Scoped |
| `sales_order_items` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salesorderitems) | Shared Lookup |
| `sales_orders` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salesorders) | Shared Lookup |
| `sales_representatives` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#salesrepresentatives) | Tenant-Scoped |
| `sdi_uuid_links` | [`Sales, Invoicing & Electronic Invoicing (SDI)`](./modules/05_sales_invoicing_and_sdi.md#sdiuuidlinks) | Shared Lookup |
| `goods_receipt_items` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#goodsreceiptitems) | System / Global |
| `goods_receipts` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#goodsreceipts) | Shared Lookup |
| `passive_invoices` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#passiveinvoices) | Shared Lookup |
| `purchase_order_items` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaseorderitems) | System / Global |
| `purchase_order_lines` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaseorderlines) | Tenant-Scoped |
| `purchase_orders` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaseorders) | Shared Lookup |
| `purchase_receipt_lines` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchasereceiptlines) | Tenant-Scoped |
| `purchase_receipts` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchasereceipts) | Tenant-Scoped |
| `purchase_requests` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaserequests) | Shared Lookup |
| `purchase_requisition_lines` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaserequisitionlines) | Tenant-Scoped |
| `purchase_requisitions` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchaserequisitions) | Tenant-Scoped |
| `purchase_return_lines` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchasereturnlines) | Tenant-Scoped |
| `purchase_returns` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#purchasereturns) | Tenant-Scoped |
| `supplier_catalogs` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#suppliercatalogs) | Tenant-Scoped |
| `supplier_categories` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#suppliercategories) | Tenant-Scoped |
| `supplier_contacts` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#suppliercontacts) | Tenant-Scoped |
| `supplier_contracts` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#suppliercontracts) | Tenant-Scoped |
| `supplier_evaluations` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#supplierevaluations) | Tenant-Scoped |
| `supplier_ledger` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#supplierledger) | Tenant-Scoped |
| `supplier_payments` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#supplierpayments) | Shared Lookup |
| `supplier_price_lists` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#supplierpricelists) | Tenant-Scoped |
| `supplier_scorecards` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#supplierscorecards) | Tenant-Scoped |
| `suppliers` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#suppliers) | Tenant-Scoped |
| `three_way_match_logs` | [`Procurement, Suppliers & Accounts Payable`](./modules/06_procurement_and_ap.md#threewaymatchlogs) | Tenant-Scoped |
| `inventory_adjustments` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventoryadjustments) | Tenant-Scoped |
| `inventory_audit_entries` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventoryauditentries) | Tenant-Scoped |
| `inventory_count_lines` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventorycountlines) | Tenant-Scoped |
| `inventory_count_sessions` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventorycountsessions) | Tenant-Scoped |
| `inventory_movement_type_translations` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventorymovementtypetranslations) | Shared Lookup |
| `inventory_movement_types` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#inventorymovementtypes) | Shared Lookup |
| `price_list_items` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#pricelistitems) | System / Global |
| `price_lists` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#pricelists) | Shared Lookup |
| `product_brands` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#productbrands) | Shared Lookup |
| `product_categories` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#productcategories) | Shared Lookup |
| `products` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#products) | Shared Lookup |
| `stock_item_categories` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockitemcategories) | Tenant-Scoped |
| `stock_items` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockitems) | Tenant-Scoped |
| `stock_lots` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stocklots) | Tenant-Scoped |
| `stock_movements` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockmovements) | Shared Lookup |
| `stock_packing_lists` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockpackinglists) | Tenant-Scoped |
| `stock_pick_lines` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockpicklines) | Tenant-Scoped |
| `stock_pick_lists` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockpicklists) | Tenant-Scoped |
| `stock_quants` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockquants) | Tenant-Scoped |
| `stock_reorder_rules` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockreorderrules) | Tenant-Scoped |
| `stock_reservations` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockreservations) | Tenant-Scoped |
| `stock_serial_numbers` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockserialnumbers) | Tenant-Scoped |
| `stock_valuation_snapshots` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#stockvaluationsnapshots) | Tenant-Scoped |
| `warehouse_aisles` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#warehouseaisles) | Tenant-Scoped |
| `warehouse_bins` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#warehousebins) | Tenant-Scoped |
| `warehouse_racks` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#warehouseracks) | Tenant-Scoped |
| `warehouse_zones` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#warehousezones) | Tenant-Scoped |
| `warehouses` | [`Inventory, Warehouses & Logistics`](./modules/07_inventory_and_warehouses.md#warehouses) | Shared Lookup |
| `accounting_anomalies` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#accountinganomalies) | Tenant-Scoped |
| `accrual_entries` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#accrualentries) | Tenant-Scoped |
| `chart_of_accounts` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#chartofaccounts) | Shared Lookup |
| `cost_centers` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#costcenters) | Tenant-Scoped |
| `financial_closing_runs` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#financialclosingruns) | Tenant-Scoped |
| `fiscal_periods` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#fiscalperiods) | Tenant-Scoped |
| `fiscal_years` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#fiscalyears) | Tenant-Scoped |
| `general_ledger_entries` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#generalledgerentries) | Shared Lookup |
| `general_ledger_lines` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#generalledgerlines) | System / Global |
| `journal_batches` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#journalbatches) | Tenant-Scoped |
| `journal_entries` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#journalentries) | Tenant-Scoped |
| `journal_lines` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#journallines) | Tenant-Scoped |
| `period_locks` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#periodlocks) | Tenant-Scoped |
| `posting_templates` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#postingtemplates) | Tenant-Scoped |
| `profit_centers` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#profitcenters) | Tenant-Scoped |
| `reconciliation_items` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#reconciliationitems) | Tenant-Scoped |
| `reconciliation_matches` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#reconciliationmatches) | Tenant-Scoped |
| `reconciliation_runs` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#reconciliationruns) | Tenant-Scoped |
| `vat_code_translations` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#vatcodetranslations) | Shared Lookup |
| `vat_codes` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#vatcodes) | Shared Lookup |
| `vat_registers` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#vatregisters) | Tenant-Scoped |
| `vat_settlements` | [`General Ledger, Chart of Accounts & Fiscal Compliance`](./modules/08_general_ledger_and_fiscal.md#vatsettlements) | Shared Lookup |
| `bank_account_balances` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankaccountbalances) | Tenant-Scoped |
| `bank_account_signatories` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankaccountsignatories) | Tenant-Scoped |
| `bank_accounts` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankaccounts) | Shared Lookup |
| `bank_branches` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankbranches) | Tenant-Scoped |
| `bank_connections` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankconnections) | Tenant-Scoped |
| `bank_guarantees` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankguarantees) | Tenant-Scoped |
| `bank_reconciliations` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankreconciliations) | Tenant-Scoped |
| `bank_statement_lines` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankstatementlines) | Shared Lookup |
| `bank_statements` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#bankstatements) | Shared Lookup |
| `bank_transactions` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#banktransactions) | Shared Lookup |
| `cash_forecast_lines` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#cashforecastlines) | Tenant-Scoped |
| `cash_forecasts` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#cashforecasts) | Tenant-Scoped |
| `cash_pools` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#cashpools) | Tenant-Scoped |
| `currencies` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#currencies) | Shared Lookup |
| `exchange_rates` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#exchangerates) | System / Global |
| `fx_positions` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#fxpositions) | Tenant-Scoped |
| `fx_revaluations` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#fxrevaluations) | Tenant-Scoped |
| `intercompany_funding` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#intercompanyfunding) | Tenant-Scoped |
| `interest_schedules` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#interestschedules) | Tenant-Scoped |
| `letters_of_credit` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#lettersofcredit) | Tenant-Scoped |
| `loan_agreements` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#loanagreements) | Tenant-Scoped |
| `loan_drawdowns` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#loandrawdowns) | Tenant-Scoped |
| `payment_approvals` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentapprovals) | Tenant-Scoped |
| `payment_batches` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentbatches) | Shared Lookup |
| `payment_executions` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentexecutions) | Tenant-Scoped |
| `payment_import_lines` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentimportlines) | Shared Lookup |
| `payment_imports` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentimports) | Shared Lookup |
| `payment_lines` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentlines) | Tenant-Scoped |
| `payment_method_translations` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentmethodtranslations) | Shared Lookup |
| `payment_methods` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentmethods) | Shared Lookup |
| `payment_reminders` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentreminders) | Shared Lookup |
| `payment_term_installments` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentterminstallments) | System / Global |
| `payment_term_translations` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymenttermtranslations) | Shared Lookup |
| `payment_terms` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#paymentterms) | Shared Lookup |
| `payments` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#payments) | Shared Lookup |
| `receivable_collections` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#receivablecollections) | Tenant-Scoped |
| `treasury_alerts` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#treasuryalerts) | Tenant-Scoped |
| `working_capital_metrics` | [`Treasury, Banking & Cash Management`](./modules/09_treasury_and_banking.md#workingcapitalmetrics) | Tenant-Scoped |
| `billable_activities` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#billableactivities) | Shared Lookup |
| `construction_sites` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#constructionsites) | Shared Lookup |
| `progress_billings` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#progressbillings) | Shared Lookup |
| `project_audit_entries` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectauditentries) | Tenant-Scoped |
| `project_billing_events` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectbillingevents) | Tenant-Scoped |
| `project_budget_approvals` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectbudgetapprovals) | Tenant-Scoped |
| `project_budget_lines` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectbudgetlines) | Tenant-Scoped |
| `project_budget_versions` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectbudgetversions) | Tenant-Scoped |
| `project_budgets` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectbudgets) | Tenant-Scoped |
| `project_change_order_lines` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectchangeorderlines) | Tenant-Scoped |
| `project_change_orders` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectchangeorders) | Tenant-Scoped |
| `project_cost_allocations` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectcostallocations) | Tenant-Scoped |
| `project_cost_entries` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectcostentries) | Tenant-Scoped |
| `project_cost_snapshots` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectcostsnapshots) | Tenant-Scoped |
| `project_documents` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectdocuments) | Tenant-Scoped |
| `project_financial_summaries` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectfinancialsummaries) | Tenant-Scoped |
| `project_invoice_links` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectinvoicelinks) | Tenant-Scoped |
| `project_issues` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectissues) | Tenant-Scoped |
| `project_milestones` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectmilestones) | Tenant-Scoped |
| `project_notes` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectnotes) | Tenant-Scoped |
| `project_phases` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectphases) | Tenant-Scoped |
| `project_portfolios` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectportfolios) | Tenant-Scoped |
| `project_profitability_snapshots` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectprofitabilitysnapshots) | Tenant-Scoped |
| `project_resources` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectresources) | Tenant-Scoped |
| `project_revenue_recognition` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectrevenuerecognition) | Tenant-Scoped |
| `project_risks` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectrisks) | Tenant-Scoped |
| `project_status_histories` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectstatushistories) | Tenant-Scoped |
| `project_status_translations` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectstatustranslations) | Shared Lookup |
| `project_statuses` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectstatuses) | Shared Lookup |
| `project_task_assignments` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projecttaskassignments) | Tenant-Scoped |
| `project_task_dependencies` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projecttaskdependencies) | Tenant-Scoped |
| `project_tasks` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projecttasks) | Tenant-Scoped |
| `project_templates` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projecttemplates) | Tenant-Scoped |
| `project_timesheets` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projecttimesheets) | Tenant-Scoped |
| `project_variation_requests` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projectvariationrequests) | Tenant-Scoped |
| `projects` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#projects) | Tenant-Scoped |
| `resource_allocations` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#resourceallocations) | Tenant-Scoped |
| `resource_calendars` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#resourcecalendars) | Tenant-Scoped |
| `resource_capacity_profiles` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#resourcecapacityprofiles) | Tenant-Scoped |
| `task_status_translations` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#taskstatustranslations) | Shared Lookup |
| `task_statuses` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#taskstatuses) | Shared Lookup |
| `time_entries` | [`Projects, Job Costing & Timesheets`](./modules/10_projects_and_job_costing.md#timeentries) | Shared Lookup |
| `bills_of_materials` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#billsofmaterials) | Shared Lookup |
| `bom_items` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#bomitems) | System / Global |
| `mfg_bom_components` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgbomcomponents) | Tenant-Scoped |
| `mfg_boms` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgboms) | Tenant-Scoped |
| `mfg_engineering_change_orders` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgengineeringchangeorders) | Tenant-Scoped |
| `mfg_items` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgitems) | Tenant-Scoped |
| `mfg_labor_time_logs` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfglabortimelogs) | Tenant-Scoped |
| `mfg_machine_centers` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmachinecenters) | Tenant-Scoped |
| `mfg_machine_logs` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmachinelogs) | Tenant-Scoped |
| `mfg_mrp_peggings` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmrppeggings) | Tenant-Scoped |
| `mfg_mrp_planned_orders` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmrpplannedorders) | Tenant-Scoped |
| `mfg_mrp_runs` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmrpruns) | Tenant-Scoped |
| `mfg_mrp_shortages` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgmrpshortages) | Tenant-Scoped |
| `mfg_operations` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgoperations) | Tenant-Scoped |
| `mfg_production_costs` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgproductioncosts) | Tenant-Scoped |
| `mfg_production_order_lines` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgproductionorderlines) | Tenant-Scoped |
| `mfg_production_order_operations` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgproductionorderoperations) | Tenant-Scoped |
| `mfg_production_orders` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgproductionorders) | Tenant-Scoped |
| `mfg_production_versions` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgproductionversions) | Tenant-Scoped |
| `mfg_quality_characteristics` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgqualitycharacteristics) | Tenant-Scoped |
| `mfg_quality_inspections` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgqualityinspections) | Tenant-Scoped |
| `mfg_quality_non_conformances` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgqualitynonconformances) | Tenant-Scoped |
| `mfg_quality_plans` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgqualityplans) | Tenant-Scoped |
| `mfg_routings` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgroutings) | Tenant-Scoped |
| `mfg_shop_floor_executions` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgshopfloorexecutions) | Tenant-Scoped |
| `mfg_work_center_capacities` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgworkcentercapacities) | Tenant-Scoped |
| `mfg_work_centers` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#mfgworkcenters) | Tenant-Scoped |
| `production_order_stages` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#productionorderstages) | System / Global |
| `production_orders` | [`Manufacturing, Bills of Materials & MRP`](./modules/11_manufacturing_and_mrp.md#productionorders) | Shared Lookup |
| `eam_asset_assignments` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetassignments) | Tenant-Scoped |
| `eam_asset_categories` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetcategories) | Tenant-Scoped |
| `eam_asset_classes` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetclasses) | Tenant-Scoped |
| `eam_asset_components` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetcomponents) | Tenant-Scoped |
| `eam_asset_custodians` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetcustodians) | Tenant-Scoped |
| `eam_asset_disposals` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetdisposals) | Tenant-Scoped |
| `eam_asset_documents` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetdocuments) | Tenant-Scoped |
| `eam_asset_locations` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetlocations) | Tenant-Scoped |
| `eam_asset_relationships` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetrelationships) | Tenant-Scoped |
| `eam_asset_transfers` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassettransfers) | Tenant-Scoped |
| `eam_asset_valuations` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamassetvaluations) | Tenant-Scoped |
| `eam_depreciation_runs` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamdepreciationruns) | Tenant-Scoped |
| `eam_depreciation_schedules` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamdepreciationschedules) | Tenant-Scoped |
| `eam_fixed_assets` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamfixedassets) | Tenant-Scoped |
| `eam_maintenance_activities` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eammaintenanceactivities) | Tenant-Scoped |
| `eam_maintenance_plans` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eammaintenanceplans) | Tenant-Scoped |
| `eam_maintenance_work_orders` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eammaintenanceworkorders) | Tenant-Scoped |
| `eam_project_asset_allocations` | [`Enterprise Asset Management (EAM)`](./modules/12_enterprise_asset_management.md#eamprojectassetallocations) | Tenant-Scoped |
| `appointment_attendees` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#appointmentattendees) | Tenant-Scoped |
| `appointments` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#appointments) | Tenant-Scoped |
| `esm_business_hours_calendars` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmbusinesshourscalendars) | Tenant-Scoped |
| `esm_change_requests` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmchangerequests) | Tenant-Scoped |
| `esm_csat_surveys` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmcsatsurveys) | Tenant-Scoped |
| `esm_incidents` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmincidents) | Tenant-Scoped |
| `esm_knowledge_articles` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmknowledgearticles) | Tenant-Scoped |
| `esm_parts_consumptions` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmpartsconsumptions) | Tenant-Scoped |
| `esm_problems` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmproblems) | Tenant-Scoped |
| `esm_service_appointments` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmserviceappointments) | Tenant-Scoped |
| `esm_service_categories` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmservicecategories) | Tenant-Scoped |
| `esm_service_contracts` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmservicecontracts) | Tenant-Scoped |
| `esm_service_teams` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmserviceteams) | Tenant-Scoped |
| `esm_service_technicians` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmservicetechnicians) | Tenant-Scoped |
| `esm_service_visits` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmservicevisits) | Tenant-Scoped |
| `esm_sla_policies` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmslapolicies) | Tenant-Scoped |
| `esm_support_plans` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmsupportplans) | Tenant-Scoped |
| `esm_ticket_time_entries` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmtickettimeentries) | Tenant-Scoped |
| `esm_tickets` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmtickets) | Tenant-Scoped |
| `esm_work_order_items` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmworkorderitems) | Tenant-Scoped |
| `esm_work_orders` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#esmworkorders) | Tenant-Scoped |
| `portal_access_tokens` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#portalaccesstokens) | Tenant-Scoped |
| `portal_activity_logs` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#portalactivitylogs) | Tenant-Scoped |
| `service_report_lines` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#servicereportlines) | Tenant-Scoped |
| `service_report_signatures` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#servicereportsignatures) | Tenant-Scoped |
| `service_reports` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#servicereports) | Tenant-Scoped |
| `ticket_messages` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#ticketmessages) | Tenant-Scoped |
| `tickets` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#tickets) | Shared Lookup |
| `work_order_lines` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#workorderlines) | System / Global |
| `work_orders` | [`Enterprise Service Management (ESM) & Field Operations`](./modules/13_esm_and_field_service.md#workorders) | Shared Lookup |
| `employee_profiles` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#employeeprofiles) | Shared Lookup |
| `hr_attendance_records` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrattendancerecords) | Tenant-Scoped |
| `hr_business_units` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrbusinessunits) | Tenant-Scoped |
| `hr_certifications` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrcertifications) | Tenant-Scoped |
| `hr_cost_centers` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrcostcenters) | Tenant-Scoped |
| `hr_departments` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrdepartments) | Tenant-Scoped |
| `hr_employee_documents` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hremployeedocuments) | Tenant-Scoped |
| `hr_employee_lifecycle_events` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hremployeelifecycleevents) | Tenant-Scoped |
| `hr_employee_skills` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hremployeeskills) | Tenant-Scoped |
| `hr_employees` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hremployees) | Tenant-Scoped |
| `hr_employment_contracts` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hremploymentcontracts) | Tenant-Scoped |
| `hr_holiday_calendars` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrholidaycalendars) | Tenant-Scoped |
| `hr_job_grades` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrjobgrades) | Tenant-Scoped |
| `hr_leave_balances` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrleavebalances) | Tenant-Scoped |
| `hr_leave_requests` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrleaverequests) | Tenant-Scoped |
| `hr_leave_types` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrleavetypes) | Tenant-Scoped |
| `hr_performance_reviews` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrperformancereviews) | Tenant-Scoped |
| `hr_positions` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrpositions) | Tenant-Scoped |
| `hr_skills` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrskills) | Tenant-Scoped |
| `hr_teams` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrteams) | Tenant-Scoped |
| `hr_timesheets` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrtimesheets) | Tenant-Scoped |
| `hr_training_courses` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrtrainingcourses) | Tenant-Scoped |
| `hr_training_records` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#hrtrainingrecords) | Tenant-Scoped |
| `leave_balances` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#leavebalances) | Shared Lookup |
| `leave_requests` | [`Human Resources (HR) & Workforce Management`](./modules/14_human_resources_and_workforce.md#leaverequests) | Shared Lookup |
| `billing_schedule_items` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#billingscheduleitems) | System / Global |
| `billing_schedules` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#billingschedules) | Tenant-Scoped |
| `sub_billing_runs` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subbillingruns) | Tenant-Scoped |
| `sub_churn_predictions` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subchurnpredictions) | Tenant-Scoped |
| `sub_dunning_policies` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subdunningpolicies) | Tenant-Scoped |
| `sub_dunning_records` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subdunningrecords) | Tenant-Scoped |
| `sub_invoice_schedules` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subinvoiceschedules) | Tenant-Scoped |
| `sub_partner_commissions` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subpartnercommissions) | Tenant-Scoped |
| `sub_performance_obligations` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subperformanceobligations) | Tenant-Scoped |
| `sub_plan_features` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subplanfeatures) | Tenant-Scoped |
| `sub_plans` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subplans) | Tenant-Scoped |
| `sub_price_books` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subpricebooks) | Tenant-Scoped |
| `sub_pricing_tiers` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subpricingtiers) | Tenant-Scoped |
| `sub_products` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subproducts) | Tenant-Scoped |
| `sub_revenue_contracts` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subrevenuecontracts) | Tenant-Scoped |
| `sub_revenue_recognition_entries` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subrevenuerecognitionentries) | Tenant-Scoped |
| `sub_revenue_schedules` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subrevenueschedules) | Tenant-Scoped |
| `sub_subscription_items` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subsubscriptionitems) | Tenant-Scoped |
| `sub_subscription_versions` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subsubscriptionversions) | Tenant-Scoped |
| `sub_subscriptions` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subsubscriptions) | Tenant-Scoped |
| `sub_usage_aggregations` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subusageaggregations) | Tenant-Scoped |
| `sub_usage_events` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subusageevents) | Tenant-Scoped |
| `sub_usage_metrics` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subusagemetrics) | Tenant-Scoped |
| `subscription_items` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subscriptionitems) | System / Global |
| `subscription_runs` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subscriptionruns) | Shared Lookup |
| `subscriptions` | [`Subscription Management & Recurring Billing`](./modules/15_subscriptions_and_recurring.md#subscriptions) | Shared Lookup |
| `ecommerce_channels` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#ecommercechannels) | Shared Lookup |
| `ecommerce_mappings` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#ecommercemappings) | Shared Lookup |
| `loyalty_cards` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#loyaltycards) | Shared Lookup |
| `loyalty_transactions` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#loyaltytransactions) | Shared Lookup |
| `pos_sale_items` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#possaleitems) | System / Global |
| `pos_sales` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#possales) | Shared Lookup |
| `pos_sessions` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#possessions) | Shared Lookup |
| `pos_terminals` | [`Retail POS, Ecommerce & Loyalty`](./modules/16_retail_pos_and_ecommerce.md#posterminals) | Shared Lookup |
| `alerts` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#alerts) | Shared Lookup |
| `attachments` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#attachments) | Shared Lookup |
| `business_calendar_holidays` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#businesscalendarholidays) | Tenant-Scoped |
| `business_calendars` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#businesscalendars) | Tenant-Scoped |
| `carbon_ledger` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#carbonledger) | Tenant-Scoped |
| `conformity_certificates` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#conformitycertificates) | Shared Lookup |
| `countries` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#countries) | Shared Lookup |
| `country_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#countrytranslations) | Shared Lookup |
| `currency_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#currencytranslations) | Shared Lookup |
| `customs_declarations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#customsdeclarations) | Shared Lookup |
| `damage_inspections` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#damageinspections) | Shared Lookup |
| `discount_policies` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#discountpolicies) | Tenant-Scoped |
| `discount_policy_rules` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#discountpolicyrules) | System / Global |
| `document_emails` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#documentemails) | Shared Lookup |
| `document_events` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#documentevents) | Shared Lookup |
| `document_sequences` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#documentsequences) | Shared Lookup |
| `document_status_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#documentstatustranslations) | Shared Lookup |
| `document_statuses` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#documentstatuses) | Shared Lookup |
| `expense_attachments` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expenseattachments) | Tenant-Scoped |
| `expense_categories` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expensecategories) | Shared Lookup |
| `expense_category_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expensecategorytranslations) | Shared Lookup |
| `expense_items` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expenseitems) | System / Global |
| `expense_reports` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expensereports) | Shared Lookup |
| `expenses` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#expenses) | Tenant-Scoped |
| `forecast_scenarios` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#forecastscenarios) | Tenant-Scoped |
| `legal_cases` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#legalcases) | Shared Lookup |
| `lookup_categories` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#lookupcategories) | System / Global |
| `lookup_item_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#lookupitemtranslations) | Shared Lookup |
| `lookup_items` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#lookupitems) | Shared Lookup |
| `notification_type_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#notificationtypetranslations) | Shared Lookup |
| `notification_types` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#notificationtypes) | Shared Lookup |
| `quote_items` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#quoteitems) | Shared Lookup |
| `region_translations` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#regiontranslations) | Shared Lookup |
| `regions` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#regions) | Shared Lookup |
| `rental_bookings` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#rentalbookings) | Shared Lookup |
| `rental_contracts` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#rentalcontracts) | Shared Lookup |
| `rental_vehicles` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#rentalvehicles) | Shared Lookup |
| `tire_hotel_records` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#tirehotelrecords) | Shared Lookup |
| `units_of_measure` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#unitsofmeasure) | Shared Lookup |
| `vehicle_inspections` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#vehicleinspections) | Shared Lookup |
| `vehicles` | [`Master Reference Data & Specialized Verticals`](./modules/17_master_data_and_verticals.md#vehicles) | Shared Lookup |
