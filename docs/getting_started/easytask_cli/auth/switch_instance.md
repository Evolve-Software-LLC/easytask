# Switch Instance

The `auth switch-instance` command switches the active instance. If no instance name is provided, it lists all available instances with the current one highlighted.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `INSTANCE_NAME` | Instance name (positional, optional — omit to list available). |

## 🖥️ Basic Usage

```bash
easytask auth switch-instance -h
```

```
 Usage: easytask auth switch-instance [OPTIONS] [INSTANCE_NAME]

 Switch to a different instance, or list available instances.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│   instance_name      [INSTANCE_NAME]  Instance name (omit to list           │
│                                       available)                            │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example — List Instances**

```bash
easytask auth switch-instance
```

```
┏━━━━━━━━━━━━┳━━━━┳━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓
┃ Name       ┃ ID ┃ Description          ┃ Current         ┃
┡━━━━━━━━━━━━╇━━━━╇━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩
│ default    │ 1  │ Development instance │ ◀ current       │
│ production │ 2  │ Production instance  │                 │
└────────────┴────┴──────────────────────┴─────────────────┘
```

### **Example — Switch Instance**

```bash
easytask auth switch-instance production
```

```
Switched to instance 'production'.
```

---

## ⏭️ Next Steps
- [Who Am I](whoami.md)
- [Health Check](../health.md)
- [CLI Overview](../intro_cli.md)
