---
title: Installation Troubleshooting - EasyTask Documentation
description: Diagnose and resolve common EasyTask installation issues including connectivity, permissions, ports, databases, and license problems.
keywords:
  - easytask troubleshooting
  - easytask
  - installation errors
  - port conflicts
  - database connectivity
  - license issues
---

# 🛠️ EasyTask Installation Troubleshooting Guide

This guide helps you diagnose common installation issues with **EasyTask** using example commands and expected outputs.

---

## ✅ Quick Checklist

- 🌐 Internet connectivity → working
- 🔒 Folder permissions → writable
- 🚪 Required ports → free
- 💽 Disk space → sufficient
- 🛢️ PostgreSQL → running and accessible
- 📦 KeyDB → running and responding
- 🔐 OpenBao → running and healthy
- 🛡️ Keycloak → running and reachable
- 📜 License → valid and active  

---

## 🌐 Internet Connectivity

```bash
curl -I https://www.google.com
```

✅ **Expected:** `HTTP/2 200`  
❌ **If fails:** Check firewall, DNS, or proxy.

```bash
export http_proxy=http://your-proxy:port
export https_proxy=https://your-proxy:port
```

---

## 🔒 Folder Permissions

```bash
ls -ld /path/to/easytask/installer
```

✅ **Expected:** Directory is writable.  
❌ **Fix:**

```bash
chmod u+w /path/to/easytask/installer
```

---

## 🚪 Available Ports

```bash
sudo netstat -tulnp | grep -E '5432|6379|8200|8080'
```

✅ **Expected:** No services on these ports.
❌ **Fix:** Stop conflicting services or change EasyTask port configs.

---

## 💽 Disk Space

```bash
df -h /path/to/easytask
```

✅ **Expected:** At least 50GB free.
❌ **Fix:** Free up disk space.

---

## 🛢️ Database (PostgreSQL)

```bash
psql -U your_user -h localhost -p 5432 -c "\l"
```

✅ **Expected:** PostgreSQL is active and credentials work.
❌ **Fix:** Start PostgreSQL or correct credentials.

---

## 📦 Message Broker (KeyDB)

```bash
nc -zv localhost (hostname or IP) 6379
```

✅ **Expected:** `Connection to localhost (127.0.0.1) 6379 port [tcp/redis] succeeded!`  
❌ **Fix:** Start KeyDB or check configs.

---

## 🔐 Secret Store (OpenBao)

```bash
nc -zv localhost 8200
```

✅ **Expected:** Connection to localhost (127.0.0.1) 8200 port [tcp/redis] succeeded!
❌ **Fix:** Start OpenBao and unseal if needed.

---

## 🛡️ Keycloak

```bash
nc -zv localhost 8080
```

✅ **Expected:** Connection to localhost (127.0.0.1) 8080 port [tcp/redis] succeeded!
❌ **Fix:** Start Keycloak, check logs.

---

## 📜 License Check

```bash
cat /path/to/easytask/license.cert
```

✅ **Expected:** Active, valid certificate  
❌ **Fix:** Renew or apply correct license.

---

> 💬 If issues persist, contact **support@runeasytask.io**.

---

## Frequently Asked Questions

**What should I check first when installation fails?**
Start with the quick checklist: verify internet connectivity, folder permissions, available disk space (at least 50GB), and that required ports (5432, 6379, 8200, 8080) are free.

**How do I check if PostgreSQL is running and accessible?**
Run `psql -U your_user -h localhost -p 5432 -c "\l"` — if it fails, start PostgreSQL or verify your credentials.

**What if my host is behind a proxy?**
Set the `http_proxy` and `https_proxy` environment variables before running the installer so it can reach EasyTask cloud services.

---

## Next Steps

- [Download the Installer](./download.md) — Start a fresh installation
- [Verify Your Installation](./verify_install.md) — Confirm agents are running
- [Post-Installation Setup](./post_install.md) — Configure autostart on boot
