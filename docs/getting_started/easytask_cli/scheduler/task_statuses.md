# Task Statuses

The `scheduler task-statuses` command shows the latest status for each task known to the scheduler.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler task-statuses -h
```

```
 Usage: easytask scheduler task-statuses [OPTIONS]

 Show latest status per task.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler task-statuses
```

```
┏━━━━━━━━━┳━━━━━━━━━━━━┓
┃ Task ID ┃ Status     ┃
┡━━━━━━━━━╇━━━━━━━━━━━━┩
│ 42      │ SUCCESS    │
│ 43      │ FAILED     │
│ 44      │ PENDING    │
│ 45      │ FROZEN     │
│ 46      │ ACTIVE     │
└─────────┴────────────┘
```

---

## ⏭️ Next Steps
- [Task Runs](task_runs.md)
- [State Codes](state_codes.md)
- [Modify Status](../events/modify_status.md)
- [CLI Overview](../intro_cli.md)
