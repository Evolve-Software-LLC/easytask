---
title: Scheduler Events - EasyTask Documentation
description: Guide to EasyTask Scheduler events including scheduler events, task events, and admin events for controlling task scheduling and system behavior.
keywords:
  - scheduler events
  - easytask
  - task events
  - scheduler debugging
  - force run task
---

# 📄 EasyTask Scheduler Events Guide

The **EasyTask Scheduler** uses three main types of broker events to control its behavior and manage tasks effectively:

| 💡 Event Type        | 🔧 Purpose                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------|
| 📅 Scheduler Events | Debugging, holiday calendar refreshes                                                        |
| 📋 Task Events      | Modifying task scheduling, status, and behavior                                              |
| 🛡️ Admin Events    | Software, configuration, and license management (internal use)                              |

---

### 📅 Scheduler Events

#### Enable Debug 

- ``ENABLE_DEBUG`` Event enables detailed logging in debug mode, allowing operators to observe internal states, task dependencies, event processing, and scheduling decisions in real time.   

  🔗 [💻 CLI](../easytask_cli/event_operations/toggle_debug.md)

#### Disable Debug 
- ``DISABLE_DEBUG`` Event returns logging to standard info mode, which limits output to essential messages.    

  🔗 [💻 CLI](../easytask_cli/event_operations/toggle_debug.md)

#### Refresh Calendar
- ``REFRESH_CALENDAR`` Event reloads all holiday and blackout calendars from the database and updates scheduler data structures.  
  📌 **Example:** If a task follows the ``US_HOLIDAYS`` calendar and a new holiday is added, the task will be automatically skipped on that day.  
  
  🔗 [💻 CLI](../easytask_cli/event_operations/refresh_calender.md)

---

### 📋 Task Events

#### Refresh Task Definition
- ``REFRESH_TASK_DEFINITION`` Event reloads the definition of an individual task after changes in the database, such as updated trigger intervals or modified dependencies.  
  📌 **Example:** If a task’s interval is changed from hourly to daily, this event must be sent for the change to take effect.  

  🔗 [💻 CLI](../easytask_cli/event_operations/refresh_task_definition.md)

#### Refresh Task Group Definition

- ``REFRESH_TASK_GROUP_DEFINITION`` Event updates a task group when its composition or rules change.  

  🔗 [💻 CLI](../easytask_cli/event_operations/refresh_task_group_definition.md)

#### Enable Task
- ``ENABLE_TASK`` Event activates a task that was inactive (disabled) at scheduler startup, loads its definition, and creates a live schedule for it.  

  🔗 [💻 CLI](../easytask_cli/event_operations/enable_task.md)

#### Disable Task

- ``DISABLE_TASK``  Event deactivates a currently scheduled task, removing it from the near-future run queue.  

  🔗 [💻 CLI](../easytask_cli/event_operations/disable_task.md)

#### Freeze Task
- ``FREEZE_TASK`` Event temporarily halts a task for the current day, respecting its timezone.  
  📌 **Example:** Freeze a task to skip execution today due to a critical upstream system outage.  

  🔗 [💻 CLI](../easytask_cli/event_operations/task_freeze.md)

#### Unfreeze Task
- ``UNFREEZE_TASK`` Event reactivates a frozen task.  
  📌 **Note:** If unfrozen after the scheduled time or when dependencies are already complete, it may **not** run until the next trigger or reset.  

  🔗 [💻 CLI](../easytask_cli/event_operations/task_unfreeze.md)

#### Force Run Task
- ``FORCE_RUN_TASK`` Event immediately triggers a task regardless of its schedule or dependency status.  

  🔗 [💻 CLI](../easytask_cli/event_operations/force_run_task.md)

#### Modify Task Status
- ``MODIFY_TASK_STATUS`` Event enables manual updates to the current status of a task (e.g., FAILED → SUCCESS) to influence downstream flows.  
  📌 **Example:** After a manual fix, marking it SUCCESS will allow dependent tasks to proceed.  

  🔗 [💻 CLI](../easytask_cli/event_operations/modify_task_status.md)

#### Terminate Task
- ``TERMINATE_TASK``  Event forcefully stops a running task by sending a termination signal.  

  🔗 [💻 CLI](../easytask_cli/event_operations/terminate_task.md)

---

### 🛡️ **Admin Events**

- Used internally for software updates, configuration adjustments, and license management.

---

### ✅ **Summary Table**

| 🔑 Category         | 💥 Examples                                                  |
|---------------------|-------------------------------------------------------------|
| 📅 Scheduler Events | ENABLE_DEBUG, DISABLE_DEBUG, REFRESH_CALENDAR              |
| 📋 Task Events      | ENABLE_TASK, DISABLE_TASK, FREEZE_TASK, FORCE_RUN_TASK     |
| 🛡️ Admin Events    | Internal software, config, and license updates             |

---

### ⚠️ **Best Practices**

- Use **debug mode** only during troubleshooting.
- Always send **refresh events** after changing definitions in the database.
- Be cautious with **force-run** and **terminate** to avoid disrupting production.

---

## Frequently Asked Questions

**Q: What is the difference between FREEZE_TASK and DISABLE_TASK?**
A: `FREEZE_TASK` temporarily halts a task for the current day only (respecting its timezone), while `DISABLE_TASK` completely deactivates a task, removing it from the run queue until explicitly re-enabled with `ENABLE_TASK`.

**Q: When should I use REFRESH_TASK_DEFINITION?**
A: Send a `REFRESH_TASK_DEFINITION` event after making changes to a task's definition in the database, such as updating trigger intervals, modifying dependencies, or changing command attributes. Without this event, the scheduler will continue using the cached definition.

**Q: How do I trigger a task to run immediately outside its schedule?**
A: Use the `FORCE_RUN_TASK` event to immediately trigger a task regardless of its schedule or dependency status. This is useful for testing, remediation, or emergency re-runs. Be cautious in production environments.

## Next Steps

- [Scheduler Overview](./scheduler_new.md)
- [Scheduler Management](./scheduler_management.md)
- [Scheduler Instance](./scheduler_instance.md)
