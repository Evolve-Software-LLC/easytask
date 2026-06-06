# Enable Task

The `events enable` command enables a task on the scheduler, allowing it to be triggered according to its schedule.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--task-name` | Task name (default: ""). |

## 🖥️ Basic Usage

```bash
easytask events enable -h
```

```
 Usage: easytask events enable [OPTIONS] TASK_ID

 Enable a task on the scheduler.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --task-name          TEXT  Task name (default: )                            │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events enable 42
```

```
Task 42 enabled on scheduler.
```

---

## ⏭️ Next Steps
- [Disable Task](disable.md)
- [Force Run](force_run.md)
- [Upcoming Tasks](../scheduler/upcoming.md)
- [CLI Overview](../intro_cli.md)
