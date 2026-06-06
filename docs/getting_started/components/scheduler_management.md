---
title: Scheduler Management - EasyTask Documentation
description: Start, stop, and manage EasyTask Scheduler instances with Podman commands, including log viewing and operational best practices.
keywords:
  - scheduler management
  - easytask
  - start scheduler
  - stop scheduler
  - scheduler logs
---

# 📄 EasyTask Scheduler Control Guide

---

### 🚀 **Starting a Scheduler Instance**

```bash
podman start easytask-scheduler
```

**Output:**
```
                  _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \__ \ |_| | || (_| \__ \   < 
 \___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Scheduler - Workflow Orchestrator Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

[INFO] Starting up processing_thread
[INFO] Starting up submitter_thread
[INFO] Starting up transition_thread
...
👉 **[INFO] Scheduler service started**
``` 
   

> 💬 **Note:** Always look for the line `Scheduler service started` to confirm that the scheduler has started successfully.   
   
> This line is important because it signals that:  

> ✅ All core processing threads have been launched  
> ✅ Database and message broker connections have been established   
> ✅ All task definitions have been loaded and graph construction is complete   
> ✅ The scheduler is ready to accept tasks     

---

### ⏹️ **Stopping a Scheduler Instance**

```bash
podman stop easytask-scheduler
```

**Output:**
```
                  _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \__ \ |_| | || (_| \__ \   < 
 \___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Scheduler - Workflow Orchestrator Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

[INFO] Received signal 15, initiating shutdown.
[INFO] Release locks
[INFO] Stopping multiprocess pool
...
👉 **[INFO] Shutdown Complete.**
```
   

> 💬 **Note:** Always look for the line `Shutdown Complete.` to confirm that the scheduler has stopped cleanly.    
   
> This line is important because it signals that:  
   
> ✅ All threads have been terminated  
> ✅ All data has been flushed to storage  
> ✅ The scheduler has cleanly exited

---

### 📜 **Viewing Scheduler Logs**

```bash
podman logs easytask-scheduler
```

**Sample Output:**
```
                  _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \__ \ |_| | || (_| \__ \   < 
 \___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Scheduler - Workflow Orchestrator Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

[INFO] Operating System -> posix
[INFO] Platform -> linux-x86_64
[INFO] Machine -> x86_64
...
👉 **[INFO] Scheduler service started**
```

---

### ✅ **Summary of Commands**

| 🛠 Action              | 💻 Command                        |
|------------------------|----------------------------------|
| 🚀 Start Scheduler    | `podman start easytask-scheduler` |
| ⏹️ Stop Scheduler     | `podman stop easytask-scheduler`  |
| 📜 View Logs          | `podman logs easytask-scheduler`  |

---

### 📌 **General Notes**
- Always check for:
    - **Start confirmation** → `Scheduler service started`
    - **Shutdown confirmation** → `Shutdown Complete.`
- Use `podman logs` to diagnose issues or verify system details.

---

## Frequently Asked Questions

**Q: How do I confirm the scheduler has started successfully?**
A: Look for the line `Scheduler service started` in the container logs. This confirms that all core processing threads have launched, database and message broker connections are established, and the scheduler is ready to accept tasks.

**Q: What is the clean way to stop the scheduler?**
A: Use `podman stop easytask-scheduler` for a graceful shutdown. Confirm clean shutdown by looking for `Shutdown Complete.` in the logs. This ensures all threads are terminated and all data is flushed to storage.

**Q: How do I check scheduler logs for troubleshooting?**
A: Use `podman logs easytask-scheduler` to view all logs, or `podman logs --tail 50 easytask-scheduler` for the most recent entries. Logs include system details, thread status, and error messages.

## Next Steps

- [Scheduler Overview](./scheduler_new.md)
- [Scheduler Instance](./scheduler_instance.md)
- [Worker Agent Management](./worker_agent_management.md)
