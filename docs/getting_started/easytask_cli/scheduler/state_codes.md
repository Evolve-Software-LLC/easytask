# State Codes

The `scheduler state-codes` command lists all task state codes and their meanings used by EasyTask.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler state-codes -h
```

```
 Usage: easytask scheduler state-codes [OPTIONS]

 List task state codes.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler state-codes
```

```
┏━━━━━━┳━━━━━━━━━━━━━━━━━━━━┓
┃ Code ┃ State              ┃
┡━━━━━━╇━━━━━━━━━━━━━━━━━━━━┩
│ 0    │ PENDING            │
│ 1    │ TRIGGER            │
│ 2    │ STARTED            │
│ 3    │ SUCCESS            │
│ 4    │ FAILED             │
│ 5    │ FROZEN             │
│ 6    │ TERMINATED         │
│ 7    │ SKIPPED            │
└──────┴────────────────────┘
```

---

## ⏭️ Next Steps
- [Task Runs](task_runs.md)
- [Task Statuses](task_statuses.md)
- [CLI Overview](../intro_cli.md)
