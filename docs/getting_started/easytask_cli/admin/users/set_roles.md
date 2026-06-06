# Set Roles

The `admin users set-roles` command adds or removes roles for a user. Requires **admin** role or higher. Superadmin accounts cannot be modified by non-superadmin users. Non-superadmin users cannot assign the superadmin role.

Role names can be provided in short form (e.g., `admin`) and will be automatically prefixed.

!!! note
    Sessions are invalidated after role changes. The affected user will need to log in again.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |
| `--add, -a` | Comma-separated roles to add. |
| `--remove, -r` | Comma-separated roles to remove. |

## 🖥️ Basic Usage

```bash
easytask admin users set-roles -h
```

```
 Usage: easytask admin users set-roles [OPTIONS] KC_ID

 Add or remove roles for a user.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --add      -a      TEXT  Comma-separated roles to add                       │
│ --remove   -r      TEXT  Comma-separated roles to remove                    │
│ --help     -h            Show this message and exit.                        │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example — Add Roles**

```bash
easytask admin users set-roles abc123-def456 --add admin
```

```
Roles added: admin
Roles removed: (none)
Note: sessions invalidated — user must log in again.
```

### **Example — Add and Remove Roles**

```bash
easytask admin users set-roles abc123-def456 --add admin --remove viewer
```

```
Roles added: admin
Roles removed: viewer
Note: sessions invalidated — user must log in again.
```

---

## ⏭️ Next Steps
- [User Roles](roles.md)
- [Roles List](../roles_list.md)
- [CLI Overview](../../intro_cli.md)
