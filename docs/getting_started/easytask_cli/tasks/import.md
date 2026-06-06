# Import Tasks

The `tasks import` command imports tasks and groups from a JSON file, creating, updating, or deleting records as needed.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `FILE` | JSON file to import (required, positional). |

## 🖥️ Basic Usage

```bash
easytask tasks import -h
```

```
 Usage: easytask tasks import [OPTIONS] FILE

 Import tasks and groups from a JSON file.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  file      PATH  JSON file to import [required]                           │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask tasks import backup.json
```

```
Import complete: 5 created, 2 updated, 1 deleted
```

### **Example — With Errors**

```bash
easytask tasks import backup.json
```

```
Import complete: 3 created, 0 updated, 0 deleted
Errors:
  - Task "invalid_task": missing required field 'cmd'
```

---

## ⏭️ Next Steps
- [Export Tasks](export.md)
- [List Tasks](list.md)
- [CLI Overview](../intro_cli.md)
