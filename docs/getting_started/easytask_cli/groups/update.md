# Update Group

The `groups update` command updates an existing group from **inline parameters** or a **JSON file**. Uses `GROUP_ID` if given, otherwise resolves by `--name`.

## Modes

| Mode | When to Use |
|------|-------------|
| **Inline** | Quick field updates — pass only the fields to change as CLI flags. |
| **File** (`--file`) | Bulk or complex updates — provide a JSON file with fields to change. |

Both modes are mutually exclusive. If `--file` is provided, all inline parameters are ignored.

## Parameters

### Identification

| Parameter | Description |
|-----------|-------------|
| `GROUP_ID` | Group ID (optional positional). Omit to use `--name` resolution. |
| `--name, -n` | Group name — used to look up the group ID when `GROUP_ID` is omitted. Can also update the name itself. |

### File Mode

| Parameter | Description |
|-----------|-------------|
| `--file, -f` | JSON file with group updates. |

### Inline Parameters (all optional — only provided fields are updated)

| Parameter | Description |
|-----------|-------------|
| `--description, -d` | Group description. |
| `--active / --inactive` | Active status. |
| `--timezone, -z` | Timezone in IANA format. |
| `--trigger-times` | Comma-separated times in `HH:MM` format. Automatically deduplicated and sorted. |
| `--day-of-week` | 7-character binary string for MTWTFSS (e.g. `1111100` = Mon–Fri). |
| `--ordinal-day` | Ordinal day description. |
| `--run-frequency` | Run frequency in `HH:MM-HH:MM-freq` format. |
| `--calendar` | Calendar name (must exist in the backend). |
| `--dependency` | Dependency string (e.g. `S:groupname`). |
| `--profile` | Profile name. |

!!! warning "Mutual Exclusivity"

    - Only one of `--trigger-times` or `--run-frequency` may be provided (not both).
    - Only one of `--day-of-week` or `--ordinal-day` may be provided (not both).

## 🖥️ Basic Usage

```bash
easytask groups update -h
```

```
 Usage: easytask groups update [OPTIONS] [GROUP_ID]

 Update a group from inline parameters or a JSON file. Uses GROUP_ID if
 given, otherwise looks up by name.

╭─ Arguments ─────────────────────────────────────────────────────────────────────╮
│   group_id      INTEGER  Group ID (optional if using --name or --file)          │
╰─────────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────────╮
│ --file            -f      PATH     JSON file with group updates                  │
│ --name            -n      TEXT     Group name (also resolves ID if GROUP_ID     │
│                                            is omitted)                           │
│ --description     -d      TEXT     Group description                             │
│ --active / --inactive               Active status                              │
│ --timezone        -z      TEXT     Timezone                                    │
│ --trigger-times            TEXT     Comma-separated HH:MM                       │
│ --day-of-week              TEXT     7-char binary MTWTFSS                       │
│ --ordinal-day              TEXT     Ordinal day                                │
│ --run-frequency            TEXT     HH:MM-HH:MM-freq                           │
│ --calendar                 TEXT     Calendar name                              │
│ --dependency               TEXT     Dependency string                           │
│ --profile                  TEXT     Profile name                               │
│ --help             -h               Show this message and exit.                 │
╰─────────────────────────────────────────────────────────────────────────────────╯
```

---

## Inline Mode Examples

### **Update group description by ID**

```bash
easytask groups update 10 --description "Updated: Daily batch processing jobs v2"
```

```
Group 10 updated.
```

### **Update group trigger times (automatically sorted)**

```bash
easytask groups update 11 --trigger-times "12:00,03:00,07:00,18:00"
```

```
Group 11 updated.
```

### **Update group by name resolution**

When you don't know the group ID, use `--name` to look it up:

```bash
easytask groups update --name "daily_jobs" --active
```

```
Resolved name 'daily_jobs' → ID 10
Group 10 updated.
```

### **Update group timezone**

```bash
easytask groups update 12 --timezone "Asia/Tokyo"
```

```
Group 12 updated.
```

### **Deactivate a group**

```bash
easytask groups update 14 --inactive
```

```
Group 14 updated.
```

---

## File Mode Examples

### **Sample Input**

```json title="group_update.json"
{
  "trigger_times": "07:00",
  "description": "Updated daily batch processing jobs"
}
```

### **Example**

```bash
easytask groups update 10 -f group_update.json
```

```
Group 10 updated.
```

---

## ⏭️ Next Steps
- [Get Group](get.md)
- [Delete Group](delete.md)
- [Refresh Group](../events/refresh_group.md)
- [CLI Overview](../intro_cli.md)
