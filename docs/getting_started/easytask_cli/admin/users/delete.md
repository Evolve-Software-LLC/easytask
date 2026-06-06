# Delete User

The `admin users delete` command deletes a user by their Keycloak ID. Requires **admin** role or higher. Superadmin accounts cannot be deleted by non-superadmin users.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |

## 🖥️ Basic Usage

```bash
easytask admin users delete -h
```

```
 Usage: easytask admin users delete [OPTIONS] KC_ID

 Delete a user.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin users delete abc123-def456
```

```
User deleted: abc123-def456
```

---

## ⏭️ Next Steps
- [List Users](list.md)
- [Create User](create.md)
- [CLI Overview](../../intro_cli.md)
