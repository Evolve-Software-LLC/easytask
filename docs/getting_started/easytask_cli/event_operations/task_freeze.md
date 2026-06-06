---
title: Task Freeze - EasyTask CLI - EasyTask Documentation
description: Freeze a specific task in EasyTask using the task_freeze CLI event command with task name, date, and trigger time.
keywords:
  - task freeze
  - easytask cli
  - freeze task
  - task control
---

# Task Freeze Event

The `task_freeze` command in the EasyTask CLI allows users to freeze a specific task by providing its task name, date, and  the trigger time.

### Parameters

| Parameter       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| `--name`        | Name of the task (required, used to specify the task).           |
| `--date`        | Date for the task (required, used to specify the date).          |
| `--trigger_time`| Trigger time for the task (required).  |
| `--instances`    | List of Scheduler instances (required). |

### 🖥️ Basic Usage

```bash
easytask.bin events task_freeze  -h
usage: easytask.bin events task_freeze [-h] --name NAME
                                      --date DATE
                                      [--trigger_time TRIGGER_TIME] 
                                      --instances INSTANCES

easytask.bin events task_freeze --name <task_name> 
--date <task_date> --trigger_time <trigger_time> --instances <instance_name>
```

#### **Sample Output**

```bash

Message published successfully.
Scheduler event record logged successfully.
Task frozen successfully

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events task_freeze --name data_processing_task --date 20260213 --trigger_time 12:10 --instances default
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 17:50:39.561555', 'publish_time': '2026-02-13 17:50:39.698897', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'data_processing_task' frozen successfully

```

---

## Frequently Asked Questions

**Q: What is the difference between freezing and disabling a task?**
A: Freezing holds a specific task instance at a given date and trigger time, while disabling prevents all future runs of the task.

**Q: Can I freeze a task that is already running?**
A: Freezing prevents the next scheduled run but does not stop a currently executing task instance.

---

## Next Steps

- [Task Unfreeze](task_unfreeze.md) - Unfreeze a frozen task
- [Disable Task](disable_task.md) - Disable a task entirely
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI