# List Users

The `admin users list` command lists all users with search and pagination support. Requires **admin** role or higher.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--search, -s` | Search by username/email. |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask admin users list -h
```

```
 Usage: easytask admin users list [OPTIONS]

 List all users.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --search     -s      TEXT  Search by username/email                         │
│ --page       -p            Page number (default: 1)                         │
│ --per-page                 Items per page (default: 25)                     │
│ --output     -o      [table\|json\|yaml]  Output format (default: table)    │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin users list
```

```
┏━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━┓
┃ Username   ┃ Email             ┃ Role         ┃ Active ┃
┡━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━┩
│ admin      │ admin@example.com │ superadmin   │ Y      │
│ jsmith     │ jsmith@corp.com   │ admin        │ Y      │
│ viewer1    │ view@corp.com     │ viewer       │ Y      │
└────────────┴───────────────────┴──────────────┴────────┘
 Page 1 of 1 (3 total users)
```

---

## ⏭️ Next Steps
- [Get User](get.md)
- [Create User](create.md)
- [CLI Overview](../../intro_cli.md)
