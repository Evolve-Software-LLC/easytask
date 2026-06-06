# Get User

The `admin users get` command retrieves detailed information about a specific user by their Keycloak ID. Requires **admin** role or higher.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask admin users get -h
```

```
 Usage: easytask admin users get [OPTIONS] KC_ID

 Get user details.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin users get abc123-def456
```

```
╭─────────────── User Details ───────────────╮
│ ID          abc123-def456                   │
│ Username    jsmith                          │
│ Email       jsmith@corp.com                 │
│ First Name  John                            │
│ Last Name   Smith                           │
│ Roles       admin                           │
│ Active      True                            │
│ Created     2026-01-15 10:30:00             │
╰────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Update User](update.md)
- [User Roles](roles.md)
- [Delete User](delete.md)
- [CLI Overview](../../intro_cli.md)
