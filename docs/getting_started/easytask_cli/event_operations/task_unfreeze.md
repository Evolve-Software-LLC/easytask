---
title: Task Unfreeze - EasyTask CLI - EasyTask Documentation
description: Unfreeze a frozen task in EasyTask using the task_unfreeze CLI event command with task name, date, and trigger time.
keywords:
  - task unfreeze
  - easytask cli
  - unfreeze task
  - task control
---

# Task Unfreeze Event

The `task_unfreeze` command in the EasyTask CLI allows users to unfreeze a specific task by providing its task name, date, and the trigger time.

### Parameters

| Parameter       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| `--name`        | Name of the task (required, used to specify the task).           |
| `--date`        | Date for the task (required, used to specify the date).          |
| `--trigger_time`| Trigger time for the task (required).  |
| `--instances`    | List of Scheduler instances (required). |

### 🖥️ Basic Usage

```bash
easytask.bin events task_unfreeze  -h
usage: easytask.bin events task_unfreeze [-h] --name NAME
                                        --date DATE
                                        [--trigger_time TRIGGER_TIME]
                                        --instances INSTANCES

easytask.bin events task_unfreeze --name <task_name> 
--date <task_date> --trigger_time <trigger_time> --instances <instance_name>
```

#### **Sample Output**

```bash

Message published successfully.
Scheduler event record logged successfully.
Published Unfreeze Message.

```

### **Example**

```

(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events task_unfreeze --name data_processing_task --date 20260213 --trigger_time 12:10 --i
nstances default
|[INFO] Message published successfully.
|[INFO] Publish Status
{'event_time': '2026-02-13 18:12:56.413274', 'publish_time': '2026-02-13 18:12:56.546291', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'data_processing_task' unfrozen successfully

|

```

---

## Frequently Asked Questions

**Q: What happens after unfreezing a task?**
A: The task resumes its normal schedule and will execute on the next scheduled trigger time.

**Q: Do I need to match the same date and trigger time used to freeze?**
A: Yes, provide the same date and trigger time to unfreeze the correct task instance.

---

## Next Steps

- [Task Freeze](task_freeze.md) - Freeze a task
- [Enable Task](enable_task.md) - Enable a disabled task
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI