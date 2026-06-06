---
title: Bulk Insert Tasks and Groups - EasyTask CLI - EasyTask Documentation
description: Bulk insert multiple tasks and task groups into EasyTask from directories using the insert_many CLI command.
keywords:
  - bulk insert
  - easytask cli
  - insert many
  - batch tasks
---

# Insert Many

You can add both tasks and groups simultaneously or choose to add only one of them as needed, depending on your workflow or organizational requirements for better task management.

## Parameters

| Parameter    | Description                                               |
|--------------|-----------------------------------------------------------|
| `--instance`     | Instance name for the tasks and groups (required).    |
| `--tasks-dir`    | Directory containing task JSON files.                 |
| `--groups-dir`   | Directory containing group JSON files.                |

!!! Schema "Instance Schema"
    ```json 
    { 
    "instance": "sample", # Instance name 
    "active": true, # Instance status
    "description": "Sample instance", # Instance description 
    "timezone": "US/Eastern" # Instance timezone   
    } 
    ```
## 🖥️ Basic Usage

```bash

easytask.bin database bulk_insert insert_many -h
usage: easytask.bin database bulk_insert insert_many [-h] --instance INSTANCE [--tasks-dir TASKS_DIR] [--groups-dir GROUPS_DIR]

options:
  -h, --help              show this help message and exit
  --instance INSTANCE     Instance name for the tasks and groups
  --tasks-dir TASKS_DIR   Directory containing task JSON files
  --groups-dir GROUPS_DIR Directory containing task group JSON files

```

### **Sample Input**
```
easytask.bin database bulk_insert insert_many --instance <instance_name> --tasks-dir <task_dir> --groups-dir <group_dir>

```

### **Sample Output**

```sh

Inserting records.
Records inserted successfully!
|[INFO] Inserting group records...
|[INFO] Group records inserted successfully.

|

```

---

## Frequently Asked Questions

**Q: Can I insert only tasks or only groups?**
A: Yes, use `--tasks-dir` for tasks only, or `--groups-dir` for groups only. At least one is required.

**Q: What file format should the bulk JSON files use?**
A: Each file should follow the same JSON schema as the individual insert commands for tasks or task groups.

---

## Next Steps

- [Insert Task](../task/insert_task.md) - Insert a single task
- [Insert Task Group](../taskgroup/insert_taskgroup.md) - Insert a single task group
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database bulk_insert insert_many --instance default --groups-dir samples/taskgroups 

[INFO] group data is : [{'name': 'sample_taskgroup1', 'day_of_week': '1100000', 'description': 'Run an ls command', 'timezone': 'UTC', 'dependency': '(S:sample_taskgroup)', 'trigger_times': '12:10', 'active': True, 'instance': 'default'}, {'name': 'TG1', 'ordinal_day': 'first sunday of every month', 'description': 'ls command', 'timezone': 'UTC', 'trigger_times': '11:15', 'active': True, 'instance': 'default'}, {'name': 'TG3', 'day_of_week': '1111111', 'trigger_times': '11:15', 'description': 'Run an ls command', 'timezone': 'US/Eastern', 'dependency': '(S:sample_taskgroup)', 'active': True, 'instance': 'default'}]
[INFO] Inserting group records...
[INFO] Group records inserted successfully.

```
