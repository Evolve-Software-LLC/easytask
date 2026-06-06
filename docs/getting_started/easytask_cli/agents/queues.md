# Queues

The `agents queues` command shows the worker-to-queue mapping across all agents.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask agents queues -h
```

```
 Usage: easytask agents queues [OPTIONS]

 Show worker-to-queue mapping.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents queues
```

```
┏━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Worker                  ┃ Queues                ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━┩
│ celery@worker-01        │ default               │
│ celery@worker-02        │ default, priority     │
│ celery@worker-priority  │ priority              │
└─────────────────────────┴───────────────────────┘
```

---

## ⏭️ Next Steps
- [Workers](workers.md)
- [Adhoc Command](../events/adhoc.md)
- [CLI Overview](../intro_cli.md)
