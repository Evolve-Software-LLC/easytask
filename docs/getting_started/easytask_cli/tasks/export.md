# Export Tasks

The `tasks export` command exports all tasks and groups as JSON. Output can be written to a file or printed to stdout.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output file path (default: stdout). |

## 🖥️ Basic Usage

```bash
easytask tasks export -h
```

```
 Usage: easytask tasks export [OPTIONS]

 Export all tasks and groups as JSON.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      PATH  Output file path (default: stdout)                │
│ --help     -h            Show this message and exit.                        │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example — Export to File**

```bash
easytask tasks export -o backup.json
```

```
Exported to backup.json
```

### **Example — Export to Stdout**

```bash
easytask tasks export
```

```json
{
  "tasks": [
    {
      "id": 42,
      "name": "data_processing",
      "cmd": "/usr/bin/python3 /scripts/process.py",
      ...
    }
  ],
  "groups": [
    {
      "id": 1,
      "name": "daily",
      ...
    }
  ]
}
```

---

## ⏭️ Next Steps
- [Import Tasks](import.md)
- [List Tasks](list.md)
- [CLI Overview](../intro_cli.md)
