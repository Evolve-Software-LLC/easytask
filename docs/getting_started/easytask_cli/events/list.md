# List Events

The `events list` command lists events with filtering by task name, event name, status, and pagination support.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--search, -s` | Search. |
| `--task-name` | Filter by task name. |
| `--event-name` | Filter by event name. |
| `--status` | Filter by publish status. |
| `--page, -p` | Page number (default: 1). |
| `--per-page` | Items per page (default: 25). |
| `--output, -o` | Output format: table, json, yaml (default: table). |

## 🖥️ Basic Usage

```bash
easytask events list -h
```

```
 Usage: easytask events list [OPTIONS]

 List events.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --search       -s      TEXT  Search                                         │
│ --task-name            TEXT  Filter by task name                            │
│ --event-name           TEXT  Filter by event name                           │
│ --status               TEXT  Filter by publish status                       │
│ --page         -p            Page number (default: 1)                       │
│ --per-page                   Items per page (default: 25)                   │
│ --output       -o      [table\|json\|yaml]  Output format (default: table)  │
│ --help         -h            Show this message and exit.                    │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask events list
```

```
┏━━━━━━━┳━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┓
┃ ID    ┃ Task              ┃ Event            ┃ Status   ┃ Origin  ┃ Time               ┃ Published By  ┃
┡━━━━━━━╇━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━┩
│ 101   │ data_processing   │ FORCE_RUN        │ SUCCESS  │ CLI     │ 2026-05-12 08:00   │ admin        │
│ 102   │ report_gen        │ ENABLE_TASK      │ SUCCESS  │ CLI     │ 2026-05-12 08:05   │ admin        │
│ 103   │ cleanup_job       │ REFRESH_TASK     │ PENDING  │ CLI     │ 2026-05-12 08:10   │ admin        │
└───────┴───────────────────┴──────────────────┴──────────┴─────────┴────────────────────┴──────────────┘
 Page 1 of 1 (3 total items)
```

---

## ⏭️ Next Steps
- [Get Event](get.md)
- [Ack Event](ack.md)
- [Force Run](force_run.md)
- [CLI Overview](../intro_cli.md)
