---
title: Delete Task Group - EasyTask CLI - EasyTask Documentation
description: Delete a task group from the EasyTask database using the database taskgroup delete CLI command by group name.
keywords:
  - delete task group
  - easytask cli
  - remove taskgroup
  - task group management
---

# Delete Task Group 

The `delete` command in the EasyTask CLI allows users to delete a task group from the database by specifying the group NAME.

## Parameters

| Parameter    | Description                                              |
|--------------|----------------------------------------------------------|
| `--name`      | Name of the task group to be deleted (string).     |
| `--instance`  | Specifies the INSTANCE to which the task belongs (string). |

## 🖥️ Basic Usage

```bash
easytask.bin database taskgroup delete  -h 
usage: easytask.bin database taskgroup delete [-h] --name NAME --instance INSTANCE [--force]

options:
  -h, --help           show this help message and exit
  --name NAME          Taskgroup name to delete
  --instance INSTANCE  Instance identifier for the taskgroup
  --force              Force delete dependent tasks
```

### **Sample Input**
```
easytask.bin database taskgroup delete --name Name --instance INSTANCE

```

### **Sample Output**

```sh
Taskgroup deleted.
All taskgroups and their references deleted successfully.

```

### **Example**

```

(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$  easytask.bin database taskgroup delete --name TG11 --instance default --force

Deleting taskgroup with arguments: {'debug': False, 'category': 'database', 'db_operation': 'taskgroup', 'operation': 'delete', 'name': 'TG11', 'instance': 'default', 'force': False, 'func': <function add_db_taskgroup_args.<locals>.<lambda> at 0x7f82c1540720>}
2026-03-02 01:12:30.809282 [INFO] [easytask_cli_v2:validate_taskgroup:2430] Validating taskgroup: {'gid': 3, 'name': 'TG11', 'instance': 'default'} for DELETE
[INFO]  Taskgroup TG11 deleted.
[INFO]  Message published successfully.
[INFO]  Publish Status
[INFO]  {'event_time': '2026-03-02 01:12:30.880219', 'publish_time': '2026-03-02 01:12:30.978722', 'status': 'SUCCESS', 'ret_code': 0}
[INFO]  eventrecord
[INFO]  Task group 'TG11' definition refreshed successfully
[INFO]  Refreshed taskgroup definition for TG11 after deletion
[INFO]  All taskgroups and their references deleted successfully.



```

---

## Frequently Asked Questions

**Q: What does the `--force` flag do?**
A: The `--force` flag forces deletion of the task group along with all its dependent tasks.

**Q: Can I recover a deleted task group?**
A: No, deletion is permanent. Re-insert the task group using the insert command if needed.

---

## Next Steps

- [Insert Task Group](insert_taskgroup.md) - Insert a new task group
- [Update Task Group](update_taskgroup.md) - Update an existing task group
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI