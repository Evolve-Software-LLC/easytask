---
title: Modify Task Status - EasyTask CLI - EasyTask Documentation
description: Modify the status of a task or task group in EasyTask using the modify_task_status CLI event command.
keywords:
  - modify task status
  - easytask cli
  - task status
  - task management
---

# Modify Task Status Event

The `modify_task_status` command in the EasyTask CLI allows users to modify the status of a task or task group by specifying the name of the task or task group, along with the status and other optional parameters.

## Parameters

| Parameter        | Description                                                     |
|------------------|-----------------------------------------------------------------|
| `--name`         | Name of the task or task group (required).                      |
| `--date`         | Date in `YYYYMMDD` format (required, used to specify the date for status modification). |
| `--status`       | Status to update (required, the new status of the task or task group).|
| `--trigger_time` | Trigger time of the task (required, used to specify a trigger time; the last one is picked if not specified).|
| `--instances`    | List of Scheduler instances (required). |

## 🖥️ Basic Usage

```bash
easytask.bin events modify_task_status  -h
usage: easytask.bin events modify_task_status [-h] --name NAME [--date DATE] --status STATUS --trigger_time TRIGGER_TIME --instances INSTANCES

options:
  -h, --help            show this help message and exit
  --name NAME           name of the task or task group.
  --date DATE           date in YYYYMMDD format.
  --status STATUS       status to update.
  --trigger_time TRIGGER_TIME
                        trigger time of the task, last one picked when not specified
  --instances INSTANCES
                        list of instances

```

### **Sample Output**

```bash

Task status modified.

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events modify_task_status --name data_processing_task  --status A
CTIVE --instances default --trigger_time 12:10 --date 20260213
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 04:24:44.743082', 'publish_time': '2026-02-13 04:24:44.880617', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'data_processing_task' status modified to 'ACTIVE'


```

---

## Frequently Asked Questions

**Q: What statuses can I set using `--status`?**
A: Common statuses include `ACTIVE`, `COMPLETED`, `FAILED`, and `DISABLED`.

**Q: Is the `--trigger_time` parameter always required?**
A: It is required; if multiple trigger times exist, the last one is picked when not specified.

---

## Next Steps

- [Force Run Task](force_run_task.md) - Force run a task immediately
- [Task Freeze](task_freeze.md) - Freeze a task to prevent execution
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI