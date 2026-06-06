# Create Group

The `groups create` command creates a new group from **inline parameters** or a **JSON definition file**.

## Modes

| Mode | When to Use |
|------|-------------|
| **Inline** | Quick group creation — pass all fields as CLI flags. |
| **File** (`--file`) | Complex or repeatable definitions — provide a JSON file. |

Both modes are mutually exclusive. If `--file` is provided, all inline parameters are ignored.

## Parameters

### File Mode

| Parameter | Description |
|-----------|-------------|
| `--file, -f` | JSON file with group definition. |

### Inline Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `--name, -n` | Yes | Group name. |
| `--description, -d` | No | Group description. |
| `--active / --inactive` | No | Active status (default: `--active`). |
| `--timezone, -z` | No | Timezone in IANA format (e.g. `UTC`, `America/New_York`). |
| `--trigger-times` | No | Comma-separated times in `HH:MM` format (e.g. `09:00,14:30`). Automatically deduplicated and sorted. |
| `--day-of-week` | No | 7-character binary string for MTWTFSS (e.g. `1111100` = Mon–Fri). |
| `--ordinal-day` | No | Ordinal day description (e.g. `first monday of every month`). |
| `--run-frequency` | No | Run frequency in `HH:MM-HH:MM-freq` format (e.g. `00:00-23:59-60`). |
| `--calendar` | No | Calendar name (must exist in the backend). |
| `--dependency` | No | Dependency string (e.g. `S:groupname`). |
| `--profile` | No | Profile name. |

!!! warning "Mutual Exclusivity"

    - Only one of `--trigger-times` or `--run-frequency` may be provided (not both).
    - Only one of `--day-of-week` or `--ordinal-day` may be provided (not both).

## 🖥️ Basic Usage

```bash
easytask groups create -h
```

```
 Usage: easytask groups create [OPTIONS]

 Create a group from inline parameters or a JSON file.

╭─ Options ───────────────────────────────────────────────────────────────────────╮
│ --file            -f      PATH     JSON file with group definition               │
│ --name            -n      TEXT     Group name (required if no --file)             │
│ --description     -d      TEXT     Group description                             │
│ --active / --inactive               Active status (default: active)              │
│ --timezone        -z      TEXT     Timezone, e.g. UTC                           │
│ --trigger-times            TEXT     Comma-separated HH:MM                        │
│ --day-of-week              TEXT     7-char binary MTWTFSS                        │
│ --ordinal-day              TEXT     Ordinal day                                 │
│ --run-frequency            TEXT     HH:MM-HH:MM-freq                            │
│ --calendar                 TEXT     Calendar name                               │
│ --dependency               TEXT     Dependency string                            │
│ --profile                  TEXT     Profile name                                │
│ --help             -h               Show this message and exit.                  │
╰─────────────────────────────────────────────────────────────────────────────────╯
```

---

## Inline Mode Examples

### **Create a basic group**

```bash
easytask groups create \
  --name "daily_jobs" \
  --description "Daily batch processing jobs" \
  --trigger-times "09:00" \
  --day-of-week "1111100" \
  --timezone "UTC"
```

```
Group created with ID: 10
```

### **Create a group with multiple trigger times**

Trigger times are automatically deduplicated and sorted:

```bash
easytask groups create \
  --name "etl_pipelines" \
  --description "ETL pipelines" \
  --trigger-times "18:00,07:00,12:00" \
  --day-of-week "1111100" \
  --timezone "America/New_York"
```

```
Group created with ID: 11
```

### **Create a group with run frequency**

```bash
easytask groups create \
  --name "high_freq_checks" \
  --description "High-frequency health checks" \
  --run-frequency "08:00-20:00-30" \
  --day-of-week "1111111" \
  --timezone "Asia/Kolkata"
```

```
Group created with ID: 12
```

### **Create a group with dependency**

```bash
easytask groups create \
  --name "dependent_jobs" \
  --description "Runs after daily_jobs completes" \
  --trigger-times "10:00" \
  --day-of-week "1111100" \
  --timezone "UTC" \
  --dependency "S:daily_jobs"
```

```
Group created with ID: 13
```

### **Create an inactive group**

```bash
easytask groups create \
  --name "maintenance" \
  --description "Disabled maintenance group" \
  --trigger-times "02:00" \
  --day-of-week "0000001" \
  --timezone "UTC" \
  --inactive
```

```
Group created with ID: 14
```

---

## File Mode Examples

!!! Schema "Group Schema"

    ```json
    {
      "name": "daily_jobs",
      "day_of_week": "1111100",
      "description": "Daily batch processing jobs",
      "timezone": "UTC",
      "trigger_times": "06:00",
      "active": true,
      "dependency": ""
    }
    ```

### **Sample Input**

```json title="group_def.json"
{
  "name": "daily_jobs",
  "day_of_week": "1111100",
  "description": "Daily batch processing jobs",
  "timezone": "UTC",
  "trigger_times": "06:00",
  "active": true
}
```

### **Example**

```bash
easytask groups create -f group_def.json
```

```
Group created with ID: 10
```

---

## ⏭️ Next Steps
- [List Groups](list.md)
- [Update Group](update.md)
- [Create Task](../tasks/create.md)
- [CLI Overview](../intro_cli.md)
