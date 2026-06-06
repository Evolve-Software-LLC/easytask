---
title: Integration Server Management - EasyTask Documentation
description: Manage the EasyTask Integration Server with start, stop, and monitoring commands using Podman containers.
keywords:
  - integration server management
  - easytask
  - start integration server
  - stop integration server
  - podman containers
---

# 🔧 EasyTask Integration Server Management Guide

---

### 🚀 **Start Integration Server**

Run the following command to start the Integration Server:

```bash
podman start easytask-intserver
```

✅ **Sample Output:**

```
                     _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \\__ \\ |_| | || (_| \\__ \\   < 
 \\___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Integration Server Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

[INFO] Mode: on-prem, Port: 8008, Listen on: 0.0.0.0
[INFO] Setting up message broker
[INFO] MessageBroker client setup successful
[INFO] Registering root signal handler
[INFO] Starting Integration Server
[INFO] Uvicorn running on http://0.0.0.0:8008 (Press CTRL+C to quit)
```

💡 **What to Look For:**  
Look for this line to confirm a successful start:
```
Uvicorn running on http://0.0.0.0:8008 (Press CTRL+C to quit)
```

---

### 🛑 **Stop Integration Server**

Run the following command to gracefully stop the Integration Server:

```bash
podman stop easytask-intserver
```

✅ **Sample Output:**

```
                     _            _    
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \\__ \\ |_| | || (_| \\__ \\   < 
 \\___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/

Integration Server Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

[INFO] Shutting down
[INFO] Waiting for application shutdown.
[INFO] Application shutdown complete.
[INFO] Finished server process
[INFO] Received signal 15, initiating shutdown.
[INFO] Detected shutdown ..
[INFO] Stopping publisher thread ..
```

💡 **What to Look For:**  
Look for this line to confirm a clean shutdown:
```
Application shutdown complete.
```

---

### ⚙️ **Additional Notes**

- 📍 **Port & Address:** The Integration Server runs on port `8008` and listens on `0.0.0.0` by default.
- 🧩 **Mode:** It operates in `on-prem` mode but can be configured for cloud deployments.
- 🔒 **Health & Safety:** Uses a heartbeat (`integration_heartbeat_interval`) to track health and safely exits on termination signals.
- 📈 **Broker Connection:** Integrates with the message broker to handle integration jobs.
- 🛡️ **Graceful Exit:** Ensures that active threads are stopped and resources are cleaned up during shutdown.

---

## Frequently Asked Questions

**Q: How do I confirm the Integration Server started successfully?**
A: Look for the line `Uvicorn running on http://0.0.0.0:8008 (Press CTRL+C to quit)` in the container logs. You can check logs with `podman logs easytask-intserver`.

**Q: What port does the Integration Server run on by default?**
A: The Integration Server runs on port `8008` and listens on `0.0.0.0` by default. It operates in `on-prem` mode but can be configured for cloud deployments.

**Q: How do I safely stop the Integration Server?**
A: Use `podman stop easytask-intserver` for a graceful shutdown. Confirm clean shutdown by looking for `Application shutdown complete.` in the logs.

## Next Steps

- [Integration Server Overview](./integration_server.md)
- [Integration Server Troubleshooting](./integration_server_trouble_shooting.md)
- [Scheduler Management](./scheduler_management.md)
