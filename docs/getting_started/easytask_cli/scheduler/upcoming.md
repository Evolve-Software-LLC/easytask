# Upcoming Tasks

The `scheduler upcoming` command shows tasks scheduled to run next, including their next run time in UTC and local timezone.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler upcoming -h
```

```
 Usage: easytask scheduler upcoming [OPTIONS]

 Show upcoming scheduled tasks.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler upcoming
```

```
┏━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━┓
┃ Task ID ┃ Task Name         ┃ Next Run (UTC)      ┃ Local Run           ┃ Timezone ┃ Group   ┃ Agent   ┃
┡━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━┩
│ 42      │ data_processing   │ 2026-05-13 08:00:00 │ 2026-05-13 08:00:00 │ UTC      │ daily   │ agent-1 │
│ 55      │ backup_job        │ 2026-05-13 00:00:00 │ 2026-05-13 05:30:00 │ IST      │ nightly │ agent-2 │
└─────────┴───────────────────┴─────────────────────┴─────────────────────┴──────────┴─────────┴─────────┘
```

---

## ⏭️ Next Steps
- [Task Runs](task_runs.md)
- [Force Run](../events/force_run.md)
- [CLI Overview](../intro_cli.md)
