---
title: Refresh Calendar - EasyTask CLI - EasyTask Documentation
description: Refresh the EasyTask scheduler calendar to synchronize all scheduled tasks with the latest calendar data.
keywords:
  - refresh calendar
  - easytask cli
  - calendar sync
  - task scheduling
---

# Refresh Calendar Event

The `refresh_calendar` command in the EasyTask CLI is used to refresh the calendar, ensuring that all scheduled tasks are synchronized with the latest calendar data.

### Parameters

This operation does not require any additional parameters.

### 🖥️ Basic Usage

```bash
easytask.bin events refresh_calendar  -h
usage: easytask.bin events refresh_calendar [-h] --instances INSTANCES

options:
  -h, --help            show this help message and exit
  --instances INSTANCES
                        list of instances
                        
easytask.bin events refresh_calendar
```

#### **Sample Output**

```bash

Executing e_refresh_calendar:
Message published successfully.
Publish Status:
{'event_time': '2024-12-04 14:04:40.688335', 
'publish_time': '2024-12-04 14:04:40.744419', 
'status': 'SUCCESS', 
'ret_code': 0 }
Scheduler event record logged successfully.

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events refresh_calendar --instances default
|[INFO]  Message published successfully.
|[INFO]  Publish Status
|[INFO]  {'event_time': '2026-02-12 23:23:15.977045', 'publish_time': '2026-02-12 23:23:16.130746', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO]  eventrecord
|[INFO]  Calendar refreshed successfully
```

---

## Frequently Asked Questions

**Q: When should I refresh the calendar?**
A: Refresh the calendar after updating holiday calendars or making changes to scheduling configurations.

**Q: Does this affect currently running tasks?**
A: No, it only updates the scheduler's calendar cache for future scheduling decisions.

---

## Next Steps

- [Refresh Task Definition](refresh_task_definition.md) - Refresh a specific task definition
- [Refresh Task Group Definition](refresh_task_group_definition.md) - Refresh a task group definition
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI