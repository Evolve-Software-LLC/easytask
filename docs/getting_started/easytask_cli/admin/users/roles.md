# User Roles

The `admin users roles` command retrieves the roles assigned to a specific user. Requires **admin** role or higher.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |

## 🖥️ Basic Usage

```bash
easytask admin users roles -h
```

```
 Usage: easytask admin users roles [OPTIONS] KC_ID

 Get a user's roles.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin users roles abc123-def456
```

```
┏━━━━━━━━━━━━┓
┃ Role       ┃
┡━━━━━━━━━━━━┥
│ admin      │
│ user       │
└────────────┘
```

---

## ⏭️ Next Steps
- [Set Roles](set_roles.md)
- [Roles List](../roles_list.md)
- [CLI Overview](../../intro_cli.md)
