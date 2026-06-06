# Delete Task

The `tasks delete` command deletes a task by its ID. Use the `--cascade` flag to also remove dependencies.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--cascade` | Cascade delete dependencies. |

## 🖥️ Basic Usage

```bash
easytask tasks delete -h
```

```
 Usage: easytask tasks delete [OPTIONS] TASK_ID

 Delete a task.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --cascade          Cascade delete dependencies                              │
│ --help     -h      Show this message and exit.                              │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask tasks delete 42
```

```
Task deleted: data_processing (ID: 42)
```

### **Example — Cascade Delete**

```bash
easytask tasks delete 42 --cascade
```

```
Task deleted: data_processing (ID: 42)
Dependencies cascade deleted.
```

---

## ⏭️ Next Steps
- [List Tasks](list.md)
- [Create Task](create.md)
- [CLI Overview](../intro_cli.md)
