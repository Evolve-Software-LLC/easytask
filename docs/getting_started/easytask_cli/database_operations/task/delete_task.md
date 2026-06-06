---
title: Delete Task - EasyTask CLI - EasyTask Documentation
description: Delete an existing task from the EasyTask database using the database task delete CLI command by task name.
keywords:
  - delete task
  - easytask cli
  - remove task
  - task database
---

# Delete Task 

The `delete` command in the EasyTask CLI allows users to delete an existing task from the database by specifying the task NAME.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--name`  | Specifies the NAME of the task to be deleted. |
| `--instance`  | Specifies the INSTANCE to which the task belongs. |

<!-- !!! Schema inline start "Task Schema"
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
    ``` -->

## 🖥️ Basic Usage

```bash
easytask.bin database task delete -h 
usage: easytask.bin database task delete [-h] --name NAME --instance INSTANCE

options:
  -h, --help  show this help message and exit
  --name NAME          Task name to delete
  --instance INSTANCE  Instance identifier for the task

```

### **Sample Input**
```
easytask.bin database task delete --name task_name --instance default

```

### **Sample Output**

```bash 
Task Validations done 
All tasks deleted successfully..

```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database task delete --name task2 --instance default

Deleting task with arguments: {'debug': False, 'category': 'database', 'db_operation': 'task', 'operation': 'delete', 'name': 'task2', 'instance': 'default', 'func': <function add_db_task_args.<locals>.<lambda> at 0x7f207a4dbce0>}
[INFO] [easytask_cli_v2:validate_task:1446] Validating task: {'tid': 1004, 'instance': 'default', 'name': 'task2'} for DELETE
[INFO] Message published successfully.
[INFO] Publish Status
[INFO] {'event_time': '2026-02-10 23:38:23.233196', 'publish_time': '2026-02-10 23:38:23.374251', 'status': 'SUCCESS', 'ret_code': 0}
[INFO] eventrecord
[INFO] All tasks deleted successfully.

```

---

## Frequently Asked Questions

**Q: Can I recover a deleted task?**
A: No, deletion is permanent. Re-insert the task using the insert command if needed.

**Q: Does deleting a task stop its currently running instance?**
A: No, you need to use the `terminate_task` event command to stop a running instance.

---

## Next Steps

- [Insert Task](insert_task.md) - Insert a new task
- [Update Task](update_task.md) - Update an existing task
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI
