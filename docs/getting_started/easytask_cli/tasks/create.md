# Create Task

The `tasks create` command creates a new task from **inline parameters** or a **JSON definition file**.

## Modes

| Mode | When to Use |
|------|-------------|
| **Inline** | Quick one-off tasks — pass all fields as CLI flags. |
| **File** (`--file`) | Complex or repeatable definitions — provide a JSON file. |

Both modes are mutually exclusive. If `--file` is provided, all inline parameters are ignored.

## Parameters

### File Mode

| Parameter | Description |
|-----------|-------------|
| `--file, -f` | JSON file with task definition. |

### Inline Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `--name, -n` | Yes | Task name. |
| `--cmd, -c` | Yes | Command to run. |
| `--host` | Yes | Agent hostname (e.g. `localhost`). |
| `--description, -d` | No | Task description. |
| `--active / --inactive` | No | Active status (default: `--active`). |
| `--group-id, -g` | No | Group ID to assign the task to. |
| `--timezone, -z` | No | Timezone in IANA format (e.g. `UTC`, `America/New_York`). |
| `--trigger-times` | No | Comma-separated times in `HH:MM` format (e.g. `09:00,14:30`). Automatically deduplicated and sorted. |
| `--day-of-week` | No | 7-character binary string for MTWTFSS (e.g. `1111100` = Mon–Fri). |
| `--ordinal-day` | No | Ordinal day description (e.g. `first monday of every month`). |
| `--run-frequency` | No | Run frequency in `HH:MM-HH:MM-freq` format (e.g. `00:00-23:59-60`). |
| `--calendar` | No | Calendar name (must exist in the backend). |
| `--dependency` | No | Dependency string (e.g. `S:taskname`). |
| `--max-run-time` | No | Maximum run time in seconds (1–172800). |
| `--retry-attempts` | No | Number of retry attempts on failure. |
| `--stdout` | No | File path for stdout capture. |
| `--stderr` | No | File path for stderr capture. |
| `--profile` | No | Profile name. |
| `--task-owner` | No | Task owner. |
| `--run-as-user` | No | System user to run the command as. |

!!! warning "Mutual Exclusivity"

    - Only one of `--trigger-times` or `--run-frequency` may be provided (not both).
    - Only one of `--day-of-week` or `--ordinal-day` may be provided (not both).

## 🖥️ Basic Usage

```bash
easytask tasks create -h
```

```
 Usage: easytask tasks create [OPTIONS]

 Create a task from inline parameters or a JSON file.

╭─ Options ───────────────────────────────────────────────────────────────────────╮
│ --file            -f      PATH     JSON file with task definition               │
│ --name            -n      TEXT     Task name (required if no --file)             │
│ --cmd             -c      TEXT     Command to run (required if no --file)        │
│ --host                    TEXT     Agent hostname (required if no --file)        │
│ --description     -d      TEXT     Task description                             │
│ --run-as-user              TEXT     Run as user                                 │
│ --active / --inactive               Active status (default: active)             │
│ --group-id        -g      INT      Group ID                                    │
│ --timezone        -z      TEXT     Timezone, e.g. UTC                          │
│ --trigger-times            TEXT     Comma-separated HH:MM                       │
│ --day-of-week              TEXT     7-char binary MTWTFSS                       │
│ --ordinal-day              TEXT     Ordinal day                                │
│ --run-frequency            TEXT     HH:MM-HH:MM-freq                           │
│ --calendar                 TEXT     Calendar name                              │
│ --dependency               TEXT     Dependency string                           │
│ --max-run-time             INT      Max run time in seconds                    │
│ --retry-attempts           INT      Retry attempts                             │
│ --stdout                   TEXT     Stdout file path                           │
│ --stderr                   TEXT     Stderr file path                           │
│ --profile                  TEXT     Profile name                               │
│ --task-owner               TEXT     Task owner                                 │
│ --help             -h               Show this message and exit.                 │
╰─────────────────────────────────────────────────────────────────────────────────╯
```

---

## Inline Mode Examples

### **Create a basic task**

```bash
easytask tasks create --name "data_processing" --cmd "/usr/bin/python3 /scripts/process.py" --host "worker-01"
```

```
Task created with ID: 42
```

### **Create a task with schedule**

```bash
easytask tasks create \
  --name "daily_report" \
  --cmd "/opt/reports/daily.sh" \
  --host "localhost" \
  --description "Daily report generation" \
  --trigger-times "09:00" \
  --day-of-week "1111100" \
  --timezone "UTC" \
  --max-run-time 3600 \
  --retry-attempts 3
```

```
Task created with ID: 43
```

### **Create a task with multiple trigger times**

Trigger times are automatically deduplicated and sorted:

```bash
easytask tasks create \
  --name "multi_check" \
  --cmd "python check.py" \
  --host "localhost" \
  --trigger-times "22:00,06:00,14:00" \
  --day-of-week "1111111" \
  --timezone "UTC"
```

```
Task created with ID: 44
```

### **Create a task with run frequency**

```bash
easytask tasks create \
  --name "frequent_pulse" \
  --cmd "watch -n 1 echo pulse" \
  --host "localhost" \
  --run-frequency "00:00-23:59-120" \
  --day-of-week "1000001" \
  --timezone "Europe/London"
```

```
Task created with ID: 45
```

### **Create a task in a group with dependency**

```bash
easytask tasks create \
  --name "report_notify" \
  --cmd "python notify.py" \
  --host "localhost" \
  --group-id 1 \
  --dependency "S:daily_report" \
  --run-as-user "appuser"
```

```
Task created with ID: 46
```

### **Create an inactive task**

```bash
easytask tasks create \
  --name "maintenance_job" \
  --cmd "echo disabled" \
  --host "localhost" \
  --inactive
```

```
Task created with ID: 47
```

---

## File Mode Examples

!!! Schema "Task Schema"

    ```json
    {
      "name": "data_processing",
      "task_owner": "admin",
      "cmd": "/usr/bin/python3 /scripts/process.py",
      "run_on_host": "worker-01",
      "description": "Daily data processing task",
      "stderr": "/var/log/easytask/data_processing.err",
      "stdout": "/var/log/easytask/data_processing.out",
      "timezone": "UTC",
      "active": true,
      "instance": "default",
      "day_of_week": "1111100",
      "trigger_times": "08:00",
      "run_as_user": "easytask",
      "max_run_time": 3600,
      "retry_attempts": 3,
      "calendar": "WORKDAY"
    }
    ```

### **Sample Input**

```json title="task_def.json"
{
  "name": "data_processing",
  "task_owner": "admin",
  "cmd": "/usr/bin/python3 /scripts/process.py",
  "run_on_host": "worker-01",
  "description": "Daily data processing task",
  "timezone": "UTC",
  "active": true,
  "day_of_week": "1111100",
  "trigger_times": "08:00"
}
```

### **Example**

```bash
easytask tasks create -f task_def.json
```

```
Task created with ID: 42
```

---

## ⏭️ Next Steps
- [List Tasks](list.md)
- [Update Task](update.md)
- [Enable Task](../events/enable.md)
- [Force Run](../events/force_run.md)
- [CLI Overview](../intro_cli.md)
