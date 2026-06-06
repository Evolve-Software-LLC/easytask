# Restart Agent

The `agents restart` command sends a restart action to a specified agent.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `AGENT_NAME` | Agent name (required, positional). |

## 🖥️ Basic Usage

```bash
easytask agents restart -h
```

```
 Usage: easytask agents restart [OPTIONS] AGENT_NAME

 Send restart action to an agent.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  agent_name      TEXT  Agent name [required]                              │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents restart worker-01
```

```
Restart action sent to agent 'worker-01'.
```

---

## ⏭️ Next Steps
- [List Agents](list.md)
- [Get Agent](get.md)
- [CLI Overview](../intro_cli.md)
