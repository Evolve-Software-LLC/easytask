---
title: Insert Task Group - EasyTask CLI - EasyTask Documentation
description: Insert a new task group into the EasyTask database from a JSON or INI file using the database taskgroup insert CLI command.
keywords:
  - insert task group
  - easytask cli
  - create taskgroup
  - task group configuration
---

# Insert Task Group

The `insert` command in the EasyTask CLI allows users to insert a task group into the database by providing the path to a JSON or INI file containing the task group data.

## Parameters

| Parameter    | Description                                              |
|--------------|----------------------------------------------------------|
| `--file`     | Enter the path of the JSON or INI file containing the task group. |
| `--instance`  | Specifies the INSTANCE to which the task group belongs. |

!!! Schema  "Taskgroup Schema"
```json
{
    "name": "sample_taskgroup",
    "day_of_week": "1111110",
    "description": "Run an ls command",
    "timezone": "US/Eastern",
    "trigger_times": "12:10",
    "active": true,
    "dependency": ""
    
}
```

## 🖥️ Basic Usage

```bash
easytask.bin database taskgroup insert  -h
usage: easytask.bin database taskgroup insert [-h] [--file FILE] --instance INSTANCE

options:
  -h, --help           show this help message and exit
  --file FILE          enter the path of the JSON/INI file containing the taskgroup.
  --instance INSTANCE  Instance name for the taskgroup
```

### **Sample Input**
```
easytask.bin database taskgroup insert
--file <file_path> --instance <instance_name>

```

### **Sample Output**

```bash

Task Validations done
Taskgroup inserted successfully.
Insert Completed!
|[INFO]  Refreshed taskgroup definition for sample_taskgroup after deletion
|[INFO]  Insert Completed!

|

```

---

## Frequently Asked Questions

**Q: What file formats are supported for task group insertion?**
A: Both JSON and INI file formats are supported for defining task group configurations.

**Q: How do I set dependencies between task groups?**
A: Use the `dependency` field in the task group JSON with the syntax `(S:GROUP_NAME)` for sequential dependencies.

---

## Next Steps

- [Update Task Group](update_taskgroup.md) - Update an existing task group
- [Query Task Group](query_taskgroup.md) - Look up task group definitions
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$  easytask.bin database taskgroup insert --file taskgroups/2.json --instance default

[INFO]  Validating taskgroup: {'name': 'sample_taskgroup', 'day_of_week': '1111110', 'description': 'Run an ls command', 'timezone': 'US/Eastern', 'trigger_times': '12:10', 'active': True, 'instance': 'default', 'gid': 15, 'non_mandatory_fields': {'dependency': '(S:TG1)'}} for insert
[INFO]  Taskgroup inserted successfully.
[INFO]  Message published successfully.
[INFO]  Publish Status
[INFO]  {'event_time': '2026-02-11 22:29:12.159144', 'publish_time': '2026-02-11 22:29:12.271352', 'status': 'SUCCESS', 'ret_code': 0}
[INFO]  eventrecord
[INFO]  Refreshed taskgroup definition for sample_taskgroup after deletion
[INFO]  Insert Completed!

```