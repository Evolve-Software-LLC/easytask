# Get Group

The `groups get` command retrieves detailed information about a specific group, displaying all group fields in a formatted panel.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `GROUP_ID` | Group ID (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask groups get -h
```

```
 Usage: easytask groups get [OPTIONS] GROUP_ID

 Get group details.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  group_id      INTEGER  Group ID [required]                               │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask groups get 1
```

```
╭──────────────── Group: daily ─────────────────╮
│ ID              1                              │
│ Name            daily                          │
│ Active          True                           │
│ Timezone        UTC                            │
│ Day of Week     MON,TUE,WED,THU,FRI            │
│ Trigger Times   06:00                          │
│ Description     Daily batch processing jobs    │
│ Dependency      []                             │
│ Tasks           5                              │
╰───────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Update Group](update.md)
- [Delete Group](delete.md)
- [Refresh Group](../events/refresh_group.md)
- [CLI Overview](../intro_cli.md)
