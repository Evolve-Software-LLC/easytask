---
title: Enable Task Event - EasyTask CLI - EasyTask Documentation
description: Enable a disabled task in EasyTask using the enable_task CLI event command with task name and instance parameters.
keywords:
  - enable task
  - easytask cli
  - task scheduling
  - activate task
---

# Enable Task Event

The `ENABLE_TASK` event activates a task that is in a disabled state.

### Parameters

| Parameter       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| `--name`        | Name of the task (required, used to specify the task).           |
| `--instances`    | List of Scheduler instances |

### 🖥️ Basic Usage

```bash
easytask.bin  events enable_task -h
usage: easytask.bin events enable_task [-h] --name NAME --instances INSTANCES

options:
  -h, --help            show this help message and exit
  --name NAME           name of the task or task group
  --instances INSTANCES
                        List of instances.

easytask.bin events enable_task --name task_name --instances Instance_name

```

### **Sample Output**

```sh
Task enabled successfully
```


### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$  easytask.bin events enable_task --name data_processing_task --instances default
|[INFO]  Message published successfully.
|[INFO]  Publish Status
|[INFO]  {'event_time': '2026-02-12 23:50:35.852398', 'publish_time': '2026-02-12 23:50:35.994362', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO]  eventrecord
|[INFO]  Task 'data_processing_task' enabled successfully

|

```

---

## Frequently Asked Questions

**Q: Can I enable a task that is already active?**
A: Yes, sending an enable event to an already-active task is safe and has no adverse effect.

**Q: How long does it take for the enable event to take effect?**
A: The event is published immediately; the task will be active on the next scheduled trigger.

---

## Next Steps

- [Disable Task](disable_task.md) - Deactivate an active task
- [Force Run Task](force_run_task.md) - Force run a task immediately
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI