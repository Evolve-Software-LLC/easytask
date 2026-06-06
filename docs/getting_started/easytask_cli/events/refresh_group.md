# Refresh Group

The `events refresh-group` command reloads a group's definition on the scheduler, picking up any changes made to the group configuration.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `GROUP_ID` | Group ID (required, positional). |
| `--group-name` | Group name (default: ""). |

## 🖥️ Basic Usage

```bash
easytask events refresh-group -h
```

```
 Usage: easytask events refresh-group [OPTIONS] GROUP_ID

 Reload group definition on scheduler.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  group_id      INTEGER  Group ID [required]                               │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --group-name          TEXT  Group name (default: )                          │
│ --help         -h            Show this message and exit.                    │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events refresh-group 10
```

```
Group definition refreshed for group 10 (daily).
```

---

## ⏭️ Next Steps
- [Refresh Task](refresh_task.md)
- [Refresh Graph](refresh_graph.md)
- [Get Group](../groups/get.md)
- [CLI Overview](../intro_cli.md)
