---
title: Force Run Task - EasyTask CLI - EasyTask Documentation
description: Force run an EasyTask task immediately using the force_run_task CLI event command with task name, date, and instance parameters.
keywords:
  - force run task
  - easytask cli
  - task execution
  - manual trigger
---

# Force Run Task Event

The `force_run_task` command in the EasyTask CLI allows users to force a task to run immediately by specifying the task name, and the date for the task execution.

## Parameters

| Parameter        | Description                                                    |
|------------------|----------------------------------------------------------------|
| `--name`         | Task name (required, the name of the task to be forced to run).|
| `--date`         | Date (required, the date for which the task will be forced to run).|
| `--instances`    | List of Scheduler instances (required). |

## 🖥️ Basic Usage

```bash
easytask.bin events force_run_task -h
usage: easytask.bin events force_run_task [-h] --name NAME
                                         --date DATE --instances
                                         INSTANCES

options:
  -h, --help            show this help message and exit
  --name NAME           name of the task.
  --date DATE           date in YYYYMMDD format.
  --instances INSTANCES
                        list of instances

easytask.bin events force_run_task --name <task_name> --date <execution_date>
```

### **Sample Output**

```sh
Force run triggered for task 'data_processing_task'
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events force_run_task --name data_processing_task --instances default --date 20260213
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 00:26:39.896515', 'publish_time': '2026-02-13 00:26:40.033663', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Force run triggered for task 'data_processing_task'

|

```

---

## Frequently Asked Questions

**Q: What date format should I use for `--date`?**
A: Use the `YYYYMMDD` format, for example `20260213` for February 13, 2026.

**Q: Does force run respect calendar holidays?**
A: Force run bypasses calendar checks and triggers the task regardless of holiday settings.

---

## Next Steps

- [Enable Task](enable_task.md) - Enable a task before force running
- [Modify Task Status](modify_task_status.md) - Change task status after execution
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI