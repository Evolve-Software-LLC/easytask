---
title: Task Definition - EasyTask Documentation
description: Comprehensive reference for defining, scheduling, and configuring tasks in EasyTask including JSON fields, validation rules, dependencies, placeholders, and alerting.
keywords:
  - easytask task definition
  - easytask
  - task scheduling
  - task configuration
  - task dependencies
  - task alerts
  - json task format
---

# Task Definition

## 🧭 Overview

This document provides comprehensive information on configuring and scheduling tasks in EasyTask. Tasks are the fundamental units of work that the system schedules and executes. Each task is defined using JSON format with specific required and optional fields, validation rules, and type constraints.

## 🗂️ Sample Task Definition

```json
{
  "tid": 1000001,
  "name": "daily_backup_task",
  "task_owner": "admin",
  "cmd": "/scripts/backup.sh",
  "run_on_host": "backup-server",
  "max_run_time": 3600,
  "description": "Daily database backup with file rotation",
  "retry_attempts": 3,
  "stdout": "/logs/backup_${E:YYYYMMDD}.out",
  "stderr": "/logs/backup_${E:YYYYMMDD}.err",
  "timezone": "US/Eastern",
  "profile": "backup_profile",
  "active": true,
  "calendar": "US_HOLIDAYS",
  "instance": "default",
  "day_of_week": "1111111",
  "run_frequency": "02:00-02:00-1440",
  "task_accept_expiry_time": 300  
}
```

## 📊 Complete Field Reference

All task fields with their types, requirements, and constraints:

### Core Required Fields

| Field | Type | Required For | Description | Constraints |
|-------|------|--------------|-------------|-------------|
| **tid** | `integer` | All tasks | Unique task identifier | Must be > 1000, cannot start with 0 |
| **name** | `string` | All tasks | Task name (unique within instance) | Non-empty, alphanumeric + underscore |
| **task_owner** | `string` | All tasks | User/admin responsible for task | Non-empty string |
| **cmd** | `string` | All tasks | Command or script to execute | Non-empty, supports placeholders |
| **run_on_host** | `string` | All tasks | Queue name/hostname for execution | Valid hostname/queue name |
| **description** | `string` | All tasks | Task purpose description | Non-empty string |
| **stdout** | `string` | All tasks | Standard output file path | Valid file path, supports placeholders |
| **stderr** | `string` | All tasks | Standard error file path | Valid file path, supports placeholders |
| **active** | `boolean` | All tasks | Task enabled/disabled state | `true` or `false` |

### Scheduling Fields (Single Tasks Only)

| Field | Type | Required | Description | Constraints |
|-------|------|----------|-------------|-------------|
| **timezone** | `string` | Single tasks | Task timezone | Valid pytz timezone (e.g., "US/Eastern") |
| **instance** | `string` | Single tasks | Scheduler instance | Non-empty string, must exist |
| **day_of_week** | `string` | Single tasks* | 7-digit binary for weekdays | "0000000" to "1111111" (Mon-Sun) |
| **trigger_times** | `string` | Single tasks** | Specific trigger times | "HH:MM" format, 24-hour, comma-separated |
| **run_frequency** | `string` | Single tasks** | Interval-based scheduling | "HH:MM-HH:MM-INTERVAL" format |
| **ordinal_day** | `string` | Optional | Specific day patterns | Cannot use with day_of_week |

*Required if not using ordinal_day  
**Either trigger_times OR run_frequency required for single tasks (mutually exclusive)

### Optional Execution Fields

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| **run_as_user** | `string` | User account for execution | Valid system user |
| **max_run_time** | `integer` | Maximum execution time (seconds) | Positive integer |
| **retry_attempts** | `integer` | Number of retry attempts | 0-10 |
| **task_accept_expiry_time** | `integer` | Queue timeout (seconds) | Positive integer |
| **profile** | `string` | Environment profile for placeholders | Required if using ${...} placeholders |
| **calendar** | `string` | Holiday calendar name | Valid calendar ID |

### Group Task Fields

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| **task_group** | `string` | Parent task group name | Must exist in system |
| **dependency** | `string` | Task dependencies expression | Valid dependency syntax |

**Important**: Tasks in groups inherit scheduling configuration from their parent task group:
- **trigger_times** - Inherited from group (task group mandatory field)
- **day_of_week** - Inherited from group  
- **timezone** - Inherited from group
- **ordinal_day** - Inherited from group (if used)

**Critical**: `run_frequency` is NOT ALLOWED for task groups or tasks in groups - only `trigger_times` is supported for group scheduling

### Alert Configuration

| Field | Type | Description | Format |
|-------|------|-------------|---------|
| **alert** | `object` | Alert configuration | See Alert Configuration section |

## 🔧 Task Types and Field Requirements

### Single Task Requirements
**Mandatory Fields:**
```json
[
  "tid", "name", "cmd", "run_on_host", "description", 
  "stdout", "stderr", "timezone", "active", "instance"
]
```
**Plus one of:** `trigger_times` OR `run_frequency`

**Cannot Have:**
- `dependency` (single tasks cannot have dependencies)
- `task_group` (would make it a group task)

### Task in Group Requirements
**Mandatory Fields:**
```json
[
  "tid", "name", "run_on_host", "description", 
  "active", "stdout", "stderr", "task_group", "cmd"
]
```

**Cannot Have:**
- `day_of_week` (inherited from task group)
- `trigger_times` (inherited from task group)  
- `run_frequency` (inherited from task group)
- `timezone` (inherited from task group)
- `ordinal_day` (inherited from task group)

## ⚙️ Validation Rules

### ID Validation
- Must be integer > 1000
- Cannot start with 0
- Must be unique within instance

### Scheduling Validation
- **Single tasks**: Either `trigger_times` OR `run_frequency` required (mutually exclusive)
- **Task groups**: ONLY `trigger_times` allowed (required field) - `run_frequency` NOT SUPPORTED
- **Tasks in groups**: NO scheduling fields allowed - all inherited from parent group
- **day_of_week** and **ordinal_day** are mutually exclusive
- **trigger_times** format: "HH:MM" in 24-hour format, multiple times comma-separated
- **run_frequency** format: "START-END-INTERVAL" where START < END, INTERVAL 1-1440 minutes (single tasks only)

### Profile Requirement
If any field contains placeholders (`${...}`), the **profile** field is mandatory.

### Dependency Rules
1. Only allowed for tasks in groups
2. All dependent tasks must be in same group
3. No circular dependencies
4. Referenced tasks must exist

## 📅 Scheduling Formats

### Day of Week Binary Format

The `day_of_week` field uses a **7-digit binary string** to specify which days of the week a single task should run.

!!! info "Important"
    This field is **only for single tasks**. Tasks within a task group inherit their day_of_week from the parent group and cannot define it individually.

#### Format Structure

```
Position:  1    2    3    4    5    6    7
Day:       Mon  Tue  Wed  Thu  Fri  Sat  Sun
Binary:    1    1    1    1    1    0    0
```

- **`1`** = Run on this day
- **`0`** = Do not run on this day
- **Position 1** = Monday (first day)
- **Position 7** = Sunday (last day)

#### Common Examples

| Binary String | Days Selected | Description |
|--------------|---------------|-------------|
| `"1111111"` | Mon-Tue-Wed-Thu-Fri-Sat-Sun | Every day |
| `"1111100"` | Mon-Tue-Wed-Thu-Fri | Weekdays only (Monday-Friday) |
| `"0000011"` | Sat-Sun | Weekends only |
| `"1000000"` | Mon | Mondays only |
| `"0100000"` | Tue | Tuesdays only |
| `"0010000"` | Wed | Wednesdays only |
| `"0001000"` | Thu | Thursdays only |
| `"0000100"` | Fri | Fridays only |
| `"0000010"` | Sat | Saturdays only |
| `"0000001"` | Sun | Sundays only |
| `"1111010"` | Mon-Tue-Wed-Thu-Fri-Sat | All days except Sunday |
| `"0111110"` | Tue-Wed-Thu-Fri | Tuesday through Friday |

#### Important Notes

!!! note "Day Order"
    The binary string **always starts with Monday** as position 1 and ends with Sunday as position 7. This order is fixed and cannot be changed.

!!! warning "Common Mistakes"
    - ❌ Don't use `"0111110"` thinking it means Monday-Friday (it actually means Tuesday-Saturday)
    - ❌ Don't reverse the order (Sunday-Saturday)
    - ✅ Always use Monday-Sunday order: `"1111100"` for weekdays

!!! warning "Task Groups vs Single Tasks"
    - **Single Tasks**: Can define `day_of_week` field
    - **Tasks in Groups**: CANNOT define `day_of_week` (inherited from parent task group)
    - **Task Groups**: Define `day_of_week` in the group definition, not in individual tasks

#### Practical Examples

##### Daily Backup Task (Every Day)
```json
{
  "tid": 1000001,
  "name": "daily_backup",
  "day_of_week": "1111111",
  "trigger_times": "02:00",
  "timezone": "US/Eastern"
}
```

##### Business Hours Task (Weekdays Only)
```json
{
  "tid": 1000002,
  "name": "business_hours_check",
  "day_of_week": "1111100",
  "trigger_times": "09:00, 13:00, 17:00",
  "timezone": "US/Eastern"
}
```

##### Weekly Report (Wednesdays Only)
```json
{
  "tid": 1000003,
  "name": "weekly_report",
  "day_of_week": "0010000",
  "trigger_times": "10:00",
  "timezone": "US/Eastern"
}
```

##### Weekend Maintenance Task
```json
{
  "tid": 1000004,
  "name": "weekend_cleanup",
  "day_of_week": "0000011",
  "trigger_times": "03:00",
  "timezone": "US/Eastern"
}
```

### Trigger Times Format
```
Format: "HH:MM" or "HH:MM,HH:MM,..." (24-hour format)
Examples:
- "09:00"           = Once daily at 9 AM
- "09:00,14:00,18:00" = Three times daily (9 AM, 2 PM, 6 PM)
- "(09:00, 14:00)"  = Two times daily (parentheses and spaces removed)
- "00:00,12:00"     = Twice daily (midnight and noon)
```

### Run Frequency Format
```
Format: "HH:MM-HH:MM-INTERVAL" (interval-based scheduling)
Examples:
- "09:00-17:00-60"   = Every hour from 9 AM to 5 PM
- "02:00-02:00-1440" = Once daily at 2 AM
- "08:00-20:00-240"  = Every 4 hours from 8 AM to 8 PM
```

### Scheduling Field Usage

#### For Single Tasks:
- **Use trigger_times**: When you need specific execution times (e.g., "09:00,14:00,18:00")
- **Use run_frequency**: When you need interval-based execution within a time window (e.g., "09:00-17:00-60")
- **Cannot use both**: These fields are mutually exclusive for single tasks
- **Must use one**: Either trigger_times OR run_frequency is required

#### For Task Groups:
- **Task Group Definition**: Must include `trigger_times` (required field) - `run_frequency` NOT ALLOWED
- **Tasks in Group**: Cannot define any scheduling fields (trigger_times, run_frequency, day_of_week, timezone, ordinal_day)
- **Inheritance**: All scheduling is inherited from the parent task group via `trigger_times`
- **Important**: `run_frequency` is NEVER supported for task groups - only `trigger_times`

### 📋 Scheduling Rules Summary

| Task Type | trigger_times | run_frequency | day_of_week | timezone | ordinal_day |
|-----------|---------------|---------------|-------------|-----------|-------------|
| **Single Task** | ✅ Option A | ✅ Option B | ✅ Required* | ✅ Required | ✅ Optional* |
| **Task Group** | ✅ **Required** | ❌ **NOT ALLOWED** | ✅ Required | ✅ Required | ✅ Optional |
| **Task in Group** | ❌ **Inherited** | ❌ **NOT ALLOWED** | ❌ **Inherited** | ❌ **Inherited** | ❌ **Inherited** |

*Either day_of_week OR ordinal_day (mutually exclusive)

**Key Points:**
- Single tasks: Choose trigger_times OR run_frequency (never both)
- Task groups: Only trigger_times supported (run_frequency never allowed)
- Tasks in groups: All scheduling inherited from parent group

## 🔤 Placeholders & Field Interpolation

### Placeholder System Overview
Placeholders allow dynamic value substitution at runtime. When using placeholders, the **profile** field must be defined.

### Supported Fields
| Field | Supports Placeholders | Example |
|-------|----------------------|---------|
| **cmd** | ✅ | `rsync -avz ${E:SOURCE}/ user@${E:HOST}:${E:DEST}/` |
| **stdout** | ✅ | `/logs/task_${T:task_name}_${E:YYYYMMDD}.out` |
| **stderr** | ✅ | `/logs/task_${T:task_name}_${E:YYYYMMDD}.err` |
| **alert** | ✅ | Subject/body in alert configuration |
| **payload** | ✅ | JSON values can include placeholders |

### Placeholder Types

| Type | Prefix | Available Variables | Usage |
|------|--------|-------------------|-------|
| **Environment** | `${E:...}` | Any environment variable | `${E:HOME}`, `${E:USER}`, `${E:YYYYMMDD}` |
| **Task** | `${T:...}` | Task metadata | `${T:task_name}`, `${T:task_id}` |
| **Process** | `${P:...}` | Runtime process info | `${P:stdout}`, `${P:stderr}`, `${P:pid}`, `${P:status}` |

### Common Environment Variables
- `${E:YYYYMMDD}` - Current date (20240315)
- `${E:HH:MM}` - Current time (14:30)
- `${E:HOME}` - User home directory
- `${E:USER}` - Current user
- `${E:HOSTNAME}` - System hostname

### Process Variables (Alert Only)
- `${P:stdout}` - Task output
- `${P:stderr}` - Task errors  
- `${P:pid}` - Process ID
- `${P:status}` - Task completion status

### Important Notes
- **Profile Required**: If any field contains `${...}`, the `profile` field must specify a valid environment file
- **Runtime Resolution**: Placeholders are resolved when the task executes
- **Error Handling**: Invalid placeholders cause task failure

### Logging and Output

| Field      | Description                                                                                                       | Type   |
| ---------- | ----------------------------------------------------------------------------------------------------------------- |--------|
| **stdout** | Path where the task’s standard output is logged. Supports environment placeholders like `/tmp/${E:YYYYMMDD}.out`. |String  |
| **stderr** | Path where the task’s error output is logged. Supports placeholders like `/tmp/${E:YYYYMMDD}.err`.                |String  |

## 🚨 Alert Configuration

### Complete Alert Structure
```json
{
  "alert": {
    "alert_on": "failure|success|always",
    "integrations": [
      {
        "integration": "genericsmtp",
        "init": {
          "vault_path_key": "email/credentials"
        },
        "action": [
          {
            "send_email": {
              "to_address": "admin@company.com",
              "subject": "Task ${T:task_name} - ${P:status}",
              "body": "Task: ${T:task_name} (ID: ${T:task_id})\nTime: ${E:YYYYMMDD} ${E:HH:MM}\nStatus: ${P:status}\n\nOutput:\n${P:stdout}\n\nErrors:\n${P:stderr}"
            }
          }
        ]
      }
    ]
  }
}
```

### Alert Fields Reference

| Field | Type | Description | Values |
|-------|------|-------------|---------|
| **alert_on** | `string` | When to trigger alerts | `"failure"`, `"success"`, `"always"` |
| **integrations** | `array` | List of alert integrations | Array of integration objects |
| **integration** | `string` | Integration service type | `"genericsmtp"`, `"slack"`, `"teams"`, etc. |
| **init** | `object` | Integration initialization | Credentials and configuration |
| **vault_path_key** | `string` | Vault path for credentials | Path to stored credentials |
| **action** | `array` | Actions to perform | Array of action objects |
| **send_email** | `object` | Email action configuration | Email-specific parameters |
| **to_address** | `string` | Recipient email address | Valid email address |
| **subject** | `string` | Email subject line | Supports placeholders |
| **body** | `string` | Email message body | Supports placeholders |

### Alert Examples

#### Failure-Only Alerts
```json
{
  "alert": {
    "alert_on": "failure",
    "integrations": [
      {
        "integration": "genericsmtp",
        "init": {"vault_path_key": "alerts/email"},
        "action": [
          {
            "send_email": {
              "to_address": "ops@company.com",
              "subject": "ALERT: ${T:task_name} Failed",
              "body": "Task ${T:task_name} failed at ${E:YYYYMMDD}\nError: ${P:stderr}"
            }
          }
        ]
      }
    ]
  }
}
```

#### Success and Failure Alerts
```json
{
  "alert": {
    "alert_on": "always",
    "integrations": [
      {
        "integration": "genericsmtp",
        "init": {"vault_path_key": "monitoring/email"},
        "action": [
          {
            "send_email": {
              "to_address": "monitor@company.com",
              "subject": "Task Report: ${T:task_name} - ${P:status}",
              "body": "Task ${T:task_name} completed with status: ${P:status}\nDuration: ${P:duration}\nOutput: ${P:stdout}"
            }
          }
        ]
      }
    ]
  }
}
```

# Task Dependency Specification

This section explains the syntax and semantics used to define task dependencies, as well as the various task lifecycle states.

---

## 📌 Dependency Format

A task may define a `dependency` field to indicate that its execution depends on the successful completion of other tasks.

**Example:**

```json
{
  "dependency": "(S:task7) and (S:task8)"
}
```

This expression means that the current task should only be considered for execution if **both `task7` and `task8` have reached the `SUCCESS` state** (`S`).

---

## ✅ Dependency Expression Syntax

- **Format:** `(STATE:TASK_NAME)`
- **STATE:** One-letter status code representing a valid task state (see table below)
- **TASK_NAME:** The unique name of a task which must be pre-defined and present in the system

Logical operators are supported to combine multiple conditions:
- `and`: All conditions must be met
- `or`: At least one condition must be met
- Parentheses `()` can be used to group expressions for precedence

---

## 🔁 Supported Task States

Each task in the system can exist in one of several states. The following table provides the possible task states and their descriptions:

| Code | State       | Description                                      |
|------|-------------|--------------------------------------------------|
| `I`  | IDLE        | Task is registered but inactive                  |
| `P`  | PASSIVE     | Task is dormant and waiting                      |
| `A`  | ACTIVE      | Task is active but not yet running               |
| `Z`  | TRIGGER     | Task is marked for triggering                    |
| `D`  | STARTED     | Task has just begun execution                    |
| `R`  | RUNNING     | Task is currently in progress                    |
| `E`  | REJECTED    | Task was rejected and won't run                  |
| `F`  | FAILED      | Task execution failed                            |
| `S`  | SUCCESS     | Task completed successfully                      |
| `G`  | RESTARTING  | Task is in process of restarting                 |
| `T`  | TERMINATED  | Task was manually or automatically terminated    |
| `O`  | FREEZE      | Task is paused/frozen                            |
| `U`  | UNFREEZE    | Task has resumed from freeze                     |

---

## 🔒 Integrity Requirements

- All referenced task names **must be pre-existing** in the system's task registry.
- Invalid or undefined task names or states will result in dependency resolution failure at runtime or insertion.

---

## 📝 Complete Examples

### Example 1: Simple Daily Backup Task
```json
{
  "tid": 100001,
  "name": "daily_database_backup",
  "task_owner": "dba_team",
  "cmd": "/scripts/backup_database.sh production",
  "run_on_host": "backup-server",
  "max_run_time": 3600,
  "description": "Daily backup of production database",
  "retry_attempts": 3,
  "stdout": "/logs/backup/backup_${E:YYYYMMDD}.out",
  "stderr": "/logs/backup/backup_${E:YYYYMMDD}.err",
  "timezone": "US/Eastern",
  "profile": "database_backup_profile",
  "active": true,
  "instance": "production",
  "day_of_week": "1111111",
  "trigger_times": "02:00",
  "calendar": "BUSINESS_HOLIDAYS",
  "alert": {
    "alert_on": "failure",
    "integrations": [
      {
        "integration": "genericsmtp",
        "init": {"vault_path_key": "alerts/dba_email"},
        "action": [
          {
            "send_email": {
              "to_address": "dba@company.com",
              "subject": "CRITICAL: Database Backup Failed",
              "body": "Database backup failed at ${E:YYYYMMDD}\nError: ${P:stderr}\nPlease investigate immediately."
            }
          }
        ]
      }
    ]
  }
}
```

### Example 2: Multiple Daily Reports with Trigger Times
```json
{
  "tid": 100002,
  "name": "daily_sales_reports",
  "task_owner": "analytics",
  "cmd": "python /apps/reports/sales_report.py --period ${E:REPORT_PERIOD}",
  "run_on_host": "analytics-01",
  "max_run_time": 900,
  "description": "Generate sales reports three times daily",
  "stdout": "/reports/sales/report_${E:YYYYMMDD}_${E:HHMM}.out",
  "stderr": "/reports/sales/report_${E:YYYYMMDD}_${E:HHMM}.err",
  "timezone": "US/Pacific",
  "profile": "analytics_profile",
  "active": true,
  "instance": "reporting",
  "day_of_week": "0111110",
  "trigger_times": "09:00,14:00,18:00",
  "calendar": "US_HOLIDAYS"
}
```

### Example 2b: Weekday Report with Interval Scheduling
```json
{
  "tid": 100003,
  "name": "hourly_sales_report",
  "task_owner": "analytics", 
  "cmd": "python /apps/reports/sales_report.py --hourly",
  "run_on_host": "analytics-01",
  "max_run_time": 900,
  "description": "Generate hourly sales reports during business hours",
  "stdout": "/reports/sales/hourly_${E:YYYYMMDD}_${E:HH}.out",
  "stderr": "/reports/sales/hourly_${E:YYYYMMDD}_${E:HH}.err",
  "timezone": "US/Pacific",
  "profile": "analytics_profile",
  "active": true,
  "instance": "reporting",
  "day_of_week": "0111110",
  "run_frequency": "08:00-18:00-60",
  "calendar": "US_HOLIDAYS"
}
```

### Example 3: Task in Group with Dependencies
```json
{
  "tid": 200001,
  "name": "process_customer_data",
  "task_group": "etl_pipeline",
  "task_owner": "data_engineering",
  "cmd": "/etl/scripts/process_customers.py",
  "run_on_host": "etl-worker-01",
  "max_run_time": 1800,
  "description": "Process customer data after extraction",
  "active": true,
  "stdout": "/etl/logs/process_customers.out",
  "stderr": "/etl/logs/process_customers.err",
  "dependency": "(S:extract_customer_data)",
  "retry_attempts": 2
}
```

### Example 4: File Transfer with Complex Alerting
```json
{
  "tid": 300001,
  "name": "sync_production_files",
  "task_owner": "devops",
  "cmd": "rsync -avz --delete ${E:SOURCE_PATH}/ user@${E:DEST_HOST}:${E:DEST_PATH}/",
  "run_on_host": "file-ops",
  "max_run_time": 7200,
  "description": "Synchronize production files to backup location",
  "retry_attempts": 3,
  "stdout": "/var/log/sync/production_sync_${E:YYYYMMDD}.out",
  "stderr": "/var/log/sync/production_sync_${E:YYYYMMDD}.err",
  "profile": "file_sync_profile",
  "timezone": "UTC",
  "active": true,
  "instance": "file_operations",
  "day_of_week": "1111111",
  "run_frequency": "00:00-23:00-360",
  "task_accept_expiry_time": 300,
  "team": "infrastructure",
  "alert": {
    "alert_on": "always",
    "integrations": [
      {
        "integration": "genericsmtp",
        "init": {"vault_path_key": "notifications/ops_email"},
        "action": [
          {
            "send_email": {
              "to_address": "ops@company.com",
              "subject": "File Sync Status: ${P:status}",
              "body": "Production file sync completed\nTime: ${E:YYYYMMDD} ${E:HH:MM}\nStatus: ${P:status}\nDuration: ${P:duration}\n\nSummary:\n${P:stdout}\n\nErrors (if any):\n${P:stderr}"
            }
          }
        ]
      }
    ]
  }
}
```

## 🛠️ Quick Validation Checklist

Before submitting a task definition:

- [ ] **tid** is unique and > 1000
- [ ] **name** is unique within scope
- [ ] All required fields present for task type
- [ ] No excluded fields present for task type
- [ ] Valid scheduling configuration (trigger_times OR run_frequency)
- [ ] **profile** specified if using placeholders
- [ ] **timezone** valid for single tasks
- [ ] **dependency** syntax correct for grouped tasks
- [ ] File paths valid for **stdout**/**stderr**
- [ ] **alert** configuration complete if specified
- [ ] **active** set to true when ready to run

## 🚨 Common Validation Errors

| Error | Solution |
|-------|----------|
| "tid must be > 1000" | Use task IDs starting from 1001 |
| "Both trigger_times and run_frequency defined" | Remove one - they're mutually exclusive for single tasks |
| "Neither trigger_times nor run_frequency defined" | Add one scheduling field for single tasks |
| "trigger_times/run_frequency defined for task in group" | Remove - scheduling inherited from task group |
| "run_frequency defined for task group" | NOT ALLOWED - task groups can only use trigger_times |
| "dependency cannot be defined for single task" | Remove dependency or add task to a group |
| "timezone defined for task in group" | Remove timezone - inherited from group |
| "profile required for placeholders" | Add profile field when using ${...} |
| "Bad entry in Trigger Times field" | Use 24-hour format: "HH:MM" or "HH:MM,HH:MM" |
| "circular dependency detected" | Review and fix task dependency chain |
| "task_group does not exist" | Create the task group first |

---

## Frequently Asked Questions

**What is the difference between trigger_times and run_frequency?**
`trigger_times` specifies exact execution times (e.g., `"09:00,14:00"`), while `run_frequency` defines interval-based scheduling within a time window (e.g., `"09:00-17:00-60"` for every hour). They are mutually exclusive for single tasks.

**Can a single task have dependencies?**
No. Dependencies are only allowed for tasks within a group. Single tasks run independently based on their own schedule.

**What happens if I use placeholders without a profile?**
The task will fail at validation. If any field contains `${...}` placeholders, the `profile` field must be specified to provide the environment file for resolution.

---

## Next Steps

- [Task Groups](./task_group.md) — Learn how to organize tasks into groups with shared scheduling
- [Task Lifecycle](./task_lifecycle.md) — Understand task states from creation to completion
- [Cloud Agent Installation](../installation/cloud/agent_setup.md) — Set up agents to execute your tasks
