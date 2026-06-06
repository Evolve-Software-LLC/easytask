# Update User

The `admin users update` command updates a user from a JSON definition file. Requires **admin** role or higher. Superadmin accounts cannot be modified by non-superadmin users.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |
| `--file, -f` | JSON file with fields to update (required). |

## 🖥️ Basic Usage

```bash
easytask admin users update -h
```

```
 Usage: easytask admin users update [OPTIONS] KC_ID

 Update a user from a JSON file.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --file   -f      PATH  JSON file with fields to update [required]           │
│ --help   -h            Show this message and exit.                          │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Sample Input**

```json title="user_update.json"
{
  "email": "john.smith@newcorp.com",
  "firstName": "John",
  "lastName": "Smith-Updated"
}
```

### **Example**

```bash
easytask admin users update abc123-def456 -f user_update.json
```

```
User updated: jsmith
```

---

## ⏭️ Next Steps
- [Get User](get.md)
- [Set Roles](set_roles.md)
- [CLI Overview](../../intro_cli.md)
