# Task Runs

The `scheduler task-runs` command lists task runs with lifecycle information, including status breakdowns and execution details.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--status, -s` | Filter by status. |
| `--search` | Search by task name. |
| `--group, -g` | Filter by group name. |
| `--since` | Look back hours (default: 24). |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler task-runs -h
```

```
 Usage: easytask scheduler task-runs [OPTIONS]

 List task runs with lifecycle.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --status     -s        Filter by status                                     │
│ --search               Search by task name                                  │
│ --group      -g        Filter by group name                                 │
│ --since                Look back hours (default: 24)                        │
│ --page       -p        Page number (default: 1)                             │
│ --per-page             Items per page (default: 25)                         │
│ --output     -o        [table\|json\|yaml]  Output format (default: table)  │
│ --help       -h        Show this message and exit.                          │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler task-runs
```

```
╭─ Stats ───────────────────────────────────╮
│ SUCCESS   42                               │
│ FAILED     3                               │
│ RUNNING    2                               │
│ PENDING    5                               │
╰───────────────────────────────────────────╯

┏━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━┓
┃ Task ID ┃ Task Name         ┃ Group   ┃ Status  ┃ Started   ┃ Finished   ┃ Duration ┃ Host        ┃ Ret ┃
┡━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━┩
│ 42      │ data_processing   │ daily   │ SUCCESS │ 08:00:00  │ 08:05:32   │ 5m 32s   │ worker-01   │ 0   │
│ 43      │ report_gen        │ daily   │ FAILED  │ 08:01:00  │ 08:02:15   │ 1m 15s   │ worker-02   │ 1   │
└─────────┴───────────────────┴─────────┴─────────┴───────────┴────────────┴──────────┴─────────────┴─────┘
 Page 1 of 3 (52 total items)
```

### **Example — Filter by Status**

```bash
easytask scheduler task-runs --status FAILED
```

---

## ⏭️ Next Steps
- [Task Run Logs](task_run_logs.md)
- [Task Statuses](task_statuses.md)
- [CLI Overview](../intro_cli.md)
