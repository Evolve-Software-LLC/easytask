---
title: Query Task Runs - EasyTask CLI - EasyTask Documentation
description: Query task run history in EasyTask using the database taskrun query CLI command with various filtering parameters.
keywords:
  - query task runs
  - easytask cli
  - task run history
  - task run logs
---

# Query Task Runs

The `query` command in the EasyTask CLI allows users to query task runs based on various filtering parameters.

## Parameters

| Parameter          | Description                                                 |
|--------------------|-------------------------------------------------------------|
| `--id`             | Primary key ID of the task run (optional).                  |
| `--tid`            | Task ID (optional).                                         |
| `--date`           | Date of the task run (optional).                            |
| `--name`           | Name of the task (optional).                                |
| `--task_group`     | Task group name (optional).                                 |
| `--pid`            | Process ID (optional).                                      |
| `--job_id`         | Job ID (optional).                                          |
| `--day_of_week`    | Days of the week the task runs (optional).                  |
| `--local_trigger_times` | Local trigger times for the task run (optional).          |
| `--trigger_times`  | Trigger times for the task (optional).                      |
| `--dep_fields`     | Dependency fields (optional).                               |
| `--start_time`     | Start time of the task run (optional).                      |
| `--end_time`       | End time of the task run (optional).                        |
| `--status`         | Status of the task run (optional).                          |
| `--duration`       | Duration of the task run in seconds (optional).             |
| `--ret_code`       | Return code for the task run (optional).                    |
| `--dependency`     | Dependency for the task run (optional).                     |
| `--timezone`       | Timezone for the task run (optional).                       |
| `--host_name`      | Host name where the task ran (optional).                    |
| `--created_on`     | Creation time of the task run (optional).                   |

## 🖥️ Basic Usage

```bash
easytask.bin database taskrun query
--<parameter_name> <value>
--<parameter_name> "<value with spaces>"
...
```

### **Sample Output**

```bash
Querying task with arguments: {<query_parameters>}
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
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$  easytask.bin database taskrun query --tid 2

Total 10 task runs found: 

{'_sa_instance_state': <sqlalchemy.orm.state.InstanceState object at 0x7f79b6cac050>, 'task_group': '', 'status': 'ACTIVE', 'log_file': '', 'pid': 99999, 'duration': 0, 'job_id': '', 'ret_code': 99999, 'day_of_week': '1111111', 'dependency': '', 'tid': 2, 'local_trigger_times': '22/01/2026 07:19', 'timezone': 'US/Eastern', 'id': 37030401, 'trigger_times': '22/01/2026 12:19', 'host_name': '', 'date': 20260122, 'start_time': datetime.datetime(2026, 1, 22, 12, 18, tzinfo=datetime.timezone.utc), 'instance': 'default', 'name': 'easytask call_home', 'end_time': datetime.datetime(1970, 1, 1, 0, 0, tzinfo=datetime.timezone.utc), 'created_on': datetime.datetime(2026, 1, 22, 12, 18, 0, 529568, tzinfo=datetime.timezone.utc)} ........


```

---

## Frequently Asked Questions

**Q: Can I filter task runs by a date range?**
A: Yes, use the `--date` parameter to filter runs for a specific date; for ranges, issue multiple queries.

**Q: What does the `_sa_instance_state` field mean?**
A: It is an internal SQLAlchemy object; it can be ignored when reviewing task run data.

---

## Next Steps

- [Query Task](../task/query_task.md) - Look up task definitions
- [Query Task Group](../taskgroup/query_taskgroup.md) - Look up task group definitions
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI