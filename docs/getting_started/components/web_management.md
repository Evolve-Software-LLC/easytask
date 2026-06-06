---
title: Web Management - EasyTask Documentation
description: Start, stop, and manage the EasyTask Web Component container with Podman commands and log verification.
keywords:
  - web management
  - easytask
  - start web component
  - stop web component
  - podman web container
---

# 📄 EasyTask Web Management Guide

---

### 🚀 **Starting EasyTask Web **

```bash
podman start easytask-web
```

✅ **Check web logs for startup confirmation:**

```bash
podman logs easytask-web
```

**Sample Output Highlights:**

```
  ___  __ _ ___ _   _| |_ __ _ ___| | __
 / _ \/ _` / __| | | | __/ _` / __| |/ /
|  __/ (_| \__ \ |_| | || (_| \__ \   < 
 \___|\__,_|___/\__, |\__\__,_|___/_|\_\
                |___/                   

Web Component Version: v0.0.2  © 2025 Evolve Software LLC. All Right Reserved

Setting up MessageBroker client..
[INFO] [glogging:info:278] Starting gunicorn 21.2.0
👉 [INFO] [glogging:info:278] Listening at: http://0.0.0.0:8002 (2)
```

### 🛑 **Stop EasyTask Web**

Run the following command to gracefully stop the Integration Server:

```bash
podman stop easytask-web
```

**Sample Output Highlights:**

```

[INFO] [glogging:info:278] Handling signal: term
[INFO] [glogging:info:278] Worker exiting (pid: 7)
[INFO] [glogging:info:278] Worker exiting (pid: 6)
[INFO] [glogging:info:278] Worker exiting (pid: 9)
[INFO] [glogging:info:278] Worker exiting (pid: 8)
👉 [INFO] [glogging:info:278] Shutting down: Master

```

---

## Frequently Asked Questions

**Q: How do I confirm the Web Component has started successfully?**
A: Check the container logs with `podman logs easytask-web` and look for the line `Listening at: http://0.0.0.0:8002`. This confirms the Gunicorn workers are ready to accept requests.

**Q: What port does the Web Component run on?**
A: The Web Component runs on port `8002` by default, listening on `0.0.0.0`. It is managed as a Podman container named `easytask-web`.

**Q: How do I gracefully stop the Web Component?**
A: Use `podman stop easytask-web`. You will see log messages indicating workers are exiting, followed by `Shutting down: Master` to confirm a clean shutdown.

## Next Steps

- [Web Component Overview](./web_component.md)
- [Web Troubleshooting](./web_trouble_shooting.md)
- [Web Administration](./web_administration.md)
