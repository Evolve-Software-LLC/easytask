# List Tasks

The `tasks list` command lists all tasks with filtering by active status, search, and group, along with pagination support.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--active / --inactive` | Filter by active status. |
| `--search, -s` | Search by name. |
| `--group-id, -g` | Filter by group ID. |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask tasks list -h
```

```
 Usage: easytask tasks list [OPTIONS]

 List tasks.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --active / --inactive    Filter by active status                            │
│ --search       -s      TEXT  Search by name                                 │
│ --group-id     -g      INT   Filter by group ID                             │
│ --page         -p            Page number (default: 1)                       │
│ --per-page                   Items per page (default: 25)                   │
│ --output       -o      [table\|json\|yaml]  Output format (default: table)  │
│ --help         -h            Show this message and exit.                    │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask tasks list
```

```
┏━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┓
┃ ID    ┃ Name              ┃ Active ┃ Host        ┃ Group     ┃ Schedule         ┃
┡━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━┩
│ 42    │ data_processing   │ Y      │ worker-01   │ daily     │ MON-FRI 08:00    │
│ 43    │ report_gen        │ Y      │ worker-02   │ daily     │ MON-FRI 09:00    │
│ 44    │ cleanup_job       │ N      │ worker-01   │ maintenance│ SUN 00:00       │
└───────┴───────────────────┴────────┴─────────────┴───────────┴──────────────────┘
 Page 1 of 1 (3 total items)
```

### **Example — Filter Active Tasks**

```bash
easytask tasks list --active
```

### **Example — Search by Name**

```bash
easytask tasks list --search data
```

---

## ⏭️ Next Steps
- [Get Task](get.md)
- [Create Task](create.md)
- [Export Tasks](export.md)
- [CLI Overview](../intro_cli.md)
