# Create User

The `admin users create` command creates a new user from a JSON definition file. Requires **admin** role or higher. Non-superadmin users cannot assign the superadmin role.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--file, -f` | JSON file with user definition (required). |

## 🖥️ Basic Usage

```bash
easytask admin users create -h
```

```
 Usage: easytask admin users create [OPTIONS]

 Create a new user from a JSON file.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --file   -f      PATH  JSON file with user definition [required]            │
│ --help   -h            Show this message and exit.                          │
╰─────────────────────────────────────────────────────────────────────────────╯
```

!!! Schema "User Schema"

    ```json
    {
      "username": "jsmith",
      "password": "SecurePass123!",
      "email": "jsmith@example.com",
      "firstName": "John",
      "lastName": "Smith",
      "roles": ["user"],
      "enabled": true
    }
    ```

### **Sample Input**

```json title="user_def.json"
{
  "username": "jsmith",
  "password": "SecurePass123!",
  "email": "jsmith@example.com",
  "firstName": "John",
  "lastName": "Smith",
  "roles": ["user"],
  "enabled": true
}
```

### **Example**

```bash
easytask admin users create -f user_def.json
```

```
User created: jsmith (ID: abc123-def456)
```

---

## ⏭️ Next Steps
- [List Users](list.md)
- [Set Roles](set_roles.md)
- [CLI Overview](../../intro_cli.md)
