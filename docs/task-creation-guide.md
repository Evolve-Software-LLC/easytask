---
title: Task Creation and Scheduling Guide - EasyTask Documentation
description: Learn how to create and schedule tasks in EasyTask with clear examples for non-technical users.
keywords:
  - easytask task creation
  - easytask
  - task scheduling
  - cron scheduling
---

# Task Creation and Scheduling Guide

This guide will walk you through creating and scheduling tasks in EasyTask, with clear examples for non-technical users.

## Understanding Task Structure

A task in EasyTask is defined using a JSON format (don't worry, we'll explain everything). Think of it like filling out a form with specific information about what you want the computer to do.

## Task Types
  1. **Single Tasks** - Standalone tasks with their own scheduling
  2. **Tasks in Groups** - Part of a task group, inherit scheduling from the group

---

## 🔑 Critical Design Principle: Mutual Exclusivity

**IMPORTANT:** You cannot define tasks with both time-based scheduling (trigger_times/run_frequency) AND dependencies. This is a fundamental architectural design in EasyTask:

### Single Tasks
- ✅ **CAN have:** `trigger_times` OR `run_frequency` for scheduling
- ✅ **CAN have:** `day_of_week`, `timezone`, `ordinal_day`
- ❌ **CANNOT have:** `dependency` field
- ❌ **CANNOT be part of:** Task groups

### Tasks in Groups
- ✅ **CAN have:** `dependency` field (on other tasks within the same group)
- ✅ **MUST have:** `task_group` field
- ❌ **CANNOT have:** `trigger_times`, `run_frequency`, `day_of_week`, `timezone`
- ✅ **Inherit:** All scheduling from the parent task group

---

## Field Requirements and Constraints

### All Tasks (Required Fields)

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| **tid** | `integer` | Unique task identifier | Must be > 1000, no leading zeros |
| **name** | `string` | Task name (unique within instance) | Max 128 characters, alphanumeric + underscore |
| **task_owner** | `string` | User/admin responsible for task | Max 64 characters, non-empty |
| **cmd** | `string` | Command or script to execute | Non-empty, supports placeholders |
| **run_on_host** | `string` | Queue name/hostname for execution | Max 128 characters |
| **description** | `string` | Task purpose description | Max 256 characters, non-empty |
| **stdout** | `string` | Standard output file path | Max 128 characters, supports placeholders |
| **stderr** | `string` | Standard error file path | Max 128 characters, supports placeholders |
| **active** | `boolean` | Task enabled/disabled state | `true` or `false` |

### Single Task Fields (Scheduling)

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| **timezone** | `string` | Task timezone | Max 64 characters (e.g., "US/Eastern") |
| **instance** | `string` | Scheduler instance | Non-empty string, must exist |
| **day_of_week** | `string` | 7-digit binary for weekdays | "0000000" to "1111111" (Mon-Sun) |
| **trigger_times** | `string` | Specific trigger times | "HH:MM" format, 24-hour, comma-separated |
| **run_frequency** | `string` | Interval-based scheduling | "HH:MM-HH:MM-INTERVAL" format |
| **ordinal_day** | `string` | Specific day patterns | Cannot use with day_of_week |

**Scheduling Rule:** Single tasks can have either `trigger_times` OR `run_frequency`, never both.

### Task Group Task Fields (Required)

| Field | Type | Description | Constraints |
|-------|------|-------------|-------------|
| **run_as_user** | `string` | User to run the task as | Max 64 characters, mandatory for group tasks |
| **task_group** | `string` | Name of parent task group | Must reference existing task group |
| **dependency** | `string` | Task dependency expression | Only references tasks in same group |

**Inherited Fields:** Tasks in groups automatically inherit `timezone`, `day_of_week`, and `trigger_times` from their parent task group.

---

## Step-by-Step Task Creation

### Method 1: Using the Web Interface (Easiest)

1. **Open your web browser** and go to your EasyTask web interface
2. **Login** with your credentials
3. **Navigate to Tasks** section
4. **Click on "Task Definitions"** under the Tasks menu
5. **Click "Add New Task"**
6. **Fill in the form:**
    - Task Name: Give it a descriptive name
    - Description: Explain what it does
    - Command: What should be executed
    - Schedule: When it should run (day and time) - **for single tasks only**
    - Timezone: The timezone for schedule interpretation - **for single tasks only**
    - Host: Which server/computer should run it
    - User: User account to run the task - **required for task group tasks**
    - Task Group: Parent group (if applicable) - **removes scheduling options**
    - Stdout: Standard output log file path
    - Stderr: Standard error log file path
7. **Activate the task** by toggling it to "Active"
8. **Click "Submit"**

### Method 2: Using JSON Files (For Advanced Users)

#### Example 1: Single Task with Time-Based Scheduling

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

#### Example 2: Single Task with Specific Times

```json
{
  "name": "weekly-cleanup",
  "description": "Clean up old temporary files",
  "cmd": "find /tmp -type f -mtime +7 -delete",
  "active": true,
  "run_on_host": "192.173.115.96",
  "timezone": "UTC",
  "day_of_week": "0000001",
  "trigger_times": "02:00",
  "stdout": "/logs/morning-report.out",
  "stderr": "/logs/morning-report.err",
  "retry_attempts": 2,
  "max_run_time": 600
}
```

#### Example 3: Task in a Group with Dependencies

```json
{
  "tid": 200001,
  "name": "transform_data",
  "task_owner": "data_team",
  "cmd": "python /scripts/transform.py",
  "run_on_host": "data-server",
  "run_as_user": "data_user",
  "task_group": "data_pipeline",
  "description": "Transform extracted data",
  "dependency": "(S:extract_data)",
  "active": true,
  "stdout": "/logs/transform.out",
  "stderr": "/logs/transform.err",
  "retry_attempts": 2,
  "max_run_time": 1800
}
```

**Note:** This task inherits scheduling from the "data_pipeline" task group and depends on the "extract_data" task completing successfully.

---

## Understanding Scheduling Options

### 1. Time-Based Scheduling (Single Tasks Only)

**Trigger-Time Format:** `HH:MM` (24-hour format)

Examples:
- `"09:00"` - Run once at 9 AM
- `"02:00,14:30"` - Run twice daily at 2 AM and 2:30 PM

### 2. Day of Week Scheduling

**Format:** 7-digit string representing Monday through Sunday

#### Understanding the Binary Format

The `day_of_week` field uses a binary string where each position represents a day of the week:

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
| `"0000011"` | Sat-Sun | Weekends only (Saturday and Sunday) |
| `"1000000"` | Mon | Mondays only |
| `"0100000"` | Tue | Tuesdays only |
| `"0010000"` | Wed | Wednesdays only |
| `"0001000"` | Thu | Thursdays only |
| `"0000100"` | Fri | Fridays only |
| `"0000010"` | Sat | Saturdays only |
| `"0000001"` | Sun | Sundays only |
| `"1111000"` | Mon-Tue-Wed-Thu | First 4 days of week |
| `"0111110"` | Tue-Wed-Thu-Fri | Mid-week (Tuesday-Friday) |

!!! warning "Important Notes"
    - **Day Order**: The string ALWAYS starts with Monday and ends with Sunday
    - **Single Tasks**: Can define `day_of_week` field
    - **Task Group Tasks**: CANNOT define `day_of_week` (inherited from parent group)
    - **Common Mistake**: Don't use `"0111110"` for weekdays (that's Tuesday-Saturday!)

#### Practical Examples

**Every Day Backup:**
```json
{
  "name": "daily_backup",
  "day_of_week": "1111111",
  "trigger_times": "02:00"
}
```

**Business Hours Task (Weekdays Only):**
```json
{
  "name": "business_report",
  "day_of_week": "1111100",
  "trigger_times": "09:00"
}
```

**Weekly Maintenance (Wednesdays Only):**
```json
{
  "name": "weekly_maintenance",
  "day_of_week": "0010000",
  "trigger_times": "03:00"
}
```

### 3. Calendar-Based Scheduling

Exclude holidays from your schedule:

Examples:
- `"US_HOLIDAYS"` - Skip US federal holidays
- `"WORLD_HOLIDAYS"` - Skip world holidays
- `"MY_COMPANY_HOLIDAYS"` - Custom calendar you define

### 4. Advanced Scheduling

**Ordinal Day Scheduling:**
- `"first monday of every month"` - First Monday each month
- `"last friday of every month"` - Last Friday each month

**Run Frequency Format:** `HH:MM-HH:MM-INTERVAL`
- `"09:00-17:00-30"` - Every 30 minutes between 9 AM and 5 PM
- `"00:00-23:59-5"` - Every 5 minutes, all day
- `"14:30-15:30-1"` - Every minute between 2:30 PM and 3:30 PM

**Scheduling Rule:** Can have either `trigger_times` OR `run_frequency`, never both.

---

## Field Value Constraints

### String Field Length Limits

| Field | Max Length |
|-------|------------|
| `name` | 128 characters |
| `task_owner` | 64 characters |
| `run_on_host` | 128 characters |
| `run_as_user` | 64 characters |
| `description` | 256 characters |
| `stdout` | 128 characters |
| `stderr` | 128 characters |
| `timezone` | 64 characters |

### Numeric Field Constraints

| Field | Minimum | Maximum | Notes |
|-------|---------|---------|-------|
| `tid` | 1001 | - | No leading zeros |
| `gid` | 1 | - | For task groups |
| `max_run_time` | 1 | 82800 | In seconds (max 23 hours) |
| `retry_attempts` | 0 | - | No maximum defined |
| `task_accept_expiry_time` | 1 | - | In seconds |

### Boolean Fields

| Field | Valid Values |
|-------|--------------|
| `active` | `true`, `false` |
| `run_day_of_week` | `true`, `false` (task groups only) |

---

## Task Groups for Easier Management

Task groups let you group and schedule multiple related tasks together.

### Task Group Definition

| Field | Type | Mandatory | Description | Examples |
|-------|------|-----------|-------------|----------|
| `gid` | Integer | Yes | Task group ID | 3000001 |
| `name` | String | Yes | Group name | "data_pipeline" |
| `description` | String | Yes | Group description | "Daily data processing" |
| `day_of_week` | String | Yes | Days to run (binary) | "1111100" |
| `trigger_times` | String | Yes | Execution times | "08:00, 20:00" |
| `timezone` | String | Yes | Local timezone | "US/Eastern" |
| `active` | Boolean | Yes | Group active status | `true` |
| `dependency` | String | No | Dependency on other groups | "(S:upstream_group)" |
| `team` | String | No | Associated team | "data_team" |

### Task Group Example

```json
{
  "gid": 3000001,
  "name": "data_pipeline",
  "description": "Daily data processing workflow",
  "day_of_week": "1111111",
  "trigger_times": "08:00",
  "timezone": "US/Eastern",
  "active": true,
  "dependency": "(S:data_extraction_group)",
  "team": "data_team"
}
```

### Fields That Tasks Inherit from Groups

When a task belongs to a task group, it automatically inherits:
- `timezone`
- `day_of_week`
- `trigger_times`

### Fields NOT Allowed in Task Groups

These fields are defined in individual tasks, not in task groups:
- ❌ `run_on_host` - Define in tasks
- ❌ `run_as_user` - Define in tasks
- ❌ `profile` - Define in tasks
- ❌ `max_run_time` - Define in tasks

---

## Common Mistakes to Avoid

### ❌ Critical Mistakes

1. **Using "id" instead of "tid" for tasks**
   ```json
   // WRONG
   {"id": 200001, "name": "task_name"}

   // CORRECT
   {"tid": 200001, "name": "task_name"}
   ```

2. **Including forbidden fields in task group tasks**
   ```json
   // WRONG - these fields are inherited from the group
   {
     "tid": 200001,
     "name": "task_name",
     "task_group": "my_group",
     "timezone": "US/Eastern",        // ❌ Forbidden
     "trigger_times": "10:00",        // ❌ Forbidden
     "day_of_week": "1111100"         // ❌ Forbidden
   }

   // CORRECT - task inherits these from group
   {
     "tid": 200001,
     "name": "task_name",
     "task_group": "my_group"
     // timezone, trigger_times, day_of_week inherited
   }
   ```

3. **Missing mandatory field for group tasks**
   ```json
   // WRONG - missing run_as_user
   {
     "tid": 200001,
     "name": "task_name",
     "task_group": "my_group"
     // ❌ Missing "run_as_user"
   }

   // CORRECT
   {
     "tid": 200001,
     "name": "task_name",
     "task_group": "my_group",
     "run_as_user": "username"
   }
   ```

4. **Invalid task IDs**
   ```json
   // WRONG - task ID must be > 1000 and no leading zeros
   {"tid": 001, "name": "task_name"}
   {"tid": 999, "name": "task_name"}

   // CORRECT
   {"tid": 200001, "name": "task_name"}
   ```

5. **Trying to add both trigger_times and run_frequency**
   ```json
   // WRONG - can only have one
   {
     "trigger_times": "10:00",
     "run_frequency": "10:00-16:00-30"
   }

   // CORRECT - choose one
   {
     "trigger_times": "10:00"
     // OR
     "run_frequency": "10:00-16:00-30"
   }
   ```

6. **Single tasks with dependencies**
   ```json
   // WRONG - single tasks cannot have dependencies
   {
     "tid": 1000001,
     "name": "standalone_task",
     "dependency": "(S:other_task)"
   }

   // CORRECT - only task group tasks can have dependencies
   {
     "tid": 200001,
     "name": "group_task",
     "task_group": "my_group",
     "dependency": "(S:other_task)"
   }
   ```

---

## Best Practices

### ✅ Do's
- **Use descriptive names** - "backup-customer-db" not "task1"
- **Include good descriptions** - Help future you understand what it does
- **Set appropriate timeouts** - Don't let tasks run forever (max 82800 seconds)
- **Use retry attempts** for critical tasks
- **Log output and errors** - Specify stdout and stderr files with date placeholders
- **Test commands manually first** - Make sure they work before scheduling
- **Use proper field names** - Always use "tid", never "id"
- **Provide the hostname** - The host machine where the task should run
- **Use task groups** for related workflows with dependencies
- **Set run_as_user** for all task group tasks

### ❌ Don'ts
- **Don't schedule too frequently** - Every minute tasks can overload the system
- **Don't forget timezones** - Specify them clearly to avoid confusion
- **Don't make tasks dependent on manual intervention** - They should run automatically
- **Don't use the same name twice** - Each task needs a unique name
- **Don't forget to activate** - If you deactivate a task, remember to turn it back on
- **Don't mix trigger_times and run_frequency** - Choose one scheduling method
- **Don't add dependencies to single tasks** - Only task group tasks can have dependencies
- **Don't define scheduling in task group tasks** - They inherit from the group

---

## Monitoring Your Tasks

### Checking Task Status
1. **Web Interface:** Go to "Task Runs" to see execution history
2. **Log Files:** Check the stdout/stderr files you specified

### Understanding Task States
- **Idle** ⏳ - Task is scheduled but not started
- **Active** 🟢 - Task is ready to run
- **Triggered** 🚀 - Task has been initiated and queued
- **Started** ▶️ - Task has begun its startup process
- **Running** ⚡ - Task is currently executing
- **Success** ✅ - Task completed without errors
- **Failed** ❌ - Task encountered an error
- **Terminated** 🛑 - Task was terminated
- **Freeze** 🧊 - Task is paused
- **Unfreeze** 💧 - Task has resumed from freeze

---

## Troubleshooting Common Issues

### Task Not Running
- Check if task is **active** (enabled)
- Verify the **schedule** is correct
- Confirm the **timezone** settings
- Check **system clock** is accurate

### Task Failing
- Review **error logs** (stderr file)
- Test the **command manually**
- Check **file permissions**
- Verify **required software** is installed
- Increase **max_run_time** if timing out

### Validation Errors
- Check **field names** - use "tid" not "id"
- Verify **task ID** is > 1000 with no leading zeros
- Ensure **mandatory fields** are present for your task type
- Confirm **no forbidden fields** for your task type
- Check **field length constraints**

### Scheduling Issues
- **24-hour format** - Use 14:30, not 2:30 PM
- **Day of week** - Remember Monday = 1st position
- **Timezone** - Specify explicitly, don't assume
- **Frequency format** - Follow HH:MM-HH:MM-MINUTES exactly
- **Mutual exclusivity** - Don't mix trigger_times and run_frequency

---

## Quick Reference Card

### Single Task Template
```json
{
  "tid": 1000001,
  "name": "your-task-name",
  "description": "What this task does",
  "task_owner": "your-team",
  "cmd": "command to run",
  "run_on_host": "your-server",
  "active": true,
  "timezone": "America/New_York",
  "day_of_week": "1111111",
  "trigger_times": "09:00",
  "stdout": "/logs/task.out",
  "stderr": "/logs/task.err",
  "retry_attempts": 3,
  "max_run_time": 300
}
```

### Task Group Task Template
```json
{
  "tid": 200001,
  "name": "your-group-task",
  "description": "What this task does",
  "task_owner": "your-team",
  "cmd": "command to run",
  "run_on_host": "your-server",
  "run_as_user": "username",
  "task_group": "your-group-name",
  "active": true,
  "dependency": "(S:prerequisite_task)",
  "stdout": "/logs/task.out",
  "stderr": "/logs/task.err",
  "retry_attempts": 2,
  "max_run_time": 1800
}
```

---

## Frequently Asked Questions

**Q: Can I schedule a task to run every 15 minutes?**
A: Yes. Use `minute: "*/15"` in your cron expression along with the desired hours. EasyTask supports full cron-style flexibility for fine-grained scheduling.

**Q: What happens if a task fails?**
A: EasyTask logs the error and marks the task as failed. You can configure `retry_attempts` to automatically re-run failed tasks. Check the task's error log file for diagnostics.

**Q: Can I create tasks from the command line instead of the web UI?**
A: Yes. Use the EasyTask CLI `insert_task` command to create tasks programmatically. See the [CLI documentation](https://runeasytask.io/docs/getting_started/easytask_cli/database_operations/task/insert_task/) for details.

For complete documentation and advanced features, visit [runeasytask.io/docs](https://runeasytask.io/docs)
