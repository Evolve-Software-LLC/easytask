# Update Task

The `tasks update` command updates an existing task from **inline parameters** or a **JSON file**. Uses `TASK_ID` if given, otherwise resolves by `--name`.

## Modes

| Mode | When to Use |
|------|-------------|
| **Inline** | Quick field updates — pass only the fields to change as CLI flags. |
| **File** (`--file`) | Bulk or complex updates — provide a JSON file with fields to change. |

Both modes are mutually exclusive. If `--file` is provided, all inline parameters are ignored.

## Parameters

### Identification

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (optional positional). Omit to use `--name` resolution. |
| `--name, -n` | Task name — used to look up the task ID when `TASK_ID` is omitted. Can also update the name itself. |

### File Mode

| Parameter | Description |
|-----------|-------------|
| `--file, -f` | JSON file with task updates. |

### Inline Parameters (all optional — only provided fields are updated)

| Parameter | Description |
|-----------|-------------|
| `--cmd, -c` | Command to run. |
| `--host` | Agent hostname. |
| `--description, -d` | Task description. |
| `--run-as-user` | System user to run the command as. |
| `--active / --inactive` | Active status. |
| `--group-id, -g` | Group ID. |
| `--timezone, -z` | Timezone in IANA format. |
| `--trigger-times` | Comma-separated times in `HH:MM` format. Automatically deduplicated and sorted. |
| `--day-of-week` | 7-character binary string for MTWTFSS (e.g. `1111100` = Mon–Fri). |
| `--ordinal-day` | Ordinal day description. |
| `--run-frequency` | Run frequency in `HH:MM-HH:MM-freq` format. |
| `--calendar` | Calendar name (must exist in the backend). |
| `--dependency` | Dependency string (e.g. `S:taskname`). |
| `--max-run-time` | Maximum run time in seconds (1–172800). |
| `--retry-attempts` | Number of retry attempts on failure. |
| `--stdout` | File path for stdout capture. |
| `--stderr` | File path for stderr capture. |
| `--profile` | Profile name. |
| `--task-owner` | Task owner. |

!!! warning "Mutual Exclusivity"

    - Only one of `--trigger-times` or `--run-frequency` may be provided (not both).
    - Only one of `--day-of-week` or `--ordinal-day` may be provided (not both).

## 🖥️ Basic Usage

```bash
easytask tasks update -h
```

```
 Usage: easytask tasks update [OPTIONS] [TASK_ID]

 Update a task from inline parameters or a JSON file. Uses TASK_ID if given,
 otherwise looks up by name.

╭─ Arguments ─────────────────────────────────────────────────────────────────────╮
│   task_id      INTEGER  Task ID (optional if using --name or --file)            │
╰─────────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────────╮
│ --file            -f      PATH     JSON file with task updates                  │
│ --name            -n      TEXT     Task name (also resolves ID if TASK_ID       │
│                                            is omitted)                          │
│ --cmd             -c      TEXT     Command to run                               │
│ --host                    TEXT     Agent hostname                               │
│ --description     -d      TEXT     Task description                             │
│ --run-as-user              TEXT     Run as user                                 │
│ --active / --inactive               Active status                              │
│ --group-id        -g      INT      Group ID                                    │
│ --timezone        -z      TEXT     Timezone                                    │
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

### **Update task command by ID**

```bash
easytask tasks update 42 --cmd "/usr/bin/python3 /scripts/process_v2.py"
```

```
Task 42 updated.
```

### **Update task by name resolution**

When you don't know the task ID, use `--name` to look it up:

```bash
easytask tasks update --name "data_processing" --description "Updated description" --active
```

```
Resolved task_name 'data_processing' → ID 42
Task 42 updated.
```

### **Update trigger times (automatically sorted)**

```bash
easytask tasks update 44 --trigger-times "23:00,01:00,11:00,17:00"
```

```
Task 44 updated.
```

### **Deactivate a task**

```bash
easytask tasks update 42 --inactive
```

```
Task 42 updated.
```

### **Update max run time and retry**

```bash
easytask tasks update 42 --max-run-time 7200 --retry-attempts 5
```

```
Task 42 updated.
```

---

## File Mode Examples

### **Sample Input**

```json title="task_update.json"
{
  "cmd": "/usr/bin/python3 /scripts/process_v2.py",
  "max_run_time": 7200,
  "active": true
}
```

### **Example**

```bash
easytask tasks update 42 -f task_update.json
```

```
Task 42 updated.
```

---

## ⏭️ Next Steps
- [Get Task](get.md)
- [Delete Task](delete.md)
- [Refresh Task](../events/refresh_task.md)
- [CLI Overview](../intro_cli.md)
