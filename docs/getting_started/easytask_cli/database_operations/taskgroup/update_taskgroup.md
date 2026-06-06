---
title: Update Task Group - EasyTask CLI - EasyTask Documentation
description: Update an existing task group in the EasyTask database using a JSON or INI file with the database taskgroup update CLI command.
keywords:
  - update task group
  - easytask cli
  - modify taskgroup
  - task group configuration
---

# Update Task Group

The `update` command in the EasyTask CLI allows users to update an existing task group in the database by providing the path to a JSON or INI file containing the updated task group data.

## Parameters

| Parameter    | Description                                              |
|--------------|----------------------------------------------------------|
| `--file`     | Enter the path of the JSON or INI file containing the updated task group. |
| `--name`  | Specifies the NAME of the task group to be updated. |
| `--instance`  | Specifies the INSTANCE to which the task group belongs. |

!!! Schema "Taskgroup Schema"
```json
{
    "name": "sample_taskgroup",
    "day_of_week": "1100000",
    "description": "Run an ls command",
    "timezone": "UTC",
    "trigger_times": "12:10",
    "active": true,
    "non_mandatory_fields": {
        "dependency": "(S:TG1)"
    }
}
```

## 🖥️ Basic Usage

```bash
easytask.bin database taskgroup update -h
usage: easytask.bin database taskgroup update [-h] [--file FILE] --name NAME --instance INSTANCE

options:
  -h, --help           show this help message and exit
  --file FILE          enter the path of the JSON/INI file containing the taskgroup.
  --name NAME          Task Name
  --instance INSTANCE  Instance name for the taskgroup
```

### **Sample Input**
```
easytask.bin database taskgroup update --file <file_path> --name NAME --instance INSTANCE

```

### **Sample Output**

```sh

TaskGroup Validations done
Taskgroup updated successfully.
Update Completed!

```

### **Example**

```

(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database taskgroup update --name sample_taskgroup  --file taskgroups/2.json --instance default

[INFO] [easytask_cli_v2:validate_taskgroup:2068] Validating taskgroup: {'name': 'sample_taskgroup', 'day_of_week': '1100000', 'description': 'Run an ls command', 'timezone': 'UTC', 'trigger_times': '12:10', 'active': True, 'instance': 'default', 'gid': 15, 'non_mandatory_fields': {'dependency': '(S:TG1)'}} for UPDATE
[INFO] [easytask_cli_v2:update_taskgroup:2235] Taskgroup updated successfully.
[INFO] [util:publish_to_message_broker:70] Message published successfully.
[INFO] [util:audit_event:100] Publish Status
[INFO] [util:audit_event:101] {'event_time': '2026-02-11 22:56:11.912110', 'publish_time': '2026-02-11 22:56:12.037441', 'status': 'SUCCESS', 'ret_code': 0}
[INFO] [util:audit_event:126] eventrecord
[INFO] [easytask_cli_v2:update_taskgroup:2246] Refreshed taskgroup definition for sample_taskgroup after deletion
[INFO] [easytask_cli_v2:print_failures:2323] Update Completed!




```

---

## Frequently Asked Questions

**Q: Can I update a task group without a JSON file?**
A: No, the update command requires a JSON or INI file containing the updated task group details.

**Q: Does updating a task group refresh its definition automatically?**
A: Yes, the update command automatically publishes a refresh event for the updated task group.

---

## Next Steps

- [Insert Task Group](insert_taskgroup.md) - Insert a new task group
- [Delete Task Group](delete_taskgroup.md) - Delete a task group
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI