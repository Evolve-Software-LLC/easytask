# Delete Group

The `groups delete` command deletes a group by its ID. Use the `--cascade` flag to also remove dependencies.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `GROUP_ID` | Group ID (required, positional). |
| `--cascade` | Cascade delete dependencies. |

## 🖥️ Basic Usage

```bash
easytask groups delete -h
```

```
 Usage: easytask groups delete [OPTIONS] GROUP_ID

 Delete a group.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  group_id      INTEGER  Group ID [required]                               │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --cascade          Cascade delete dependencies                              │
│ --help     -h      Show this message and exit.                              │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask groups delete 10
```

```
Group deleted: daily_jobs (ID: 10)
```

### **Example — Cascade Delete**

```bash
easytask groups delete 10 --cascade
```

```
Group deleted: daily_jobs (ID: 10)
Dependencies cascade deleted.
```

---

## ⏭️ Next Steps
- [List Groups](list.md)
- [Create Group](create.md)
- [CLI Overview](../intro_cli.md)
