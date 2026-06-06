---
title: Worker Agent Management - EasyTask Documentation
description: Start, stop, and restart EasyTask Worker Agents using the watchdog process with lock safeguards and log verification.
keywords:
  - worker agent management
  - easytask
  - start worker agent
  - stop worker agent
  - watchdog process
  - agent restart
---

# 📄 EasyTask Worker Agent Management Guide

---

### 🚀 **Starting an Agent**

The **EasyTask worker agent** (`worker_agent.bin`) is started by a **watchdog process** that runs indefinitely.  
This watchdog automatically monitors the agent and restarts it if it crashes, ensuring high availability.

✅ **Command to start the watchdog:**

```bash
nohup ./watchdog.bin > watchdog.log 2>&1 &
```

✅ **Check agent logs for startup confirmation:**

```bash
cat agent.log
```

**Sample Output Highlights:**

```
                  _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \__ \ |_| | || (_| \__ \   < 
 \___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Worker Agent Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved
...
👉 [INFO] [workeragent:start:38] Worker agent started(node_name=VMware-Virtual-Platform).
```

> 💬 **Important:**  
> Look for the line:  
> `Worker agent started(node_name=VMware-Virtual-Platform)`  
> This confirms that the agent has successfully initialized, registered itself, started heartbeat and admin listener threads , and is ready to execute tasks.

---

### 🔐 **Multiple Agent Safeguards**

The agent uses a combination of file locks and **expiring broker locks** to detect duplicate processes on the same host.

✅ If you accidentally attempt to start another watchdog:

```bash
nohup ./watchdog.bin > watchdog.log 2>&1 &
```

⚠️ **You will see this error:**

```
[ERROR] Found existing .watchdog.lock file - Please check an already running watchdog process.
```

💬 **Why it matters:**  
This lock prevents accidental resource conflicts or task duplication by enforcing a single agent process per host.

---

### 🛑 **Stop Worker Agent**

Run the following command to gracefully stop the Integration Server:

```bash
pkill -f './watchdog.bin'
rm .watchdog.lock
```

---

### 🔄 **Restarting an Agent**

To restart an agent cleanly:

```bash
pkill -f './watchdog.bin'
rm .watchdog.lock
nohup ./watchdog.bin > watchdog.log 2>&1
```

💬 **Step breakdown:**  
- `pkill` → terminates the running watchdog + agent process.  
- `rm .watchdog.lock` → clears the lockfile preventing re-launch.  
- `nohup` → starts the watchdog again in background mode.

---

### ✅ **Summary of Commands**

| 🛠 Action         | 💻 Command                                                      |
|-------------------|----------------------------------------------------------------|
| Start Agent      | `nohup ./watchdog.bin > watchdog.log 2>&1 &`                  |
| Check Logs       | `cat agent.log`                                               |
| Restart Agent    | `pkill -f './watchdog.bin' && rm .watchdog.lock && nohup ./watchdog.bin > watchdog.log 2>&1 &` |

---

### ⚠️ **Best Practices**

- Always check `agent.log` after startup to confirm the agent is running smoothly.  
- **Look for the line:**  
  `Worker agent started(node_name=VMware-Virtual-Platform)` to verify successful startup.
- Do **not** manually start multiple agents on the same host — rely on the watchdog.
- Use restart only if you need to apply updates, change configurations, or recover from lock issues.

---

## Frequently Asked Questions

**Q: How do I start a Worker Agent?**
A: Start the watchdog process using `nohup ./watchdog.bin > watchdog.log 2>&1 &`. The watchdog monitors the agent and automatically restarts it if it crashes. Confirm startup by looking for `Worker agent started` in `agent.log`.

**Q: What prevents me from accidentally running multiple agents on the same host?**
A: The watchdog uses a file lock (`.watchdog.lock`) and expiring broker locks. If you try to start a second watchdog, you will see: `Found existing .watchdog.lock file - Please check an already running watchdog process.`

**Q: How do I safely restart an agent?**
A: Kill the watchdog process with `pkill -f './watchdog.bin'`, remove the lock file with `rm .watchdog.lock`, then start the watchdog again with `nohup ./watchdog.bin > watchdog.log 2>&1 &`.

## Next Steps

- [Worker Agent Troubleshooting](./worker_agent_trouble_shooting.md)
- [Scheduler Management](./scheduler_management.md)
- [Web Component Overview](./web_component.md)
