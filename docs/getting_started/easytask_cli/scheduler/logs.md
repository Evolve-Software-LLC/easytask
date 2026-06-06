# Scheduler Logs

The `scheduler logs` command lists scheduler run logs with filtering by action type and search.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--action, -a` | Filter by action (STARTED, STOPPED, RESTARTED, CRASHED). |
| `--search, -s` | Search. |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler logs -h
```

```
 Usage: easytask scheduler logs [OPTIONS]

 List scheduler run logs.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --action     -a        Filter by action (STARTED, STOPPED, RESTARTED,       │
│                         CRASHED)                                            │
│ --search     -s        Search                                               │
│ --page       -p        Page number (default: 1)                             │
│ --per-page             Items per page (default: 25)                         │
│ --output     -o        [table\|json\|yaml]  Output format (default: table)  │
│ --help       -h        Show this message and exit.                          │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler logs
```

```
┏━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┓
┃ ID ┃ Action    ┃ Host        ┃ PID   ┃ Message                   ┃ Time               ┃
┡━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━┩
│ 1  │ STARTED   │ scheduler-1 │ 12345 │ Scheduler started         │ 2026-05-12 06:00:00│
│ 2  │ STARTED   │ scheduler-1 │ 12345 │ Workers initialized: 4    │ 2026-05-12 06:00:01│
│ 3  │ STOPPED   │ scheduler-1 │ 12345 │ Scheduler stopped         │ 2026-05-12 05:59:59│
└────┴───────────┴─────────────┴───────┴───────────────────────────┴────────────────────┘
 Page 1 of 1 (3 total items)
```

### **Example — Filter by Action**

```bash
easytask scheduler logs --action CRASHED
```

---

## ⏭️ Next Steps
- [Task Run Logs](task_run_logs.md)
- [Task Runs](task_runs.md)
- [CLI Overview](../intro_cli.md)
