---
title: Query Task Group - EasyTask CLI - EasyTask Documentation
description: Query task groups from the EasyTask database using various filtering options like name, description, and active status.
keywords:
  - query task group
  - easytask cli
  - search taskgroup
  - task group lookup
---

# Query Task Group 

The `query` command in the EasyTask CLI allows users to query task groups from the database based on various filtering options such as name, description, active, and more.

## Parameters

| Parameter               | Description                                               |
|-------------------------|-----------------------------------------------------------|
| `--name`                | Task group name (string).                                 |
| `--day_of_week`         | Days of the week the task group runs (string).            |
| `--ordinal_day`         | Ordinal days for task group scheduling (string).          |
| `--description`         | Description of the task group (string).                   |
| `--timezone`            | Timezone for the task group (string).                     |
| `--dependency`          | Dependency of the task group (string).                    |
| `--trigger_times`       | Specific trigger times for the task group (string).       |
| `--active`              | Whether the task group is active (boolean).               |
| `--instance`            | Instance of the task group (string).                            |

## 🖥️ Basic Usage

```bash
easytask.bin database taskgroup query  -h 
usage: easytask.bin database taskgroup query 
  [-h]
  [--name NAME]
  [--day_of_week DAY_OF_WEEK]
  [--ordinal_day ORDINAL_DAY]
  [--description DESCRIPTION]
  [--timezone TIMEZONE]
  [--dependency DEPENDENCY]
  [--trigger_times TRIGGER_TIMES]
  [--active ACTIVE]
  [--instance INSTANCE]
```

### **Sample Input**
```
easytask.bin database taskgroup query --<parameter_name> <value> --<parameter_name> "<value with spaces>"

```

### **Sample Output**

```bash

Total <count> tasks found: 
{
  "<field_name>": <value>,
  "<field_name>": "<string_value>",
  "<field_name>": <number_value>,
  "<field_name>": <boolean_value>
}
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database taskgroup query --name TG4

Taskgroup: {'_sa_instance_state': <sqlalchemy.orm.state.InstanceState object at 0x7f31e7f861b0>, 'name': 'TG4', 'trigger_times': '11:40,12:00,12:05,12:10,12:15', 'gid': 11, 'active': True, 'description': 'test', 'timezone': 'America/New_York', 'instance': 'default', 'day_of_week': '1000111'}

|

```

|

---

## Frequently Asked Questions

**Q: Can I query task groups without any filter parameters?**
A: Yes, running `query` without filters returns all task groups in the database.

**Q: How do I find inactive task groups?**
A: Use the `--active false` parameter to filter for inactive task groups.

---

## Next Steps

- [Insert Task Group](insert_taskgroup.md) - Insert a new task group
- [Update Task Group](update_taskgroup.md) - Update an existing task group
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI