# Module Reference: Enterprise Service Management (ESM) & Field Operations

**Module ID**: `13_esm_and_field_service`  
**Tables Count**: `30`  
**Description**: ITSM ticketing, incident management, service catalogs, SLAs, customer portal, appointments, and work orders.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `appointment_attendees` | Tenant-Scoped | `id` | `undefined->tenants, undefined->appointments, undefined->users...` | `appointment_attendees_tenant_id_user_id_index, appointment_attendees_tenant_id_appointment_id_index` |
| `appointments` | Tenant-Scoped | `id` | `undefined->tenants, undefined->lookup_items, undefined->contacts...` | `appointments_tenant_id_ticket_id_index, appointments_tenant_id_status_id_index` |
| `esm_business_hours_calendars` | Tenant-Scoped | `id` | `undefined->tenants` | `esm_business_hours_calendars_company_id_index, esm_business_hours_calendars_code_index` |
| `esm_change_requests` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_problems, undefined->esm_tickets` | `esm_change_requests_workflow_instance_id_index, esm_change_requests_status_index` |
| `esm_csat_surveys` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_tickets, undefined->esm_work_orders` | `esm_csat_surveys_customer_id_index, esm_csat_surveys_company_id_index` |
| `esm_incidents` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_tickets` | `esm_incidents_workflow_instance_id_index, esm_incidents_status_index` |
| `esm_knowledge_articles` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_categories` | `esm_knowledge_articles_company_id_index, esm_knowledge_articles_article_number_index` |
| `esm_parts_consumptions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_work_orders` | `esm_parts_consumptions_warehouse_id_index, esm_parts_consumptions_product_id_index` |
| `esm_problems` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_categories` | `esm_problems_status_index, esm_problems_problem_number_index` |
| `esm_service_appointments` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_work_orders, undefined->esm_service_technicians` | `esm_service_appointments_status_index, esm_service_appointments_start_time_index` |
| `esm_service_categories` | Tenant-Scoped | `id` | `undefined->tenants` | `esm_service_categories_company_id_index, esm_service_categories_code_index` |
| `esm_service_contracts` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_support_plans` | `esm_service_contracts_workflow_instance_id_index, esm_service_contracts_status_index` |
| `esm_service_teams` | Tenant-Scoped | `id` | `undefined->tenants` | `esm_service_teams_lead_user_id_index, esm_service_teams_department_id_index` |
| `esm_service_technicians` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_teams` | `esm_service_technicians_user_id_index, esm_service_technicians_technician_number_index` |
| `esm_service_visits` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_appointments, undefined->esm_work_orders...` | `esm_service_visits_company_id_index` |
| `esm_sla_policies` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_categories, undefined->esm_support_plans` | `esm_sla_policies_company_id_index, esm_sla_policies_code_index` |
| `esm_support_plans` | Tenant-Scoped | `id` | `undefined->tenants` | `esm_support_plans_company_id_index, esm_support_plans_code_index` |
| `esm_ticket_time_entries` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_tickets, undefined->esm_service_technicians` | `esm_ticket_time_entries_company_id_index` |
| `esm_tickets` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_service_contracts, undefined->esm_service_categories...` | `esm_tickets_workflow_instance_id_index, esm_tickets_ticket_number_index` |
| `esm_work_order_items` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_work_orders` | `esm_work_order_items_product_id_index, esm_work_order_items_company_id_index` |
| `esm_work_orders` | Tenant-Scoped | `id` | `undefined->tenants, undefined->esm_tickets, undefined->esm_service_teams...` | `esm_work_orders_workflow_instance_id_index, esm_work_orders_work_order_number_index` |
| `portal_access_tokens` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts` | `portal_access_tokens_tenant_id_expires_at_index, portal_access_tokens_tenant_id_contact_id_index` |
| `portal_activity_logs` | Tenant-Scoped | `id` | `undefined->tenants, undefined->contacts, undefined->portal_access_tokens` | `portal_activity_logs_tenant_id_created_at_index, portal_activity_logs_tenant_id_contact_id_index` |
| `service_report_lines` | Tenant-Scoped | `id` | `undefined->tenants, undefined->service_reports, undefined->lookup_items...` | `service_report_lines_tenant_id_service_report_id_index, service_report_lines_tenant_id_line_type_id_index` |
| `service_report_signatures` | Tenant-Scoped | `id` | `undefined->tenants, undefined->service_reports, undefined->users...` | `service_report_signatures_tenant_id_service_report_id_index` |
| `service_reports` | Tenant-Scoped | `id` | `undefined->tenants, undefined->lookup_items, undefined->contacts...` | `service_reports_tenant_id_ticket_id_index, service_reports_tenant_id_technician_id_index` |
| `ticket_messages` | Tenant-Scoped | `id` | `undefined->tenants, undefined->tickets, undefined->users` | `ticket_messages_tenant_id_ticket_id_index, ticket_messages_tenant_id_is_internal_index` |
| `tickets` | Shared Lookup | `id` | `undefined->tenants, undefined->contacts, undefined->users` | `tickets_tenant_id_status_index, tickets_tenant_id_client_id_idx` |
| `work_order_lines` | System / Global | `id` | `undefined->work_orders` | `work_order_lines_product_id_index` |
| `work_orders` | Shared Lookup | `id` | `undefined->users, undefined->contacts, undefined->tickets...` | `work_orders_work_order_number_index, work_orders_tenant_id_technician_user_id_idx` |

---

## Detailed Entity Schema & Data Dictionary

### `appointment_attendees`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `appointment_id` -> `appointments(id)`
  - `user_id` -> `users(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `appointment_attendees_tenant_id_user_id_index` (Unique: No)
  - `appointment_attendees_tenant_id_appointment_id_index` (Unique: No)
  - `sqlite_autoindex_appointment_attendees_2` (Unique: Yes)
  - `sqlite_autoindex_appointment_attendees_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `appointment_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for appointment |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `role` | `VARCHAR(255)` | No | `'lead'` | Operational entity attribute |
| `is_organizer` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `status` | `VARCHAR(255)` | No | `'accepted'` | State machine status indicator |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `appointments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `status_id` -> `lookup_items(id)`
  - `contact_id` -> `contacts(id)`
  - `ticket_id` -> `tickets(id)`
  - `service_report_id` -> `service_reports(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `appointments_tenant_id_ticket_id_index` (Unique: No)
  - `appointments_tenant_id_status_id_index` (Unique: No)
  - `appointments_tenant_id_starts_at_ends_at_index` (Unique: No)
  - `appointments_tenant_id_service_report_id_index` (Unique: No)
  - `appointments_tenant_id_is_portal_visible_index` (Unique: No)
  - `appointments_tenant_id_contact_id_index` (Unique: No)
  - `sqlite_autoindex_appointments_2` (Unique: Yes)
  - `sqlite_autoindex_appointments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `appointment_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for status |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `service_report_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for service_report |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `starts_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `ends_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `all_day` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `latitude` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `longitude` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `estimated_travel_minutes` | `INTEGER` | No | `0` | Operational entity attribute |
| `estimated_duration_minutes` | `INTEGER` | No | `60` | Operational entity attribute |
| `technician_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `customer_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_portal_visible` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `reminder_sent_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `confirmed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `cancelled_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `cancellation_reason` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_business_hours_calendars`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `esm_business_hours_calendars_company_id_index` (Unique: No)
  - `esm_business_hours_calendars_code_index` (Unique: No)
  - `sqlite_autoindex_esm_business_hours_calendars_2` (Unique: Yes)
  - `sqlite_autoindex_esm_business_hours_calendars_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `timezone` | `VARCHAR(255)` | No | `'UTC'` | Operational entity attribute |
| `weekly_schedule` | `TEXT` | Yes | NULL | Operational entity attribute |
| `holidays` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_change_requests`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `problem_id` -> `esm_problems(id)`
  - `ticket_id` -> `esm_tickets(id)`
- **Indexes & Constraints**:
  - `esm_change_requests_workflow_instance_id_index` (Unique: No)
  - `esm_change_requests_status_index` (Unique: No)
  - `esm_change_requests_company_id_index` (Unique: No)
  - `esm_change_requests_change_number_index` (Unique: No)
  - `sqlite_autoindex_esm_change_requests_2` (Unique: Yes)
  - `sqlite_autoindex_esm_change_requests_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `problem_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for problem |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `change_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `change_type` | `VARCHAR(255)` | No | `'normal'` | Operational entity attribute |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `risk_level` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `impact_assessment` | `TEXT` | No | NULL | Operational entity attribute |
| `implementation_plan` | `TEXT` | No | NULL | Operational entity attribute |
| `rollback_plan` | `TEXT` | No | NULL | Operational entity attribute |
| `scheduled_start_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `scheduled_end_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `implemented_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `validated_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `cab_decision` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `cab_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `cab_reviewers` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_csat_surveys`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ticket_id` -> `esm_tickets(id)`
  - `work_order_id` -> `esm_work_orders(id)`
- **Indexes & Constraints**:
  - `esm_csat_surveys_customer_id_index` (Unique: No)
  - `esm_csat_surveys_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_csat_surveys_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `work_order_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for work_order |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `score` | `INTEGER` | No | `5` | Operational entity attribute |
| `sentiment` | `VARCHAR(255)` | No | `'positive'` | Operational entity attribute |
| `feedback` | `TEXT` | Yes | NULL | Operational entity attribute |
| `responded_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_incidents`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ticket_id` -> `esm_tickets(id)`
- **Indexes & Constraints**:
  - `esm_incidents_workflow_instance_id_index` (Unique: No)
  - `esm_incidents_status_index` (Unique: No)
  - `esm_incidents_priority_index` (Unique: No)
  - `esm_incidents_incident_number_index` (Unique: No)
  - `esm_incidents_company_id_index` (Unique: No)
  - `esm_incidents_asset_id_index` (Unique: No)
  - `sqlite_autoindex_esm_incidents_2` (Unique: Yes)
  - `sqlite_autoindex_esm_incidents_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset |
| `incident_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `severity` | `VARCHAR(255)` | No | `'P3'` | Operational entity attribute |
| `impact` | `VARCHAR(255)` | No | `'moderate'` | Operational entity attribute |
| `urgency` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'P3'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'identified'` | State machine status indicator |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `summary` | `TEXT` | No | NULL | Operational entity attribute |
| `reported_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `contained_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `resolved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `closed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `workaround` | `TEXT` | Yes | NULL | Operational entity attribute |
| `post_mortem_summary` | `TEXT` | Yes | NULL | Operational entity attribute |
| `post_mortem_completed` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `timeline` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_knowledge_articles`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `category_id` -> `esm_service_categories(id)`
- **Indexes & Constraints**:
  - `esm_knowledge_articles_company_id_index` (Unique: No)
  - `esm_knowledge_articles_article_number_index` (Unique: No)
  - `sqlite_autoindex_esm_knowledge_articles_2` (Unique: Yes)
  - `sqlite_autoindex_esm_knowledge_articles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for category |
| `article_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `summary` | `TEXT` | Yes | NULL | Operational entity attribute |
| `content` | `TEXT` | No | NULL | Operational entity attribute |
| `tags` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_published` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `views_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `helpful_count` | `INTEGER` | No | `0` | Operational entity attribute |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_parts_consumptions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `work_order_id` -> `esm_work_orders(id)`
- **Indexes & Constraints**:
  - `esm_parts_consumptions_warehouse_id_index` (Unique: No)
  - `esm_parts_consumptions_product_id_index` (Unique: No)
  - `esm_parts_consumptions_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_parts_consumptions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `product_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for product |
| `warehouse_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for warehouse |
| `quantity` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `lot_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `serial_numbers` | `TEXT` | Yes | NULL | Unique business identification code or document number |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_problems`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `category_id` -> `esm_service_categories(id)`
- **Indexes & Constraints**:
  - `esm_problems_status_index` (Unique: No)
  - `esm_problems_problem_number_index` (Unique: No)
  - `esm_problems_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_problems_2` (Unique: Yes)
  - `sqlite_autoindex_esm_problems_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for category |
| `problem_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'under_investigation'` | State machine status indicator |
| `root_cause` | `TEXT` | Yes | NULL | Operational entity attribute |
| `workaround` | `TEXT` | Yes | NULL | Operational entity attribute |
| `permanent_solution` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_known_error` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `resolved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `closed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `linked_incident_ids` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_appointments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `work_order_id` -> `esm_work_orders(id)`
  - `technician_id` -> `esm_service_technicians(id)`
- **Indexes & Constraints**:
  - `esm_service_appointments_status_index` (Unique: No)
  - `esm_service_appointments_start_time_index` (Unique: No)
  - `esm_service_appointments_end_time_index` (Unique: No)
  - `esm_service_appointments_customer_id_index` (Unique: No)
  - `esm_service_appointments_company_id_index` (Unique: No)
  - `esm_service_appointments_appointment_number_index` (Unique: No)
  - `sqlite_autoindex_esm_service_appointments_2` (Unique: Yes)
  - `sqlite_autoindex_esm_service_appointments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `appointment_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `technician_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for technician |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `start_time` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `end_time` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'scheduled'` | State machine status indicator |
| `route_order` | `INTEGER` | No | `1` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_categories`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `esm_service_categories_company_id_index` (Unique: No)
  - `esm_service_categories_code_index` (Unique: No)
  - `sqlite_autoindex_esm_service_categories_2` (Unique: Yes)
  - `sqlite_autoindex_esm_service_categories_1` (Unique: Yes)

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
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_contracts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `support_plan_id` -> `esm_support_plans(id)`
- **Indexes & Constraints**:
  - `esm_service_contracts_workflow_instance_id_index` (Unique: No)
  - `esm_service_contracts_status_index` (Unique: No)
  - `esm_service_contracts_customer_id_index` (Unique: No)
  - `esm_service_contracts_contract_number_index` (Unique: No)
  - `esm_service_contracts_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_service_contracts_2` (Unique: Yes)
  - `sqlite_autoindex_esm_service_contracts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `support_plan_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for support_plan |
| `contract_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `renewal_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `annual_value` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `auto_renew` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `terms` | `TEXT` | Yes | NULL | Operational entity attribute |
| `entitlements` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_teams`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `esm_service_teams_lead_user_id_index` (Unique: No)
  - `esm_service_teams_department_id_index` (Unique: No)
  - `esm_service_teams_company_id_index` (Unique: No)
  - `esm_service_teams_code_index` (Unique: No)
  - `sqlite_autoindex_esm_service_teams_2` (Unique: Yes)
  - `sqlite_autoindex_esm_service_teams_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `lead_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lead_user |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_technicians`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `team_id` -> `esm_service_teams(id)`
- **Indexes & Constraints**:
  - `esm_service_technicians_user_id_index` (Unique: No)
  - `esm_service_technicians_technician_number_index` (Unique: No)
  - `esm_service_technicians_employee_id_index` (Unique: No)
  - `esm_service_technicians_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_service_technicians_2` (Unique: Yes)
  - `sqlite_autoindex_esm_service_technicians_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for employee |
| `team_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for team |
| `technician_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `first_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `last_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `email` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `skill_level` | `VARCHAR(255)` | No | `'intermediate'` | Operational entity attribute |
| `hourly_cost_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `hourly_billable_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_available` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `current_status` | `VARCHAR(255)` | No | `'available'` | State machine status indicator |
| `skills` | `TEXT` | Yes | NULL | Operational entity attribute |
| `certifications` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_service_visits`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `appointment_id` -> `esm_service_appointments(id)`
  - `work_order_id` -> `esm_work_orders(id)`
  - `technician_id` -> `esm_service_technicians(id)`
- **Indexes & Constraints**:
  - `esm_service_visits_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_service_visits_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `appointment_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for appointment |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `technician_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for technician |
| `check_in_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `check_out_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `duration_minutes` | `INTEGER` | No | `0` | Operational entity attribute |
| `customer_present` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `is_successful` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `visit_summary` | `TEXT` | Yes | NULL | Operational entity attribute |
| `location_check_in` | `TEXT` | Yes | NULL | Operational entity attribute |
| `location_check_out` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_sla_policies`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `service_category_id` -> `esm_service_categories(id)`
  - `support_plan_id` -> `esm_support_plans(id)`
- **Indexes & Constraints**:
  - `esm_sla_policies_company_id_index` (Unique: No)
  - `esm_sla_policies_code_index` (Unique: No)
  - `sqlite_autoindex_esm_sla_policies_2` (Unique: Yes)
  - `sqlite_autoindex_esm_sla_policies_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `service_category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for service_category |
| `support_plan_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for support_plan |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `response_time_minutes` | `INTEGER` | No | `240` | Operational entity attribute |
| `resolution_time_minutes` | `INTEGER` | No | `1440` | Operational entity attribute |
| `escalation_time_minutes` | `INTEGER` | No | `120` | Operational entity attribute |
| `business_hours_only` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_support_plans`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `esm_support_plans_company_id_index` (Unique: No)
  - `esm_support_plans_code_index` (Unique: No)
  - `sqlite_autoindex_esm_support_plans_2` (Unique: Yes)
  - `sqlite_autoindex_esm_support_plans_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `tier` | `VARCHAR(255)` | No | `'standard'` | Operational entity attribute |
| `response_time_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `resolution_time_hours` | `NUMERIC(16, 4)` | No | `24` | Operational entity attribute |
| `price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `billing_cycle` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_ticket_time_entries`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ticket_id` -> `esm_tickets(id)`
  - `technician_id` -> `esm_service_technicians(id)`
- **Indexes & Constraints**:
  - `esm_ticket_time_entries_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_ticket_time_entries_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `ticket_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for ticket |
| `technician_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for technician |
| `work_date` | `DATE` | No | NULL | Operational entity attribute |
| `hours` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `hourly_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_charge` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_tickets`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `service_contract_id` -> `esm_service_contracts(id)`
  - `category_id` -> `esm_service_categories(id)`
  - `assigned_team_id` -> `esm_service_teams(id)`
  - `assigned_technician_id` -> `esm_service_technicians(id)`
  - `knowledge_article_id` -> `esm_knowledge_articles(id)`
- **Indexes & Constraints**:
  - `esm_tickets_workflow_instance_id_index` (Unique: No)
  - `esm_tickets_ticket_number_index` (Unique: No)
  - `esm_tickets_status_index` (Unique: No)
  - `esm_tickets_response_due_at_index` (Unique: No)
  - `esm_tickets_resolution_due_at_index` (Unique: No)
  - `esm_tickets_project_id_index` (Unique: No)
  - `esm_tickets_priority_index` (Unique: No)
  - `esm_tickets_customer_id_index` (Unique: No)
  - `esm_tickets_contact_id_index` (Unique: No)
  - `esm_tickets_company_id_index` (Unique: No)
  - `esm_tickets_asset_id_index` (Unique: No)
  - `sqlite_autoindex_esm_tickets_2` (Unique: Yes)
  - `sqlite_autoindex_esm_tickets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `contact_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for contact |
| `service_contract_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for service_contract |
| `asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `category_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for category |
| `ticket_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `type` | `VARCHAR(255)` | No | `'incident'` | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `source` | `VARCHAR(255)` | No | `'portal'` | Operational entity attribute |
| `subject` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | No | NULL | Operational entity attribute |
| `assigned_team_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_team |
| `assigned_technician_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_technician |
| `response_due_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `resolution_due_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `first_responded_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `resolved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `closed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `is_escalated` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `escalation_level` | `INTEGER` | No | `0` | Operational entity attribute |
| `resolution_summary` | `TEXT` | Yes | NULL | Operational entity attribute |
| `root_cause` | `TEXT` | Yes | NULL | Operational entity attribute |
| `knowledge_article_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for knowledge_article |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `csat_score` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `custom_fields` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_work_order_items`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `work_order_id` -> `esm_work_orders(id)`
- **Indexes & Constraints**:
  - `esm_work_order_items_product_id_index` (Unique: No)
  - `esm_work_order_items_company_id_index` (Unique: No)
  - `sqlite_autoindex_esm_work_order_items_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `item_type` | `VARCHAR(255)` | No | `'labor'` | Operational entity attribute |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `esm_work_orders`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ticket_id` -> `esm_tickets(id)`
  - `service_team_id` -> `esm_service_teams(id)`
  - `assigned_technician_id` -> `esm_service_technicians(id)`
- **Indexes & Constraints**:
  - `esm_work_orders_workflow_instance_id_index` (Unique: No)
  - `esm_work_orders_work_order_number_index` (Unique: No)
  - `esm_work_orders_status_index` (Unique: No)
  - `esm_work_orders_scheduled_start_index` (Unique: No)
  - `esm_work_orders_scheduled_end_index` (Unique: No)
  - `esm_work_orders_project_id_index` (Unique: No)
  - `esm_work_orders_invoice_id_index` (Unique: No)
  - `esm_work_orders_customer_id_index` (Unique: No)
  - `esm_work_orders_company_id_index` (Unique: No)
  - `esm_work_orders_asset_id_index` (Unique: No)
  - `sqlite_autoindex_esm_work_orders_2` (Unique: Yes)
  - `sqlite_autoindex_esm_work_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `customer_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for customer |
| `asset_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for asset |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `service_team_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for service_team |
| `assigned_technician_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_technician |
| `work_order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `work_type` | `VARCHAR(255)` | No | `'corrective'` | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `scheduled_start` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `scheduled_end` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `actual_start` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `actual_end` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `labor_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `material_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `expense_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_billable_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `is_invoiced` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |
| `customer_signed` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `signed_by_name` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `signature_data` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `resolution_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `location` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `portal_access_tokens`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
- **Indexes & Constraints**:
  - `portal_access_tokens_tenant_id_expires_at_index` (Unique: No)
  - `portal_access_tokens_tenant_id_contact_id_index` (Unique: No)
  - `portal_access_tokens_scope_type_scope_id_index` (Unique: No)
  - `sqlite_autoindex_portal_access_tokens_2` (Unique: Yes)
  - `sqlite_autoindex_portal_access_tokens_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `token_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `token_type` | `VARCHAR(255)` | No | `'dashboard'` | Operational entity attribute |
| `scope_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `scope_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for scope |
| `expires_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `last_accessed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `is_single_use` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `used_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `revoked_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `portal_activity_logs`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `contact_id` -> `contacts(id)`
  - `portal_access_token_id` -> `portal_access_tokens(id)`
- **Indexes & Constraints**:
  - `portal_activity_logs_tenant_id_created_at_index` (Unique: No)
  - `portal_activity_logs_tenant_id_contact_id_index` (Unique: No)
  - `portal_activity_logs_tenant_id_action_index` (Unique: No)
  - `sqlite_autoindex_portal_activity_logs_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `portal_access_token_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for portal_access_token |
| `action` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `subject_type` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `subject_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for subject |
| `ip_address` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `user_agent` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | No | NULL | Timestamp of record creation |

---

### `service_report_lines`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `service_report_id` -> `service_reports(id)`
  - `line_type_id` -> `lookup_items(id)`
  - `item_id` -> `products(id)`
  - `vat_code_id` -> `vat_codes(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `service_report_lines_tenant_id_service_report_id_index` (Unique: No)
  - `service_report_lines_tenant_id_line_type_id_index` (Unique: No)
  - `service_report_lines_tenant_id_item_id_index` (Unique: No)
  - `sqlite_autoindex_service_report_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `service_report_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for service_report |
| `line_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for line_type |
| `item_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for item |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_of_measure` | `VARCHAR(255)` | No | `'hours'` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `discount_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `vat_code_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for vat_code |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `line_net` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `line_tax` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_billable` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `service_report_signatures`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `service_report_id` -> `service_reports(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `service_report_signatures_tenant_id_service_report_id_index` (Unique: No)
  - `sqlite_autoindex_service_report_signatures_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `service_report_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for service_report |
| `signer_type` | `VARCHAR(255)` | No | `'customer'` | Operational entity attribute |
| `signer_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `signer_role` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `signer_email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `signature_path` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `signature_hash` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `ip_address` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `user_agent` | `TEXT` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | No | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `service_reports`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `status_id` -> `lookup_items(id)`
  - `contact_id` -> `contacts(id)`
  - `ticket_id` -> `tickets(id)`
  - `technician_id` -> `users(id)`
  - `created_by` -> `users(id)`
  - `updated_by` -> `users(id)`
- **Indexes & Constraints**:
  - `service_reports_tenant_id_ticket_id_index` (Unique: No)
  - `service_reports_tenant_id_technician_id_index` (Unique: No)
  - `service_reports_tenant_id_status_id_index` (Unique: No)
  - `service_reports_tenant_id_report_date_index` (Unique: No)
  - `service_reports_tenant_id_project_id_index` (Unique: No)
  - `service_reports_tenant_id_contact_id_index` (Unique: No)
  - `service_reports_project_id_index` (Unique: No)
  - `sqlite_autoindex_service_reports_2` (Unique: Yes)
  - `sqlite_autoindex_service_reports_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `report_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `status_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for status |
| `contact_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for contact |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `technician_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for technician |
| `report_date` | `DATE` | No | NULL | Operational entity attribute |
| `time_start` | `TIME` | Yes | NULL | Operational entity attribute |
| `time_end` | `TIME` | Yes | NULL | Operational entity attribute |
| `total_hours` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `travel_distance_km` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `site_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `customer_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `internal_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `total_net` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_tax` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_gross` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `is_portal_visible` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `invoiced_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `updated_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `ticket_messages`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `ticket_id` -> `tickets(id)`
  - `author_id` -> `users(id)`
- **Indexes & Constraints**:
  - `ticket_messages_tenant_id_ticket_id_index` (Unique: No)
  - `ticket_messages_tenant_id_is_internal_index` (Unique: No)
  - `sqlite_autoindex_ticket_messages_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `ticket_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for ticket |
| `author_type` | `VARCHAR(255)` | No | `'customer'` | Operational entity attribute |
| `author_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for author |
| `author_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `message` | `TEXT` | No | NULL | Operational entity attribute |
| `is_internal` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `tickets`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `client_id` -> `contacts(id)`
  - `assigned_to_user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `tickets_tenant_id_status_index` (Unique: No)
  - `tickets_tenant_id_client_id_idx` (Unique: No)
  - `tickets_tenant_id_assigned_to_user_id_idx` (Unique: No)
  - `tickets_status_index` (Unique: No)
  - `tickets_sla_due_at_index` (Unique: No)
  - `tickets_priority_index` (Unique: No)
  - `sqlite_autoindex_tickets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `subject` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `priority` | `VARCHAR(255)` | No | `'medium'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'open'` | State machine status indicator |
| `assigned_to_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for assigned_to_user |
| `sla_due_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `work_order_lines`

- **Operational Scope**: System / Global
- **Foreign Key References**:
  - `work_order_id` -> `work_orders(id)`
- **Indexes & Constraints**:
  - `work_order_lines_product_id_index` (Unique: No)
  - `sqlite_autoindex_work_order_lines_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `work_order_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for work_order |
| `type` | `VARCHAR(255)` | No | `'labor'` | Operational entity attribute |
| `product_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for product |
| `description` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `quantity` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `unit_price` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `tax_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `line_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `work_orders`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `technician_user_id` -> `users(id)`
  - `client_id` -> `contacts(id)`
  - `ticket_id` -> `tickets(id)`
  - `tenant_id` -> `tenants(id)`
  - `invoice_id` -> `invoices(id)`
- **Indexes & Constraints**:
  - `work_orders_work_order_number_index` (Unique: No)
  - `work_orders_tenant_id_technician_user_id_idx` (Unique: No)
  - `work_orders_tenant_id_status_idx` (Unique: No)
  - `work_orders_tenant_id_date_idx` (Unique: No)
  - `work_orders_tenant_id_client_id_idx` (Unique: No)
  - `work_orders_status_index` (Unique: No)
  - `sqlite_autoindex_work_orders_2` (Unique: Yes)
  - `sqlite_autoindex_work_orders_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `ticket_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for ticket |
| `client_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for client |
| `technician_user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for technician_user |
| `work_order_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `date` | `DATE` | No | NULL | Operational entity attribute |
| `labor_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `parts_total` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `client_signature_path` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `client_signed_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `signed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |
| `started_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `ended_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `intervention_address` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `invoice_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for invoice |

---

