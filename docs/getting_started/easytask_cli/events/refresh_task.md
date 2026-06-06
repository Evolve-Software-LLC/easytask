# Refresh Task

The `events refresh-task` command reloads a task's definition on the scheduler, picking up any changes made to the task configuration.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--task-name` | Task name (default: ""). |

## 🖥️ Basic Usage

```bash
easytask events refresh-task -h
```

```
 Usage: easytask events refresh-task [OPTIONS] TASK_ID

 Reload task definition on scheduler.

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
easytask events refresh-task 42
```

```
Task definition refreshed for task 42 (data_processing).
```

---

## ⏭️ Next Steps
- [Refresh Group](refresh_group.md)
- [Refresh Graph](refresh_graph.md)
- [Get Task](../tasks/get.md)
- [CLI Overview](../intro_cli.md)
