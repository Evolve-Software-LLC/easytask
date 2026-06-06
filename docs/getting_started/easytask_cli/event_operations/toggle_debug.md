---
title: Toggle Debug Mode - EasyTask CLI - EasyTask Documentation
description: Enable or disable debug mode in the EasyTask scheduler using the toggle debug CLI event commands.
keywords:
  - toggle debug
  - easytask cli
  - debug mode
  - scheduler debugging
---

# Toggle Debug Event

## Enable Debug 

The `enable_debug` command in the EasyTask CLI allows users to enable debug mode for events.

### 🖥️ Basic Usage

```bash

easytask.bin events enable_debug --instances INSTANCES

```

#### **Sample Output**

```sh
Enabled scheduler in DEBUG mode
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events enable_debug --instances default

[INFO] [util:publish_to_message_broker:70] Message published successfully.
[INFO] [util:audit_event:100] Publish Status
[INFO] [util:audit_event:101] {'event_time': '2026-02-12 23:07:17.821701', 'publish_time': '2026-02-12 23:07:17.929018', 'status': 'SUCCESS', 'ret_code': 0}
[INFO] [util:audit_event:126] eventrecord
[INFO] [util:publish_debug:181] Enabled scheduler in DEBUG mode

```

<br></br>

## Diable Debug

The `disable_debug` command in the EasyTask CLI allows users to disable debug mode for events.

### 🖥️ Basic Usage

#### **Sample Input**

```bash
easytask.bin events disable_debug --instances INSTANCES
```

#### **Sample Output**

```sh
Disabled scheduler DEBUG mode
```

### **Example**

```
(venv) USERNAME@HOSTNAME~/PROJECT_DIR/APP_NAME$ easytask.bin events disable_debug --instances default

2026-02-12 23:07:26.359400 [INFO] [util:publish_to_message_broker:70] Message published successfully.
2026-02-12 23:07:26.360006 [INFO] [util:audit_event:100] Publish Status
2026-02-12 23:07:26.360268 [INFO] [util:audit_event:101] {'event_time': '2026-02-12 23:07:26.218210', 'publish_time': '2026-02-12 23:07:26.359275', 'status': 'SUCCESS', 'ret_code': 0}
2026-02-12 23:07:26.360830 [INFO] [util:audit_event:126] eventrecord
2026-02-12 23:07:26.603346 [INFO] [util:publish_debug:181] Disabled scheduler DEBUG mode

```

<br></br>

---

## Frequently Asked Questions

**Q: What does debug mode do?**
A: Debug mode enables verbose logging in the scheduler, useful for troubleshooting task execution issues.

**Q: Does debug mode affect task performance?**
A: Debug mode may slightly impact performance due to increased logging; disable it in production environments.

---

## Next Steps

- [Toggle Task](toggle_task.md) - Enable or disable tasks
- [Refresh Task Definition](refresh_task_definition.md) - Refresh task configuration
- [CLI Introduction](../intro_cli.md) - Get started with the EasyTask CLI
