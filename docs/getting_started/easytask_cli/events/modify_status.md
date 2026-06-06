# Modify Status

The `events modify-status` command modifies the status of a task run.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `TASK_ID` | Task ID (required, positional). |
| `--status` | New status (required). |
| `--run-date, -d` | Run date as YYYYMMDD (default: today). |

## 🖥️ Basic Usage

```bash
easytask events modify-status -h
```

```
 Usage: easytask events modify-status [OPTIONS] TASK_ID

 Modify a task's status.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  task_id      INTEGER  Task ID [required]                                 │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --status            TEXT  New status [required]                             │
│ --run-date   -d     INT   Run date as YYYYMMDD                             │
│ --help       -h           Show this message and exit.                       │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events modify-status 42 --status SUCCESS
```

```
Task 42 status modified to SUCCESS.
```

### **Example — With Date**

```bash
easytask events modify-status 42 --status FAILED --run-date 20260512
```

```
Task 42 status modified to FAILED for date 20260512.
```

---

## ⏭️ Next Steps
- [Task Statuses](../scheduler/task_statuses.md)
- [List Events](list.md)
- [CLI Overview](../intro_cli.md)
