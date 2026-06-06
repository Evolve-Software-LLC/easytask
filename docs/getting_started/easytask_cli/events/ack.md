# Ack Event

The `events ack` command polls for an event's ACK (acknowledgement) status, waiting up to the specified timeout for a response.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `EVENT_ID` | Event ID to check ACK for (required, positional). |
| `--timeout, -t` | Poll timeout in seconds (default: 10.0). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask events ack -h
```

```
 Usage: easytask events ack [OPTIONS] EVENT_ID

 Poll for event ACK status.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  event_id      INTEGER  Event ID to check ACK for [required]              │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --timeout   -t      FLOAT  Poll timeout in seconds (default: 10.0)         │
│ --output    -o      [table\|json\|yaml]  Output format (default: table)    │
│ --help      -h              Show this message and exit.                     │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events ack 101
```

```
╭─ ACK Status ──────────────────────────────╮
│ Event ID    101                            │
│ Status      ACKNOWLEDGED                   │
│ ACK Time    2026-05-12 08:00:02            │
│ Scheduler   default                        │
╰───────────────────────────────────────────╯
```

### **Example — Custom Timeout**

```bash
easytask events ack 101 --timeout 30
```

---

## ⏭️ Next Steps
- [List Events](list.md)
- [Task Runs](../scheduler/task_runs.md)
- [CLI Overview](../intro_cli.md)
