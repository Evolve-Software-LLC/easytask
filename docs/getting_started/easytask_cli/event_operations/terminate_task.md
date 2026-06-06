---
title: Terminate Task - EasyTask CLI - EasyTask Documentation
description: Terminate a running task in EasyTask using the terminate_task CLI event command with task name, date, and trigger time.
keywords:
  - terminate task
  - easytask cli
  - kill task
  - task management
---

# Terminate Task Event

The `terminate_task` command in the EasyTask CLI allows users to terminate a specific task by providing its task name, date, and the trigger time.

### Parameters

| Parameter       | Description                                                       |
|-----------------|-------------------------------------------------------------------|
| `--name`        | Name of the task (required, used to specify the task).            |
| `--date`        | Date in `YYYYMMDD` format (required, used to specify the date).   |
| `--trigger_time`| Trigger time for the task (required).   |
| `--instances`    | List of Scheduler instances (required). |

### 🖥️ Basic Usage

```bash
easytask.bin events terminate_task  -h
usage: easytask.bin events terminate_task [-h] --tid TID --name NAME
                                         --date DATE
                                         [--trigger_time TRIGGER_TIME]
                                         --instances INSTANCES

easytask.bin events terminate_task --tid <task_id> --name <task_name> 
--date <task_date> --trigger_time <trigger_time> --instances <instance_name>
```

#### **Sample Output**

```bash

Message published successfully.
Published Terminate Message.

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events terminate_task --name testrunnow --date 20260213 --trigger_time 12:10 --instances 
default
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 18:34:22.736792', 'publish_time': '2026-02-13 18:34:22.836972', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'testrunnow' terminated successfully

```

---

## Frequently Asked Questions

**Q: What is the difference between terminate and disable?**
A: Terminate stops a specific running task instance, while disable prevents all future scheduled runs.

**Q: Is the `--trigger_time` required?**
A: Yes, trigger time identifies the specific task instance to terminate when multiple instances exist.

---

## Next Steps

- [Force Run Task](force_run_task.md) - Force run a task
- [Task Freeze](task_freeze.md) - Freeze a task instead of terminating
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI