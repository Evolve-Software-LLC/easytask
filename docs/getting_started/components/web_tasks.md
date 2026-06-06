---
title: Tasks UI - EasyTask Documentation
description: Manage EasyTask tasks and groups including task definitions, group definitions, scheduling, dependencies, and dashboard status monitoring.
keywords:
  - tasks UI
  - easytask
  - task definitions
  - task groups
  - task dashboard
  - task management
---

## ⚡ Tasks UI

### 📊 Dashboard

The Dashboard provides a real-time overview of your system's health and activity.

#### 📈 Status Definitions
The following table explains the various task statuses you will encounter on the dashboard:

| Icon | Status | Meaning | When differs from others |
| :--- | :--- | :--- | :--- |
| ✅ | **Idle** | Task is active but not currently executing. | Waiting for its scheduled trigger time. |
| 🚀 | **Active** | Task/Group is enabled in the system. | Ready to be triggered by the scheduler. |
| 🔄 | **Triggered** | Scheduler has initiated the execution. | Signal sent to agent, waiting for confirmation. |
| 🎬 | **Started** | Task received by agent, preparing to run. | Agent acknowledged receipt, execution imminent. |
| ▶️ | **Running** | Agent is actively processing the workload. | Code/Command is currently executing on the host. |
| ✅ | **Success** | Execution completed successfully. | Process exited with code `0`. |
| ❌ | **Failed** | Execution failed to complete correctly. | Process exited with non-zero code or exception. |
| ⛔ | **Terminated** | Execution was manually stopped. | Operator intervened to halt the process. |

### 🗂 Task Definitions

The Task Definitions page is the command center for managing individual automated jobs. Each task represents a single unit of work (e.g., a script, binary, or command) to be executed on a specific host.

✅ **Key Attributes & Capabilities:**

- **TID (Task ID)**: Unique integer identifier for the task.
- **Management**:
    - **Create/Edit**: Define the `Command`, `Target Host`, and `Run As User`.
    - **Ad-hoc Run**: Immediately trigger a task execution for testing or remediation, bypassing its schedule.
- **Scheduling**:
    - Define precise **Trigger Times** (Crontab-style or specific timestamps).
    - Set execution **Timezones** to ensure correct local timing.
- **Resilience**: Configure `Retry Attempts` and `Max Run Time` (timeout) to handle failures gracefully.
- **Bulk Actions**: Export or Import task definitions via JSON for backup or migration.

### 📦 Group Definitions

Task Groups serve as logical containers that organize related tasks into a single manageable unit.

✅ **Key Attributes & Capabilities:**

- **GID (Group ID)**: Unique integer identifier for the group.
- **Unified Management**:
    - **Global Activation**: Toggle the `Active` status of the group to strictly enable or disable ALL tasks within it.
    - **Shared Context**: All tasks in a group inherit the group's `Instance` and effectively share its lifecycle.
- **Orchestration**:
    - **Group Scheduling**: Define a `Trigger Time` at the group level to orchestrate when the entire batch of tasks should be considered for execution.
    - **Dependencies**: Useful for organizing workflows (e.g., "Daily ETL Pipeline") where tasks are related by function or project.

### 🔗 Relationship: Tasks & Groups

Understanding the relationship between Tasks and Groups is key to effective system organization:

1.  **Cardinality**: A **Task** can belong to exactly **one** Task Group (or none). A **Task Group** can contain **multiple** Tasks.
2.  **Inheritance**:
    - When a Task is assigned to a Group, it is strictly bound to that Group's logical "Instance".
    - Disabling a Task Group (setting `Active` to False) effectively puts a "freeze" on all tasks within that group, preventing them from running regardless of their individual schedules.
3.  **Workflow**:
    - Use **Groups** to model high-level processes (e.g., "Finance End-of-Month").
    - Use **Tasks** to define the specific steps within that process (e.g., "Generate Report", "Email Summary").

---

## Frequently Asked Questions

**Q: What is the difference between a Task and a Task Group?**
A: A Task represents a single unit of work (script, command, or binary) to be executed on a specific host. A Task Group is a logical container that organizes related tasks. A task belongs to exactly one group, and disabling a group freezes all tasks within it.

**Q: What task statuses can I see on the Dashboard?**
A: The dashboard shows Idle, Active, Triggered, Started, Running, Success, Failed, and Terminated statuses. Each has a distinct icon and meaning — for example, "Triggered" means the scheduler has initiated execution but is waiting for agent confirmation.

**Q: Can I run a task immediately without waiting for its schedule?**
A: Yes. Use the Ad-hoc Run feature to immediately trigger a task execution for testing or remediation. You can run it on its primary agent, a selectable alternative agent, or across the entire agent fleet. This requires Admin or Operator role permissions.

## Next Steps

- [Task Runs and Dependencies](./web_task_runs.md)
- [Web Scheduler](./web_scheduler.md)
- [Web Component Overview](./web_component.md)
