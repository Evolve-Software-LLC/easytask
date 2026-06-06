---
title: Query Task - EasyTask CLI - EasyTask Documentation
description: Query task definitions from the EasyTask database using various filtering options like task ID, name, owner, and more.
keywords:
  - query task
  - easytask cli
  - search task
  - task lookup
---

# Query Task 

The `query` command in the EasyTask CLI allows users to retrieve task details from the database based on various filtering options such as Task ID, name, owner, and more.

## Parameters

| Parameter               | Description                                       |
|-------------------------|---------------------------------------------------|
| `--tid`                 | Task ID (integer).                                                   |
| `--name`                | Task name (string).                               |
| `--task_owner`          | Owner of the task (string).                       |
| `--cmd`                 | Command to execute for the task (string).         |
| `--run_on_host`         | Host on which the command will run (string).      |
| `--run_as_user`         | User to run the command as (string).              |
| `--max_run_time`        | Maximum run time in seconds (integer).            |
| `--description`         | Description of the task (string).                 |
| `--retry_attempts`      | Number of retry attempts allowed (integer).       |
| `--stderr`              | Path for standard error output file (string).     |
| `--stdout`              | Path for standard output file (string).           |
| `--timezone`            | Timezone for the task (string).                   |
| `--active`              | Whether the task is active (boolean).             |
| `--calendar`            | Calendar used for scheduling the task (string).   |
| `--instance`            | Instance of the task (string).                    |
| `--day_of_week`         | Days of the week the task runs (string).          |
| `--ordinal_day`         | Ordinal days for task scheduling (string).        |
| `--run_frequency`       | Run frequency of the task (string).               |
| `--trigger_times`       | Specific trigger times for the task (string).     |

<br>
<br>

<!-- !!! Schema inline start "Task Schema"
    ```json
    {
      "name": "sample_task", # Task name
      "task_owner": "admin", # Owner
      "cmd": "ls -l",        # Command
      "run_on_host": "test_host",
      "run_as_user": "testuser",
      "max_run_time": 60,    # Max seconds
      "description": "A Stray task : Run an ls command",
      "retry_attempts": 3,   # Retries
      "stderr": "sampletask.err",
      "stdout": "sampletask.out",
      "timezone": "US/Eastern",
      "team": "US-EQUITIES2",
      "active": true,
      "calendar": "US_HOLIDAYS",
      "instance": "default",
      "day_of_week": "1111111", # Mon-Sun
      "trigger_times": "12:00"
    }
    ``` -->

## 🖥️ Basic Usage

```bash
easytask.bin database task query -h 
usage: easytask.bin database task query [-h] [--tid TID] [--name NAME] [--task_owner TASK_OWNER] [--cmd CMD] [--run_on_host RUN_ON_HOST] [--run_as_user RUN_AS_USER]
                                        [--max_run_time MAX_RUN_TIME] [--description DESCRIPTION] [--retry_attempts RETRY_ATTEMPTS] [--stderr STDERR] [--stdout STDOUT]
                                        [--timezone TIMEZONE] [--active ACTIVE] [--calendar CALENDAR] [--instance INSTANCE] [--day_of_week DAY_OF_WEEK]
                                        [--ordinal_day ORDINAL_DAY] [--run_frequency RUN_FREQUENCY] [--trigger_times TRIGGER_TIMES]

options:
  -h, --help                   show this help message and exit
  --tid TID                    Task ID
  --name NAME                  Task name
  --task_owner TASK_OWNER      Task owner
  --cmd CMD                    Command to execute
  --run_on_host RUN_ON_HOST    Host to run the command on
  --run_as_user RUN_AS_USER    User to run the command as
  --max_run_time MAX_RUN_TIME  Maximum run time in seconds
  --description DESCRIPTION    Description of the task
  --retry_attempts RETRY_ATTEMPTS Number of retry attempts
  --stderr STDERR              Standard error file
  --stdout STDOUT              Standard output file
  --timezone TIMEZONE          Timezone for the task
  --active ACTIVE              Is the task active
  --calendar CALENDAR          Calendar for the task
  --instance INSTANCE          Instance of the task
  --day_of_week DAY_OF_WEEK    Days of the week the task runs
  --ordinal_day ORDINAL_DAY    Ordinal days
  --run_frequency RUN_FREQUENCY Run frequency of the task
  --trigger_times TRIGGER_TIMES Trigger Times of the task

```

### **Sample Input**
```
easytask.bin database task query
--<parameter_name> <value>
--<parameter_name> "<value with spaces>"
...

```

### **Sample Output**

```sh
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
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin database task query --name testmax

[INFO] Total 1 tasks found: 

[INFO] Tasks: {'_sa_instance_state': <sqlalchemy.orm.state.InstanceState object at 0x7fb8d0352690>, 'task_group_fk_id': None, 'name': 'testmax', 'run_on_host': 'tejas2', 'stdout': '/tmp/task_09452226012026.out', 'timezone': 'UTC', 'instance': 'default', 'tid': 2035, 'task_group': None, 'task_owner': '', 'cmd': 'ls', 'description': 'ls testing', 'stderr': '/tmp/task_09452226012026.err', 'active': True, 'trigger_times': '14:48,14:49', 'day_of_week': '1111111', 'max_run_time': 123456, 'calendar': 'US-Calendar'}

```

---

## Frequently Asked Questions

**Q: Can I query tasks without any filter parameters?**
A: Yes, running `query` without filters returns all tasks in the database.

**Q: How do I search for tasks by partial name?**
A: Use the `--name` parameter with the exact task name; for partial matches, combine with external tools like grep.

---

## Next Steps

- [Insert Task](insert_task.md) - Insert a new task
- [Update Task](update_task.md) - Update an existing task
- [CLI Introduction](../../intro_cli.md) - Get started with the EasyTask CLI
