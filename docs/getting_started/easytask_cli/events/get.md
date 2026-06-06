# Get Event

The `events get` command retrieves details for a specific event.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `EVENT_ID` | Event ID (required, positional). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask events get -h
```

```
 Usage: easytask events get [OPTIONS] EVENT_ID

 Get event details.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  event_id      INTEGER  Event ID [required]                               │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events get 101
```

```
╭──────────────── Event: 101 ────────────────╮
│ ID           101                           │
│ Task         data_processing               │
│ Event        FORCE_RUN                     │
│ Status       SUCCESS                       │
│ Origin       CLI                           │
│ Time         2026-05-12 08:00:00           │
│ Published By admin                         │
╰────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Ack Event](ack.md)
- [Force Run](force_run.md)
- [CLI Overview](../intro_cli.md)
