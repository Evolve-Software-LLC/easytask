# Disable Task

The `events disable` command disables a task on the scheduler, preventing it from being triggered.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--task-name` | Task name (default: ""). |

## 🖥️ Basic Usage

```bash
easytask events disable -h
```

```
 Usage: easytask events disable [OPTIONS] TASK_ID

 Disable a task on the scheduler.

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
easytask events disable 42
```

```
Task 42 disabled on scheduler.
```

---

## ⏭️ Next Steps
- [Enable Task](enable.md)
- [List Events](list.md)
- [CLI Overview](../intro_cli.md)
