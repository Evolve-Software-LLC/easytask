# Workers

The `agents workers` command lists all active Celery workers across the cluster.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask agents workers -h
```

```
 Usage: easytask agents workers [OPTIONS]

 List active Celery workers.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask agents workers
```

```
┏━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━┓
┃ Worker                  ┃ Status      ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━┩
│ celery@worker-01        │ online      │
│ celery@worker-02        │ online      │
│ celery@worker-priority  │ online      │
└─────────────────────────┴─────────────┘
```

---

## ⏭️ Next Steps
- [Queues](queues.md)
- [List Agents](list.md)
- [CLI Overview](../intro_cli.md)
