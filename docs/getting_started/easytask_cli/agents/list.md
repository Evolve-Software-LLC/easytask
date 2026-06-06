# List Agents

The `agents list` command lists all registered agents with their status, resource usage, and uptime.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask agents list -h
```

```
 Usage: easytask agents list [OPTIONS]

 List all agents.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents list
```

```
2 online, 1 offline

┏━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━┳━━━━━━━┳━━━━━━━━━━┓
┃ Name      ┃ Status   ┃ Host        ┃ Queue         ┃ Version ┃ CPU% ┃ Mem%  ┃ Uptime   ┃
┡━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━╇━━━━━━━╇━━━━━━━━━━┩
│ worker-01 │ ONLINE   │ 10.0.0.1    │ default       │ 2.1.0   │ 12.3 │ 34.5  │ 5d 3h    │
│ worker-02 │ ONLINE   │ 10.0.0.2    │ priority      │ 2.1.0   │  8.1 │ 28.2  │ 5d 3h    │
│ worker-03 │ OFFLINE  │ 10.0.0.3    │ default       │ 2.0.9   │  —   │  —    │ —        │
└───────────┴──────────┴─────────────┴───────────────┴─────────┴──────┴───────┴──────────┘
```

---

## ⏭️ Next Steps
- [Get Agent](get.md)
- [Restart Agent](restart.md)
- [Workers](workers.md)
- [CLI Overview](../intro_cli.md)
