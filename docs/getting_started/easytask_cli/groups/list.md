# List Groups

The `groups list` command lists all groups with filtering by active status, search, and pagination support.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--active / --inactive` | Filter by active status. |
| `--search, -s` | Search by name. |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask groups list -h
```

```
 Usage: easytask groups list [OPTIONS]

 List groups.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --active / --inactive    Filter by active status                            │
│ --search       -s      TEXT  Search by name                                 │
│ --page         -p            Page number (default: 1)                       │
│ --per-page                   Items per page (default: 25)                   │
│ --output       -o      [table\|json\|yaml]  Output format (default: table)  │
│ --help         -h            Show this message and exit.                    │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask groups list
```

```
┏━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━┳━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┓
┃ ID    ┃ Name         ┃ Active ┃ Tasks ┃ Schedule         ┃ Dependency ┃
┡━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━╇━━━━━━━╇━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━┩
│ 1     │ daily        │ Y      │ 5     │ MON-FRI 06:00    │            │
│ 2     │ nightly      │ Y      │ 3     │ SUN-FRI 00:00    │            │
│ 3     │ maintenance  │ N      │ 2     │ SUN 02:00        │            │
└───────┴──────────────┴────────┴───────┴──────────────────┴────────────┘
 Page 1 of 1 (3 total items)
```

---

## ⏭️ Next Steps
- [Get Group](get.md)
- [Create Group](create.md)
- [CLI Overview](../intro_cli.md)
