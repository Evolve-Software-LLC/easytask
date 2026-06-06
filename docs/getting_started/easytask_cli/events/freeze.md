# Freeze Task

The `events freeze` command freezes a task, preventing it from being triggered for a specific run date.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--run-date, -d` | Run date as YYYYMMDD (default: today). |

## 🖥️ Basic Usage

```bash
easytask events freeze -h
```

```
 Usage: easytask events freeze [OPTIONS] TASK_ID

 Freeze a task.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --run-date   -d      INT   Run date as YYYYMMDD                            │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events freeze 42
```

```
Task 42 frozen for date 20260512.
```

### **Example — Specific Date**

```bash
easytask events freeze 42 --run-date 20260515
```

```
Task 42 frozen for date 20260515.
```

---

## ⏭️ Next Steps
- [Unfreeze Task](unfreeze.md)
- [Disable Task](disable.md)
- [CLI Overview](../intro_cli.md)
