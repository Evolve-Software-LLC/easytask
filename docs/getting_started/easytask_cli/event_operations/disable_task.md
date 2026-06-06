---
title: Disable Task Event - EasyTask CLI - EasyTask Documentation
description: Disable an active task in EasyTask using the disable_task CLI event command with task name and instance parameters.
keywords:
  - disable task
  - easytask cli
  - task scheduling
  - deactivate task
---

# Disable Task Event

The `DISABLE_TASK` event de-activates a task that is in an activate state.

### Parameters

| Parameter       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| `--name`        | Name of the task (required, used to specify the task).           |
| `--instances`    | List of Scheduler instances |

### 🖥️ Basic Usage

```bash
easytask.bin  events disable_task -h
usage: easytask.bin events disable_task [-h] --name NAME --instances INSTANCES

options:
  -h, --help            show this help message and exit
  --name NAME           name of the task or task group
  --instances INSTANCES
                        List of instances.

easytask.bin events disable_task --name task_name --instances Instance_name

```

### **Sample Output**

```sh
 Task disabled successfully
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$  easytask.bin events disable_task --name data_processing_task --instances default
Message published successfully.
|[INFO] Publish Status
|[INFO] {'event_time': '2026-02-13 00:12:34.569473', 'publish_time': '2026-02-13 00:12:34.711323', 'status': 'SUCCESS', 'ret_code': 0}
|[INFO] eventrecord
|[INFO] Task 'data_processing_task' disabled successfully

|```

---

## Frequently Asked Questions

**Q: What happens to a running task when I disable it?**
A: Disabling a task prevents future scheduled runs but does not stop a currently executing task.

**Q: Can I disable multiple tasks at once?**
A: The command disables one task at a time; use separate commands or a script to disable multiple tasks.

**Q: What is the `--instances` parameter?**
A: It specifies the scheduler instance(s) where the disable event should be published.

---

## Next Steps

- [Enable Task](enable_task.md) - Re-enable a disabled task
- [Toggle Task](toggle_task.md) - Toggle between enable and disable states
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI