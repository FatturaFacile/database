# Module Reference: Human Resources (HR) & Workforce Management

**Module ID**: `14_human_resources_and_workforce`  
**Tables Count**: `25`  
**Description**: Employee profiles, organizational hierarchies, leave tracking, certifications, job roles, and payroll metadata.

---

## Table Summary

| Table Name | Scope | Primary Key | Foreign Keys | Key Indexes |
| :--- | :--- | :--- | :--- | :--- |
| `employee_profiles` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `employee_profiles_social_security_number_index, employee_profiles_is_cross_border_commuter_index` |
| `hr_attendance_records` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_attendance_records_work_date_index, hr_attendance_records_status_index` |
| `hr_business_units` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_business_units_head_employee_id_index, hr_business_units_company_id_index` |
| `hr_certifications` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_certifications_status_index, hr_certifications_expiry_date_index` |
| `hr_cost_centers` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_cost_centers_company_id_index, hr_cost_centers_code_index` |
| `hr_departments` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_departments_parent_id_index, hr_departments_manager_employee_id_index` |
| `hr_employee_documents` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_employee_documents_expiry_date_index` |
| `hr_employee_lifecycle_events` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_employee_lifecycle_events_workflow_instance_id_index, hr_employee_lifecycle_events_event_type_index` |
| `hr_employee_skills` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees, undefined->hr_skills` | `PRIMARY` |
| `hr_employees` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_departments, undefined->hr_teams...` | `hr_employees_workflow_instance_id_index, hr_employees_work_email_index` |
| `hr_employment_contracts` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_employment_contracts_workflow_instance_id_index, hr_employment_contracts_status_index` |
| `hr_holiday_calendars` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_holiday_calendars_year_index, hr_holiday_calendars_company_id_index` |
| `hr_job_grades` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_job_grades_company_id_index, hr_job_grades_code_index` |
| `hr_leave_balances` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees, undefined->hr_leave_types` | `hr_leave_balances_fiscal_year_index, hr_leave_balances_company_id_index` |
| `hr_leave_requests` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees, undefined->hr_leave_types` | `hr_leave_requests_workflow_instance_id_index, hr_leave_requests_status_index` |
| `hr_leave_types` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_leave_types_company_id_index, hr_leave_types_code_index` |
| `hr_performance_reviews` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_performance_reviews_workflow_instance_id_index, hr_performance_reviews_status_index` |
| `hr_positions` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_departments, undefined->hr_job_grades` | `hr_positions_successor_employee_id_index, hr_positions_reports_to_position_id_index` |
| `hr_skills` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_skills_company_id_index, hr_skills_code_index` |
| `hr_teams` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_departments` | `hr_teams_lead_employee_id_index, hr_teams_company_id_index` |
| `hr_timesheets` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees` | `hr_timesheets_workflow_instance_id_index, hr_timesheets_work_date_index` |
| `hr_training_courses` | Tenant-Scoped | `id` | `undefined->tenants` | `hr_training_courses_course_code_index, hr_training_courses_company_id_index` |
| `hr_training_records` | Tenant-Scoped | `id` | `undefined->tenants, undefined->hr_employees, undefined->hr_training_courses` | `hr_training_records_workflow_instance_id_index, hr_training_records_status_index` |
| `leave_balances` | Shared Lookup | `id` | `undefined->tenants, undefined->users` | `leave_balances_year_index` |
| `leave_requests` | Shared Lookup | `id` | `undefined->tenants, undefined->users, undefined->users` | `leave_requests_type_index, leave_requests_status_index` |

---

## Detailed Entity Schema & Data Dictionary

### `employee_profiles`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `employee_profiles_social_security_number_index` (Unique: No)
  - `employee_profiles_is_cross_border_commuter_index` (Unique: No)
  - `sqlite_autoindex_employee_profiles_2` (Unique: Yes)
  - `sqlite_autoindex_employee_profiles_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `is_cross_border_commuter` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `social_security_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `swiss_cantonal_tax_rate` | `NUMERIC(16, 4)` | Yes | NULL | Monetary or financial decimal quantity |
| `inps_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `job_title` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `department` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `hire_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `termination_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `base_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'CHF'` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_attendance_records`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_attendance_records_work_date_index` (Unique: No)
  - `hr_attendance_records_status_index` (Unique: No)
  - `hr_attendance_records_project_id_index` (Unique: No)
  - `hr_attendance_records_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_attendance_records_2` (Unique: Yes)
  - `sqlite_autoindex_hr_attendance_records_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `work_date` | `DATE` | No | NULL | Operational entity attribute |
| `clock_in_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `clock_out_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `break_minutes` | `INTEGER` | No | `0` | Operational entity attribute |
| `regular_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `overtime_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `night_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `holiday_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'present'` | State machine status indicator |
| `source` | `VARCHAR(255)` | No | `'web_portal'` | Operational entity attribute |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_business_units`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_business_units_head_employee_id_index` (Unique: No)
  - `hr_business_units_company_id_index` (Unique: No)
  - `hr_business_units_code_index` (Unique: No)
  - `sqlite_autoindex_hr_business_units_2` (Unique: Yes)
  - `sqlite_autoindex_hr_business_units_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `head_employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for head_employee |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_certifications`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_certifications_status_index` (Unique: No)
  - `hr_certifications_expiry_date_index` (Unique: No)
  - `hr_certifications_course_id_index` (Unique: No)
  - `hr_certifications_company_id_index` (Unique: No)
  - `hr_certifications_code_index` (Unique: No)
  - `hr_certifications_certificate_number_index` (Unique: No)
  - `sqlite_autoindex_hr_certifications_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for employee |
| `course_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for course |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `certificate_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `issuing_authority` | `VARCHAR(255)` | No | `'National Safety Board'` | Operational entity attribute |
| `issue_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `expiry_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `is_mandatory` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `renewal_alert_sent_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_cost_centers`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_cost_centers_company_id_index` (Unique: No)
  - `hr_cost_centers_code_index` (Unique: No)
  - `hr_cost_centers_business_unit_id_index` (Unique: No)
  - `sqlite_autoindex_hr_cost_centers_2` (Unique: Yes)
  - `sqlite_autoindex_hr_cost_centers_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `business_unit_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for business_unit |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `gl_expense_account_code` | `VARCHAR(255)` | No | `'6100'` | Unique business identification code or document number |
| `gl_accrual_account_code` | `VARCHAR(255)` | No | `'2250'` | Unique business identification code or document number |
| `annual_budget` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_departments`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_departments_parent_id_index` (Unique: No)
  - `hr_departments_manager_employee_id_index` (Unique: No)
  - `hr_departments_cost_center_id_index` (Unique: No)
  - `hr_departments_company_id_index` (Unique: No)
  - `hr_departments_code_index` (Unique: No)
  - `hr_departments_business_unit_id_index` (Unique: No)
  - `sqlite_autoindex_hr_departments_2` (Unique: Yes)
  - `sqlite_autoindex_hr_departments_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `parent_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for parent |
| `business_unit_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for business_unit |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `manager_employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for manager_employee |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_employee_documents`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_employee_documents_expiry_date_index` (Unique: No)
  - `sqlite_autoindex_hr_employee_documents_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `document_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `file_path` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `issue_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `expiry_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `is_confidential` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `status` | `VARCHAR(255)` | No | `'valid'` | State machine status indicator |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_employee_lifecycle_events`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_employee_lifecycle_events_workflow_instance_id_index` (Unique: No)
  - `hr_employee_lifecycle_events_event_type_index` (Unique: No)
  - `hr_employee_lifecycle_events_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_employee_lifecycle_events_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `event_type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `effective_date` | `DATE` | No | NULL | Operational entity attribute |
| `from_status` | `VARCHAR(255)` | Yes | NULL | State machine status indicator |
| `to_status` | `VARCHAR(255)` | No | NULL | State machine status indicator |
| `from_department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_department |
| `to_department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_department |
| `from_position_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_position |
| `to_position_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_position |
| `from_job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for from_job_grade |
| `to_job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for to_job_grade |
| `from_salary` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `to_salary` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `initiated_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for initiated_by_user |
| `approved_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for approved_by_user |
| `snapshot` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_employee_skills`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
  - `skill_id` -> `hr_skills(id)`
- **Indexes & Constraints**:
  - `sqlite_autoindex_hr_employee_skills_2` (Unique: Yes)
  - `sqlite_autoindex_hr_employee_skills_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `skill_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for skill |
| `proficiency_level` | `INTEGER` | No | `3` | Operational entity attribute |
| `verified_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for verified_by_user |
| `verified_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_employees`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `department_id` -> `hr_departments(id)`
  - `team_id` -> `hr_teams(id)`
  - `business_unit_id` -> `hr_business_units(id)`
  - `cost_center_id` -> `hr_cost_centers(id)`
  - `position_id` -> `hr_positions(id)`
  - `job_grade_id` -> `hr_job_grades(id)`
- **Indexes & Constraints**:
  - `hr_employees_workflow_instance_id_index` (Unique: No)
  - `hr_employees_work_email_index` (Unique: No)
  - `hr_employees_user_id_index` (Unique: No)
  - `hr_employees_tax_code_index` (Unique: No)
  - `hr_employees_manager_id_index` (Unique: No)
  - `hr_employees_employment_status_index` (Unique: No)
  - `hr_employees_employee_number_index` (Unique: No)
  - `hr_employees_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_employees_2` (Unique: Yes)
  - `sqlite_autoindex_hr_employees_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for user |
| `employee_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `first_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `last_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `full_name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `work_email` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `personal_email` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `phone` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `birth_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `gender` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `nationality` | `VARCHAR(255)` | No | `'IT'` | Operational entity attribute |
| `tax_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `social_security_number` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `team_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for team |
| `business_unit_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for business_unit |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `position_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for position |
| `job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for job_grade |
| `manager_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for manager |
| `employment_status` | `VARCHAR(255)` | No | `'onboarding'` | State machine status indicator |
| `employment_type` | `VARCHAR(255)` | No | `'full_time'` | Operational entity attribute |
| `hire_date` | `DATE` | No | NULL | Operational entity attribute |
| `probation_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `confirmation_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `termination_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `termination_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `rehire_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `base_annual_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_cost_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `fte_ratio` | `NUMERIC(16, 4)` | No | `1` | Operational entity attribute |
| `work_schedule_code` | `VARCHAR(255)` | No | `'STD-40H'` | Unique business identification code or document number |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `approval_status` | `VARCHAR(255)` | No | `'approved'` | State machine status indicator |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `emergency_contact` | `TEXT` | Yes | NULL | Operational entity attribute |
| `equipment_assigned` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_employment_contracts`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_employment_contracts_workflow_instance_id_index` (Unique: No)
  - `hr_employment_contracts_status_index` (Unique: No)
  - `hr_employment_contracts_job_grade_id_index` (Unique: No)
  - `hr_employment_contracts_contract_number_index` (Unique: No)
  - `hr_employment_contracts_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_employment_contracts_2` (Unique: Yes)
  - `sqlite_autoindex_hr_employment_contracts_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `contract_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `contract_type` | `VARCHAR(255)` | No | `'permanent'` | Operational entity attribute |
| `collective_agreement` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `job_title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for job_grade |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `probation_end_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `weekly_hours` | `NUMERIC(16, 4)` | No | `40` | Operational entity attribute |
| `fte_percentage` | `NUMERIC(16, 4)` | No | `100` | Operational entity attribute |
| `base_annual_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `loaded_hourly_cost` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'active'` | State machine status indicator |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `terms` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_holiday_calendars`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_holiday_calendars_year_index` (Unique: No)
  - `hr_holiday_calendars_company_id_index` (Unique: No)
  - `hr_holiday_calendars_code_index` (Unique: No)
  - `sqlite_autoindex_hr_holiday_calendars_2` (Unique: Yes)
  - `sqlite_autoindex_hr_holiday_calendars_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `country_code` | `VARCHAR(255)` | No | `'IT'` | Unique business identification code or document number |
| `region_code` | `VARCHAR(255)` | Yes | NULL | Unique business identification code or document number |
| `year` | `INTEGER` | No | NULL | Operational entity attribute |
| `daily_standard_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `working_days` | `TEXT` | Yes | NULL | Operational entity attribute |
| `holidays` | `TEXT` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_job_grades`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_job_grades_company_id_index` (Unique: No)
  - `hr_job_grades_code_index` (Unique: No)
  - `sqlite_autoindex_hr_job_grades_2` (Unique: Yes)
  - `sqlite_autoindex_hr_job_grades_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `level_rank` | `INTEGER` | No | `1` | Operational entity attribute |
| `min_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `midpoint_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `max_salary` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_leave_balances`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
  - `leave_type_id` -> `hr_leave_types(id)`
- **Indexes & Constraints**:
  - `hr_leave_balances_fiscal_year_index` (Unique: No)
  - `hr_leave_balances_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_leave_balances_2` (Unique: Yes)
  - `sqlite_autoindex_hr_leave_balances_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `leave_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for leave_type |
| `fiscal_year` | `INTEGER` | No | NULL | Operational entity attribute |
| `entitlement_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `carryover_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `accrued_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `used_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `pending_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `available_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `last_accrued_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_leave_requests`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
  - `leave_type_id` -> `hr_leave_types(id)`
- **Indexes & Constraints**:
  - `hr_leave_requests_workflow_instance_id_index` (Unique: No)
  - `hr_leave_requests_status_index` (Unique: No)
  - `hr_leave_requests_start_date_index` (Unique: No)
  - `hr_leave_requests_request_number_index` (Unique: No)
  - `hr_leave_requests_end_date_index` (Unique: No)
  - `hr_leave_requests_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_leave_requests_2` (Unique: Yes)
  - `sqlite_autoindex_hr_leave_requests_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `leave_type_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for leave_type |
| `request_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `total_hours` | `NUMERIC(16, 4)` | No | NULL | Monetary or financial decimal quantity |
| `total_days` | `NUMERIC(16, 4)` | No | `1` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'pending_approval'` | State machine status indicator |
| `reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `medical_certificate_ref` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `approved_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for approved_by_user |
| `approved_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `rejection_reason` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_leave_types`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_leave_types_company_id_index` (Unique: No)
  - `hr_leave_types_code_index` (Unique: No)
  - `sqlite_autoindex_hr_leave_types_2` (Unique: Yes)
  - `sqlite_autoindex_hr_leave_types_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `category` | `VARCHAR(255)` | No | `'vacation'` | Operational entity attribute |
| `is_paid` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `requires_approval` | `BOOLEAN` | No | `TRUE` | Operational entity attribute |
| `requires_attachment` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `annual_entitlement_hours` | `NUMERIC(16, 4)` | No | `160` | Operational entity attribute |
| `accrual_frequency` | `VARCHAR(255)` | No | `'monthly'` | Operational entity attribute |
| `max_carryover_hours` | `NUMERIC(16, 4)` | No | `80` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_performance_reviews`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_performance_reviews_workflow_instance_id_index` (Unique: No)
  - `hr_performance_reviews_status_index` (Unique: No)
  - `hr_performance_reviews_reviewer_employee_id_index` (Unique: No)
  - `hr_performance_reviews_review_period_index` (Unique: No)
  - `hr_performance_reviews_review_number_index` (Unique: No)
  - `hr_performance_reviews_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_performance_reviews_2` (Unique: Yes)
  - `sqlite_autoindex_hr_performance_reviews_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `reviewer_employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for reviewer_employee |
| `review_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `review_period` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `review_type` | `VARCHAR(255)` | No | `'annual'` | Operational entity attribute |
| `review_date` | `DATE` | No | NULL | Operational entity attribute |
| `overall_rating` | `NUMERIC(16, 4)` | No | `3` | Operational entity attribute |
| `goals_score` | `NUMERIC(16, 4)` | No | `3` | Operational entity attribute |
| `competencies_score` | `NUMERIC(16, 4)` | No | `3` | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'draft'` | State machine status indicator |
| `promotion_recommended` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `recommended_job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for recommended_job_grade |
| `recommended_salary_increase_percent` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `career_path_notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `successor_readiness` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `goals` | `TEXT` | Yes | NULL | Operational entity attribute |
| `competencies` | `TEXT` | Yes | NULL | Operational entity attribute |
| `strengths` | `TEXT` | Yes | NULL | Operational entity attribute |
| `improvement_areas` | `TEXT` | Yes | NULL | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `completed_at` | `TIMESTAMP` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_positions`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `department_id` -> `hr_departments(id)`
  - `job_grade_id` -> `hr_job_grades(id)`
- **Indexes & Constraints**:
  - `hr_positions_successor_employee_id_index` (Unique: No)
  - `hr_positions_reports_to_position_id_index` (Unique: No)
  - `hr_positions_company_id_index` (Unique: No)
  - `hr_positions_code_index` (Unique: No)
  - `sqlite_autoindex_hr_positions_2` (Unique: Yes)
  - `sqlite_autoindex_hr_positions_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `job_grade_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for job_grade |
| `reports_to_position_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for reports_to_position |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `headcount_budget` | `INTEGER` | No | `1` | Operational entity attribute |
| `is_critical_role` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `successor_employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for successor_employee |
| `readiness_level` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `competencies_required` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_skills`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_skills_company_id_index` (Unique: No)
  - `hr_skills_code_index` (Unique: No)
  - `sqlite_autoindex_hr_skills_2` (Unique: Yes)
  - `sqlite_autoindex_hr_skills_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `category` | `VARCHAR(255)` | No | `'technical'` | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_teams`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `department_id` -> `hr_departments(id)`
- **Indexes & Constraints**:
  - `hr_teams_lead_employee_id_index` (Unique: No)
  - `hr_teams_company_id_index` (Unique: No)
  - `hr_teams_code_index` (Unique: No)
  - `sqlite_autoindex_hr_teams_2` (Unique: Yes)
  - `sqlite_autoindex_hr_teams_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `department_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for department |
| `lead_employee_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for lead_employee |
| `code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `name` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_timesheets`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
- **Indexes & Constraints**:
  - `hr_timesheets_workflow_instance_id_index` (Unique: No)
  - `hr_timesheets_work_date_index` (Unique: No)
  - `hr_timesheets_timesheet_number_index` (Unique: No)
  - `hr_timesheets_task_id_index` (Unique: No)
  - `hr_timesheets_status_index` (Unique: No)
  - `hr_timesheets_project_id_index` (Unique: No)
  - `hr_timesheets_cost_center_id_index` (Unique: No)
  - `hr_timesheets_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_timesheets_2` (Unique: Yes)
  - `sqlite_autoindex_hr_timesheets_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `project_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for project |
| `task_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for task |
| `cost_center_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for cost_center |
| `timesheet_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `work_date` | `DATE` | No | NULL | Operational entity attribute |
| `regular_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `overtime_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `total_hours` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `billable_hours` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `hourly_cost_rate` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `total_labor_cost` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `status` | `VARCHAR(255)` | No | `'submitted'` | State machine status indicator |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `approved_by_user_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for approved_by_user |
| `description` | `TEXT` | Yes | NULL | Operational entity attribute |
| `metadata` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_training_courses`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
- **Indexes & Constraints**:
  - `hr_training_courses_course_code_index` (Unique: No)
  - `hr_training_courses_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_training_courses_2` (Unique: Yes)
  - `sqlite_autoindex_hr_training_courses_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `course_code` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `title` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `category` | `VARCHAR(255)` | No | `'safety'` | Operational entity attribute |
| `provider` | `VARCHAR(255)` | No | `'Internal Academy'` | Operational entity attribute |
| `duration_hours` | `NUMERIC(16, 4)` | No | `8` | Operational entity attribute |
| `cost_per_participant` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `validity_months` | `INTEGER` | Yes | NULL | Operational entity attribute |
| `is_mandatory_compliance` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `is_active` | `BOOLEAN` | No | `TRUE` | Boolean configuration or state flag |
| `translations` | `TEXT` | Yes | NULL | Operational entity attribute |
| `syllabus` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `hr_training_records`

- **Operational Scope**: Tenant-Scoped
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `employee_id` -> `hr_employees(id)`
  - `course_id` -> `hr_training_courses(id)`
- **Indexes & Constraints**:
  - `hr_training_records_workflow_instance_id_index` (Unique: No)
  - `hr_training_records_status_index` (Unique: No)
  - `hr_training_records_enrollment_number_index` (Unique: No)
  - `hr_training_records_company_id_index` (Unique: No)
  - `sqlite_autoindex_hr_training_records_2` (Unique: Yes)
  - `sqlite_autoindex_hr_training_records_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | No | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `company_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for company |
| `employee_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for employee |
| `course_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for course |
| `enrollment_number` | `VARCHAR(255)` | No | NULL | Unique business identification code or document number |
| `status` | `VARCHAR(255)` | No | `'assigned'` | State machine status indicator |
| `assigned_date` | `DATE` | No | NULL | Operational entity attribute |
| `scheduled_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `completed_date` | `DATE` | Yes | NULL | Operational entity attribute |
| `score` | `NUMERIC(16, 4)` | Yes | NULL | Operational entity attribute |
| `cost_amount` | `NUMERIC(16, 4)` | No | `0` | Monetary or financial decimal quantity |
| `currency` | `VARCHAR(255)` | No | `'EUR'` | Operational entity attribute |
| `workflow_instance_id` | `VARCHAR(36)` | Yes | NULL | Foreign key reference identifier for workflow_instance |
| `is_locked` | `BOOLEAN` | No | `FALSE` | Boolean configuration or state flag |
| `certificate_issued` | `BOOLEAN` | No | `FALSE` | Operational entity attribute |
| `notes` | `TEXT` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

### `leave_balances`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
- **Indexes & Constraints**:
  - `leave_balances_year_index` (Unique: No)
  - `sqlite_autoindex_leave_balances_2` (Unique: Yes)
  - `sqlite_autoindex_leave_balances_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `year` | `INTEGER` | No | NULL | Operational entity attribute |
| `vacation_accrued` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `vacation_taken` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `rol_accrued` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `rol_taken` | `NUMERIC(16, 4)` | No | `0` | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |

---

### `leave_requests`

- **Operational Scope**: Shared Reference Lookup
- **Foreign Key References**:
  - `tenant_id` -> `tenants(id)`
  - `user_id` -> `users(id)`
  - `approved_by` -> `users(id)`
- **Indexes & Constraints**:
  - `leave_requests_type_index` (Unique: No)
  - `leave_requests_status_index` (Unique: No)
  - `sqlite_autoindex_leave_requests_1` (Unique: Yes)

**Field Definitions**:

| Column Name | Data Type | Nullable | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `id` | `VARCHAR(36)` | Yes | NULL | Primary Key (UUIDv7 unique identifier) |
| `tenant_id` | `VARCHAR(36)` | Yes | NULL | Multi-tenant discriminator foreign key referencing tenants(id) |
| `user_id` | `VARCHAR(36)` | No | NULL | Foreign key reference identifier for user |
| `type` | `VARCHAR(255)` | No | NULL | Operational entity attribute |
| `start_date` | `DATE` | No | NULL | Operational entity attribute |
| `end_date` | `DATE` | No | NULL | Operational entity attribute |
| `hours` | `NUMERIC(16, 4)` | No | NULL | Operational entity attribute |
| `status` | `VARCHAR(255)` | No | `'pending'` | State machine status indicator |
| `medical_cert_protocol` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `approved_by` | `VARCHAR(255)` | Yes | NULL | Operational entity attribute |
| `created_at` | `TIMESTAMP` | Yes | NULL | Timestamp of record creation |
| `updated_at` | `TIMESTAMP` | Yes | NULL | Timestamp of last record update |
| `deleted_at` | `TIMESTAMP` | Yes | NULL | Soft delete preservation timestamp |

---

