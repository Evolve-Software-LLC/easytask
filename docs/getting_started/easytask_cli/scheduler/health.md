# Scheduler Health

The `scheduler health` command checks the health status of the scheduler, displaying key metrics such as heartbeat age, version, thread information, and worker status.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask scheduler health -h
```

```
 Usage: easytask scheduler health [OPTIONS]

 Check scheduler health.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --output   -o      [table\|json\|yaml]  Output format (default: table)     │
│ --help     -h                        Show this message and exit.           │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask scheduler health
```

```
╭───────────── Scheduler Health ─────────────╮
│ Instance        default                     │
│ Status          HEALTHY                     │
│ Heartbeat Age   2s ago                      │
│ Started At      2026-05-12 06:00:00         │
│ Version         2.1.0                       │
│ Alive Threads   12                          │
│ Workers         4                           │
│ Current Tasks   3                           │
│ Triggers (24h)  128                         │
╰────────────────────────────────────────────╯
```

---

## ⏭️ Next Steps
- [Task Runs](task_runs.md)
- [Upcoming Tasks](upcoming.md)
- [Health Check](../health.md)
- [CLI Overview](../intro_cli.md)
