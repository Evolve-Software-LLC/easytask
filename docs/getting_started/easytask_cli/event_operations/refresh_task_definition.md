---
title: Refresh Task Definition - EasyTask CLI - EasyTask Documentation
description: Refresh the definition of a specific task in EasyTask using the refresh_task_definition CLI event command.
keywords:
  - refresh task definition
  - easytask cli
  - task definition
  - task configuration
---

# Refresh Task Definition Event

The `refresh_task_definition` command in the EasyTask CLI allows users to refresh the definition of a specific task by specifying the task name.

### Parameters

| Parameter  | Description                                               |
|------------|-----------------------------------------------------------|
| `--name`   | Name of the task (required, used to specify the task).    |
| `--instances`    | List of Scheduler instances (required). |

### 🖥️ Basic Usage

```bash

easytask.bin events refresh_task_definition  -h
usage: easytask.bin events refresh_task_definition [-h] --name NAME --instances INSTANCES

options:
  -h, --help             show this help message and exit
  --name NAME            name of the task.
  --instances INSTANCES  List of instances.

easytask.bin events refresh_task_definition  --name <task_name> --instances instance_name

```

#### **Sample Output**

```bash

Message published successfully.
Scheduler event record logged successfully.
Task definition refreshed successfully
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events refresh_task_definition --name data_processing_task --inst
ances default
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 04:41:53.170407', 'publish_time': '2026-02-13 04:41:53.309453', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'data_processing_task' definition refreshed successfully


```

---

## Frequently Asked Questions

**Q: When should I refresh a task definition?**
A: Refresh after updating a task's configuration in the database to ensure the scheduler picks up the changes.

**Q: Does refresh cause the task to run immediately?**
A: No, refresh only reloads the task definition; the task runs on its next scheduled trigger time.

---

## Next Steps

- [Refresh Task Group Definition](refresh_task_group_definition.md) - Refresh a task group definition
- [Refresh Calendar](refresh_calender.md) - Refresh the scheduler calendar
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI
