# Roles List

The `admin roles-list` command lists all available EasyTask roles. Requires **admin** role or higher.

## 🖥️ Basic Usage

```bash
easytask admin roles-list -h
```

```
 Usage: easytask admin roles-list [OPTIONS]

 List available EasyTask roles.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin roles-list
```

```
┏━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Name         ┃ ID                 ┃ Description                        ┃
┡━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┥
│ viewer       │ easytask-web-viewer│ Read-only access to the platform   │
│ user         │ easytask-web-user  │ Standard user with task management │
│ operator     │ easytask-web-operator│ Operator with advanced actions    │
│ admin        │ easytask-web-admin │ Administrator with user management │
│ superadmin   │ easytask-web-superadmin│ Full system access              │
└──────────────┴────────────────────┴────────────────────────────────────┘
```

---

## ⏭️ Next Steps
- [Set Roles](users/set_roles.md)
- [List Users](users/list.md)
- [CLI Overview](../intro_cli.md)
