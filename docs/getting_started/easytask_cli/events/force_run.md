# Force Run

The `events force-run` command forces immediate execution of a task on the scheduler.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--task-name` | Task name (default: ""). |
| `--run-date, -d` | Run date as YYYYMMDD (default: today). |

## 🖥️ Basic Usage

```bash
easytask events force-run -h
```

```
 Usage: easytask events force-run [OPTIONS] TASK_ID

 Force execute a task.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --task-name          TEXT  Task name (default: )                            │
│ --run-date   -d      INT   Run date as YYYYMMDD                            │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events force-run 42
```

```
Force run triggered for task 42 (data_processing)
Run date: 20260512
```

### **Example — With Specific Date**

```bash
easytask events force-run 42 --run-date 20260513
```

```
Force run triggered for task 42 (data_processing)
Run date: 20260513
```

---

## ⏭️ Next Steps
- [Task Runs](../scheduler/task_runs.md)
- [Enable Task](enable.md)
- [Disable Task](disable.md)
- [CLI Overview](../intro_cli.md)
