---
title: Toggle Task - EasyTask CLI - EasyTask Documentation
description: Enable or disable a task or task group in EasyTask using the toggle task CLI event commands.
keywords:
  - toggle task
  - easytask cli
  - enable disable task
  - task control
---

# Toggle Task Event

## Enable Task 

The `enable_task` command in the EasyTask CLI allows users to enable a task or a task group by specifying the name of the task or task group.

### Parameters

| Parameter        | Description                                                    |
|------------------|----------------------------------------------------------------|
| `--name`         | Name of the task or task group.                     |
| `--instances`    | List of Scheduler instances |

## 🖥️ Basic Usage

To enable a task or task group by its name use the following command in the CLI:

```sh
easytask.bin events enable_task --name <task_or_group_name>  --instances INSTANCES
```

<br></br>

## Disable Task

The `disable_task` command in the EasyTask CLI allows users to disable a task or a task group by specifying  name of the task or task group.

### Parameters

| Parameter        | Description                                                    |
|------------------|----------------------------------------------------------------|
| `--name`         | Name of the task or task group (required).                     |
| `--instances`    | List of Scheduler instances |

### 🖥️ Basic Usage

To disable a task or task group by its name use the following command in the CLI:

```bash
easytask.bin event disable_task --name <task_or_group_name> --instances INSTANCE
```

<br></br>

---

## Frequently Asked Questions

**Q: What is the difference between toggle_task and the individual enable/disable commands?**
A: Toggle task is a combined reference page; the individual `enable_task` and `disable_task` commands work the same way.

**Q: Can I toggle a task group?**
A: Yes, both enable_task and disable_task accept task group names via the `--name` parameter.

---

## Next Steps

- [Enable Task](enable_task.md) - Detailed enable task documentation
- [Disable Task](disable_task.md) - Detailed disable task documentation
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI
