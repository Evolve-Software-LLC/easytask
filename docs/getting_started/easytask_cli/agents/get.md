# Get Agent

The `agents get` command retrieves detailed information about a specific agent, including heartbeat data, queue info, and broker details.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `AGENT_NAME` | Agent name (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask agents get -h
```

```
 Usage: easytask agents get [OPTIONS] AGENT_NAME

 Get agent details.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  agent_name      TEXT  Agent name [required]                              │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents get worker-01
```

```
╭─────────────── Agent: worker-01 ───────────────╮
│ Name         worker-01                          │
│ Host         10.0.0.1                           │
│ Status       ONLINE                             │
│ Version      2.1.0                              │
│ Queue        default                            │
│ Pool         prefork                            │
│ Agent Mode   production                         │
│ PID          12345                              │
│ CPU%         12.3                               │
│ Memory       256 MB                             │
│ CPU Cores    4                                  │
│ Disk         50 GB                              │
│ Uptime       5d 3h 22m                          │
│ Queues       default, priority                  │
│ Broker       redis://10.0.0.100:6379/0          │
╰────────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Restart Agent](restart.md)
- [Task Stats](task_stats.md)
- [CLI Overview](../intro_cli.md)
