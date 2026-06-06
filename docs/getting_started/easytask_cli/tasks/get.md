# Get Task

The `tasks get` command retrieves detailed information about a specific task, displaying all task fields in a formatted panel.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask tasks get -h
```

```
 Usage: easytask tasks get [OPTIONS] TASK_ID

 Get task details.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask tasks get 42
```

```
╭──────────────── Task: data_processing ────────────────╮
│ ID              42                                    │
│ Name            data_processing                       │
│ Active          True                                  │
│ Owner           admin                                 │
│ Command         /usr/bin/python3 /scripts/process.py  │
│ Host            worker-01                             │
│ Group           daily (ID: 1)                         │
│ Timezone        UTC                                   │
│ Day of Week     MON,TUE,WED,THU,FRI                   │
│ Trigger Times   08:00                                 │
│ Run As User     easytask                              │
│ Max Run Time    3600                                  │
│ Retry Attempts  3                                     │
│ Calendar        WORKDAY                               │
│ Description     Daily data processing task            │
│ Stdout          /var/log/easytask/data_processing.out │
│ Stderr          /var/log/easytask/data_processing.err │
╰──────────────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Update Task](update.md)
- [Delete Task](delete.md)
- [Force Run](../events/force_run.md)
- [CLI Overview](../intro_cli.md)
