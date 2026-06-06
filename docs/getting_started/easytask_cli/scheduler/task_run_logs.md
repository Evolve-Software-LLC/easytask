# Task Run Logs

The `scheduler task-run-logs` command retrieves stdout and stderr logs for a specific task run.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `RUN_ID` | Task run ID (required, positional). |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Lines per page (default: 500). |
| `--output, -o` | Output format: table, json, yaml (default: table). |
| `--stream` | Show only stdout or stderr. |

## 🖥️ Basic Usage

```bash
easytask scheduler task-run-logs -h
```

```
 Usage: easytask scheduler task-run-logs [OPTIONS] RUN_ID

 Get logs for a task run.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  run_id    INTEGER  Task run ID [required]                                │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --page       -p        Page number (default: 1)                             │
│ --per-page             Lines per page (default: 500)                        │
│ --output     -o        [table\|json\|yaml]  Output format (default: table)  │
│ --stream               Show only stdout or stderr                           │
│ --help       -h        Show this message and exit.                          │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler task-run-logs 150
```

```
╭─ stdout ──────────────────────────────────╮
│ Starting data processing...                │
│ Loaded 10,000 records                      │
│ Processing batch 1/10...                   │
│ Processing batch 2/10...                   │
│ ...                                        │
│ Completed: 10,000 records processed        │
╰───────────────────────────────────────────╯

╭─ stderr ──────────────────────────────────╮
│ WARNING: 3 records skipped (invalid format)│
╰───────────────────────────────────────────╯
```

### **Example — Filter by Stream**

```bash
easytask scheduler task-run-logs 150 --stream stderr
```

```
╭─ stderr ──────────────────────────────────╮
│ WARNING: 3 records skipped (invalid format)│
╰───────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Task Runs](task_runs.md)
- [State Codes](state_codes.md)
- [CLI Overview](../intro_cli.md)
