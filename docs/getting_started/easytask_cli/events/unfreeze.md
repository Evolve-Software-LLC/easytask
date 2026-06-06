# Unfreeze Task

The `events unfreeze` command unfreezes a previously frozen task, allowing it to be triggered again.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--run-date, -d` | Run date as YYYYMMDD (default: today). |

## 🖥️ Basic Usage

```bash
easytask events unfreeze -h
```

```
 Usage: easytask events unfreeze [OPTIONS] TASK_ID

 Unfreeze a task.

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
easytask events unfreeze 42
```

```
Task 42 unfrozen for date 20260512.
```

---

## ⏭️ Next Steps
- [Freeze Task](freeze.md)
- [Force Run](force_run.md)
- [CLI Overview](../intro_cli.md)
