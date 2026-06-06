# Task Stats

The `agents task-stats` command retrieves Celery task statistics for a specific agent, showing active, reserved, scheduled, and registered task counts.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `AGENT_NAME` | Agent name (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask agents task-stats -h
```

```
 Usage: easytask agents task-stats [OPTIONS] AGENT_NAME

 Get Celery task stats for an agent.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  agent_name      TEXT  Agent name [required]                              │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents task-stats worker-01
```

```
╭─ Task Stats ───────────────────────────────╮
│ Active      3                               │
│ Reserved    1                               │
│ Scheduled   5                               │
│ Registered  12                              │
╰───────────────────────────────────────────╯

┏━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┓
┃ Task                  ┃ Status  ┃ Started            ┃
┡━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━┩
│ data_processing       │ ACTIVE  │ 2026-05-12 08:00   │
│ report_generation     │ ACTIVE  │ 2026-05-12 08:02   │
│ backup_job            │ ACTIVE  │ 2026-05-12 08:05   │
└───────────────────────┴─────────┴────────────────────┘
```

---

## ⏭️ Next Steps
- [Workers](workers.md)
- [Queues](queues.md)
- [Task Runs](../scheduler/task_runs.md)
- [CLI Overview](../intro_cli.md)
