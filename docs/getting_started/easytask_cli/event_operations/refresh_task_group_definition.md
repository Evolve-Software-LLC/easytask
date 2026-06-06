---
title: Refresh Task Group Definition - EasyTask CLI - EasyTask Documentation
description: Refresh the definition of a task group in EasyTask using the refresh_task_group_definition CLI event command.
keywords:
  - refresh task group definition
  - easytask cli
  - task group
  - group configuration
---

# Refresh Task Group Definition Event

The `refresh_task_group_definition` command in the EasyTask CLI allows users to refresh the definition of a task group by specifying the task group name, and optionally the date.

### Parameters

| Parameter | Description                                             |
|-----------|---------------------------------------------------------|
| `--name`  | Name of the task group (required, used to identify the task group). |
| `--instances`    | List of Scheduler instances (required). |

### 🖥️ Basic Usage

```bash
easytask.bin events refresh_task_group_definition  -h
usage: easytask.bin events refresh_task_group_definition [-h] --name NAME --instances INSTANCES

options:
  -h, --help            show this help message and exit
  --name NAME           name of the task group.
  --instances INSTANCES
                        List of instances.

easytask.bin events refresh_task_group_definition 
--name <task_group_name>  --instances instance_name
```

#### **Sample Output**

```bash

Message published successfully.
Scheduler event record logged successfully.
Task group definition refreshed successfully

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events refresh_task_group_definition --name TG1 --instances default
|[INFO] Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 17:32:50.908457', 'publish_time': '2026-02-13 17:32:51.045116', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task group 'TG1' definition refreshed successfully

```

---

## Frequently Asked Questions

**Q: What is the difference between refreshing a task group vs. a task definition?**
A: Task group refresh reloads the group's schedule and dependency graph, while task definition refresh reloads individual task configuration.

**Q: Do I need to refresh after inserting a new task group?**
A: The insert command typically triggers an automatic refresh, but you can manually refresh if needed.

---

## Next Steps

- [Refresh Task Definition](refresh_task_definition.md) - Refresh an individual task definition
- [Refresh Calendar](refresh_calender.md) - Refresh the scheduler calendar
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI