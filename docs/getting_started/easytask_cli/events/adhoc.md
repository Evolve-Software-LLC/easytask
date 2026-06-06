# Adhoc Command

The `events adhoc` command executes an adhoc command on specified worker queues. This command requires **operator** role or higher.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--name, -n` | Command name (required). |
| `--cmd, -c` | Command to execute (required). |
| `--queues, -q` | Comma-separated queue names (required). |
| `--stdout` | Stdout file (default: /tmp/adhoc.out). |
| `--stderr` | Stderr file (default: /tmp/adhoc.err). |
| `--max-run-time` | Max run time in seconds (default: 3600). |
| `--retry-attempts` | Retry attempts (default: 0). |
| `--run-as-user` | Run as user. |

## 🖥️ Basic Usage

```bash
easytask events adhoc -h
```

```
 Usage: easytask events adhoc [OPTIONS]

 Execute an adhoc command on worker queues.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --name             -n      TEXT  Command name [required]                    │
│ --cmd              -c      TEXT  Command to execute [required]              │
│ --queues           -q      TEXT  Comma-separated queue names [required]     │
│ --stdout                         Stdout file (default: /tmp/adhoc.out)      │
│ --stderr                         Stderr file (default: /tmp/adhoc.err)      │
│ --max-run-time                   Max run time in seconds (default: 3600)    │
│ --retry-attempts                 Retry attempts (default: 0)                │
│ --run-as-user          TEXT      Run as user                                │
│ --help             -h            Show this message and exit.                │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events adhoc --name cleanup --cmd "/scripts/cleanup.sh" --queues "default,priority"
```

```
Adhoc command 'cleanup' submitted.
Queue(s): default, priority
```

### **Example — With All Options**

```bash
easytask events adhoc --name backup \
  --cmd "/usr/local/bin/backup.sh" \
  --queues "default" \
  --stdout "/var/log/backup.out" \
  --stderr "/var/log/backup.err" \
  --max-run-time 7200 \
  --retry-attempts 2 \
  --run-as-user backup
```

```
Adhoc command 'backup' submitted.
Queue(s): default
```

---

## ⏭️ Next Steps
- [Force Run](force_run.md)
- [Queues](../agents/queues.md)
- [CLI Overview](../intro_cli.md)
