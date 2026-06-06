# Terminate Task

The `events terminate` command terminates a currently running task.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--run-date, -d` | Run date as YYYYMMDD (default: today). |

## 🖥️ Basic Usage

```bash
easytask events terminate -h
```

```
 Usage: easytask events terminate [OPTIONS] TASK_ID

 Terminate a running task.

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
easytask events terminate 42
```

```
Task 42 terminated.
```

---

## ⏭️ Next Steps
- [Task Runs](../scheduler/task_runs.md)
- [Force Run](force_run.md)
- [CLI Overview](../intro_cli.md)
