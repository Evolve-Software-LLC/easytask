---
title: Update Task - EasyTask CLI - EasyTask Documentation
description: Update an existing task in the EasyTask database using a JSON or INI file with the database task update CLI command.
keywords:
  - update task
  - easytask cli
  - modify task
  - task configuration
---

# Update Task

The `update` command in the EasyTask CLI allows users to update an existing task in the database using a specified task NAME and an JSON or INI file containing updated task details.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--file`  | Path to a JSON or INI file containing the updated task details. |
| `--name`  | Specifies the NAME of the task to be updated. |
| `--instance`  | Specifies the INSTANCE to which the task belongs. |

!!! Schema "Task Schema"

```json
{

  "name": "task2",
  "task_owner": "new admin",
  "task_group": "TG1",
  "cmd": "ls -l; sleep 3; ls -l  ",
  "run_on_host": "dev1",
  "run_as_user": "evolveadmin",
  "max_run_time": 15,
  "description": "ls command updated",
  "retry_attempts": 2,
  "stdout": "/tmp/2testx22.out",
  "stderr": "/tmp/2testx24.err",
  "profile": "~/.profile",
  "calendar": "INDIAN_HOLIDAYS",
  "active": true
}
```

## 🖥️ Basic Usage

```bash
easytask.bin database task update -h
usage: easytask.bin database task update [-h] --name NAME [--file FILE] --instance INSTANCE

options:
  -h, --help           show this help message and exit
  --name NAME          Task Name
  --file FILE          enter the path of the JSON/INI file containing the task.
  --instance INSTANCE  Instance name for the task

```

### **Sample Input**
```
easytask.bin database task update --name <TASK_NAME> --instance <INSTANCE_NAME> --file /path/to/file.json

```

### **Sample Output**

```sh
Task Validations done.
|[INFO] Refreshed task definition for data_processing_task after deletion
|[INFO] Update Completed!

|

```

---

## Frequently Asked Questions

**Q: Can I update a task without a JSON file?**
A: No, the update command requires a JSON or INI file containing the updated task details.

**Q: Does updating a task require a refresh?**
A: The update command automatically publishes a refresh event, so a manual refresh is not needed.

---

## Next Steps

- [Insert Task](insert_task.md) - Insert a new task
- [Delete Task](delete_task.md) - Delete an existing task
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI
```

(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database task update --name task2 --instance default --file tasks/2.json

Updating task with arguments: {'debug': False, 'category': 'database', 'db_operation': 'task', 'operation': 'update', 'name': 'task2', 'file': '/samples/tasks/2.json', 'instance': 'default', 'func': <function add_db_task_args.<locals>.<lambda> at 0x7f3daeb2fb00>}
[INFO] [easytask_cli_v2:validate_task:1122] Validating task: {'name': 'task2', 'task_owner': 'new admin', 'task_group': 'TG1', 'cmd': 'ls -l; sleep 3; ls -l  ', 'run_on_host': 'dev1', 'run_as_user': 'evolveadmin', 'max_run_time': 15, 'description': 'ls command updated', 'retry_attempts': 2, 'stdout': '/tmp/2testx22.out', 'stderr': '/tmp/2testx24.err', 'profile': '~/.profile', 'calendar': 'INDIAN_HOLIDAYS', 'active': True, 'instance': 'default', 'tid': 1004} for UPDATE
[INFO] Task updated successfully.
[INFO] Message published successfully.
[INFO] Publish Status
[INFO] {'event_time': '2026-02-10 22:51:45.107511', 'publish_time': '2026-02-10 22:51:45.220457', 'status': 'SUCCESS', 'ret_code': 0}
[INFO] eventrecord
[INFO] Refreshed task definition for data_processing_task after deletion
[INFO] Update Completed!

```
