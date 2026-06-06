# Who Am I

The `auth whoami` command displays the current authenticated user's profile information.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask auth whoami -h
```

```
 Usage: easytask auth whoami [OPTIONS]

 Show current user profile.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask auth whoami
```

```
╭─────────────── Current User ───────────────╮
│ Username           admin                    │
│ Email              admin@example.com        │
│ Name               System Administrator    │
│ Role               superadmin              │
│ Active             True                    │
│ Instance           default                 │
│ Allowed Instances  default, production     │
│ Timezone           UTC                     │
│ Dark Mode          False                   │
│ Bot Access         False                   │
│ Sandbox            False                   │
╰───────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Switch Instance](switch_instance.md)
- [Refresh Token](refresh.md)
- [CLI Overview](../intro_cli.md)
