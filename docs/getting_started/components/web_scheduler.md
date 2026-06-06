---
title: Scheduler UI - EasyTask Documentation
description: Use the EasyTask Scheduler UI to manage scheduler instances, monitor real-time scheduler health, inject control events, and track event history.
keywords:
  - scheduler UI
  - easytask
  - scheduler status
  - scheduler instances
  - scheduler events
  - web scheduler
---

## 📅 Scheduler UI

The Scheduler UI provides a centralized interface to manage, monitor, and control scheduler operations. It helps administrators and users oversee task execution, instance management, event handling, and system health — all from one place.

---

### 📌 Scheduler Instances

  
  

The **Instances** page allows you to:

- ➕ **Create scheduler instances** by entering an instance name, assigning roles, and setting Podman or SSH details.
- ✏️ **Update instances** to modify properties like Podman host, ports, or assigned roles.
- 🗑️ **Delete instances** securely with a confirmation dialog to avoid accidental removal.

💡 **Example Use Case:**  
Create a test instance for developers, configure its Podman host, and assign the `admin` and `developers` roles. You can later update or delete the instance as needed.

---

### 📊 Scheduler Status   

The **Status** page offers a real-time overview of scheduler health.

✅ **What it provides:**

- Display of current instance name and ID.
- Count of **connected workers**.
- Status of the scheduler (e.g., **UP**, **DOWN**, last start time).
- Detailed configuration information:
    - DB name
    - Status & task tables
    - Event channel
    - Message broker
- **Scheduler Threads Status**:
    - Processing, Submitter, Transition, Admin Channel, and Midnight Crossover threads — each showing whether it’s **Active** or **Inactive**.

💡 **Example Use Case:**  
Check if the production scheduler is running with at least 5 connected workers and all critical threads are active before a major deployment.

---

### ⏰ Events

The **Events** page lets you manage injected events and monitor event history.

✅ **What you can do:**

- Inject control events like:
    - `ENABLE_DEBUG`
    - `DISABLE_DEBUG`
    - `REFRESH_CALENDAR`
    - `REFRESH_TASK_DEFINITION`
    - `FORCE_RUN_TASK`
- Filter and search events using:
    - Date ranges
    - Published By
    - Task Name
    - Event Name
    - Timezone
    - Result status (SUCCESS / FAILURE)
- View detailed event logs, timestamps, and execution results.
- Track publish messages for troubleshooting and auditing.

💡 **Example Use Case:**  
After adding a new holiday calendar, inject a `REFRESH_CALENDAR` event to ensure all schedulers reload the updated calendar data.

---

## ✅ Summary

The Scheduler UI empowers you to:

- 🚀 Streamline instance management
- 📈 Monitor real-time scheduler health
- ⏳ Inject and track critical system events
- 🛡️ Maintain operational reliability with confidence

---

## Frequently Asked Questions

**Q: How do I create a new scheduler instance from the UI?**
A: Navigate to the Scheduler Instances page, click to create a new instance, enter an instance name, assign roles, and set Podman or SSH details. Save to create the instance.

**Q: What does the Scheduler Status page show?**
A: The Status page provides a real-time overview including the instance name and ID, connected worker count, scheduler status (UP/DOWN), configuration details (DB name, tables, event channel, broker), and thread status for processing, submitter, transition, admin channel, and midnight crossover.

**Q: How do I inject an event like REFRESH_CALENDAR?**
A: Go to the Events page in the Scheduler UI, select the event type (e.g., `REFRESH_CALENDAR`), and submit it. You can filter and track event history by date, publisher, task name, and result status.

## Next Steps

- [Scheduler Events](./scheduler_events.md)
- [Scheduler Instance](./scheduler_instance.md)
- [Web Component Overview](./web_component.md)
