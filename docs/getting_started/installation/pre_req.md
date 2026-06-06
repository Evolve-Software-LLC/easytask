---
description: "EasyTask prerequisites — supported Linux distributions (Ubuntu, Debian, RHEL, Rocky, SLES), Podman requirements, and system preparation for installation."
keywords: "EasyTask prerequisites, Linux requirements, Podman installation, system requirements, Ubuntu, RHEL"
---


# ✅ EasyTask Prerequisites

## 🐧 Linux Compatibility

To run **EasyTask**, your system must be based on a supported Linux distribution with a modern and stable version.

> ⚠️ We recommend using **distributions released in 2020 or later** to ensure compatibility with system libraries, security updates, and runtime environments.

---

## ✅ Supported Linux Distributions

- :material-ubuntu: **Ubuntu** ≥ 20.04 LTS  
  User-friendly and widely supported. Avoid older versions like 18.04.

- :material-linux: **Debian** ≥ 11 (Bullseye)  
  Secure and stable, perfect for server environments.

- :material-redhat: **Red Hat Enterprise Linux (RHEL)** ≥ 8  
  Enterprise-grade stability with long-term support.

- :material-redhat: **Rocky Linux** ≥ 8  
  Community-driven RHEL-compatible alternative.

- :material-redhat: **CentOS Stream** ≥ 8  
  Rolling-release preview of RHEL. Not for long-term use in production.

- :material-linux: **openSUSE Leap** ≥ 15.3  
  Reliable and well-supported with powerful system management tools.

- :material-arch: **Arch Linux** (rolling release)  
  Continuously updated. Best for experienced users.

- :material-fedora: **Fedora** ≥ 34  
  Ideal for developers who want the latest software and libraries.

---

> ℹ️ These distributions ensure compatibility with critical system components like `systemd` and `OpenSSL 1.1+`.

---

## ⚙️ System Requirements

Before installing **EasyTask**, please ensure the following system prerequisites are met:

- 🧠 **CPU Architecture**: x86_64 (64-bit)
- 🌐 **Network**: Stable internet connection
- 📦 **Container Runtime**: [Podman](https://podman.io/) installed and configured
- 🔐 **Privileges**: Sufficient permissions to install packages and manage services

---

## 📄 Podman Prerequisite Setup Guide

---

### ⚙️ **Check Podman Socket Status**

```bash
systemctl --user status podman.socket
```

---

### 🔑 **Enable and Start Podman Socket**

```bash
systemctl --user enable --now podman.socket
```

---

### ✅ **Verify Podman Socket Is Active**

```bash
systemctl --user status podman.socket
```

---
## 🧩 Podman API Service Setup

## ⚡ Manual (One-Time) Launch

Use this for quick testing or temporary sessions:

```bash
podman system service --time=0 tcp:0.0.0.0:10001 &
```

> 🔒 The `--time=0` disables automatic shutdown.  
> 🛑 This will run the service in the background .Use a `systemd` service for production use.

---
## 🛠 Recommended: Use Systemd User Service

### 📝 **Create a User-Level Systemd Service for Podman API**

```bash
mkdir -p ~/.config/systemd/user
nano ~/.config/systemd/user/podman-api.service
```

Paste the following:

```ini
[Unit]
Description=Podman API Service
After=network-online.target
Wants=network-online.target

[Service]
ExecStart=/usr/bin/podman system service --time=0 tcp:0.0.0.0:10001
Restart=on-failure

[Install]
WantedBy=default.target
```

> 📝 Replace `/usr/bin/podman` with the correct path (`which podman`) if different.

---

## 🚀 Enable and Start the Podman API Service

```bash
systemctl --user daemon-reload
systemctl --user enable podman-api.service
systemctl --user start podman-api.service
```

---

## 🔍 Verify the Podman API Service is Running and Listening on Port 10001

```bash
systemctl --user status podman-api.service
ss -tuln | grep 10001
```

Expected output:

```
LISTEN  0  128  0.0.0.0:10001  0.0.0.0:*
```

> 🧪 If no output appears, verify the service is running and the port is not blocked by a firewall.

---

### 📌 **Command Summary**

| 🛠 Action                         | 💻 Command                                          |
|----------------------------------|----------------------------------------------------|
| Check Podman socket             | `systemctl --user status podman.socket`           |
| Enable & start socket           | `systemctl --user enable --now podman.socket`     |
| Create Podman API service       | `nano ~/.config/systemd/user/podman-api.service`  |
| Start and enable API service    | `systemctl --user enable --now podman-api.service`|
| Check if API port is listening  | `ss -tuln | grep 10001`                            |

---

### ⚠️ **Reminder**
- Ensure Podman is active before proceeding with EasyTask.
- Port **10001** must be reachable for API communication.

---

## Frequently Asked Questions

### What Linux distributions does EasyTask support?
EasyTask supports a range of modern Linux distributions including Ubuntu 20.04 LTS or later, Debian 11 (Bullseye) or later, Red Hat Enterprise Linux (RHEL) 8 or later, Rocky Linux 8 or later, CentOS Stream 8 or later, openSUSE Leap 15.3 or later, Arch Linux, and Fedora 34 or later. Distributions released in 2020 or later are recommended to ensure compatibility with system libraries like systemd and OpenSSL 1.1+.

### Does EasyTask require Docker or Podman?
EasyTask requires Podman as its container runtime. Podman must be installed and configured on your system before installing EasyTask. The Podman API service needs to be running and listening on port 10001 for EasyTask to communicate with it. You can set up Podman as a systemd user service for production deployments.

### What are the minimum system requirements for EasyTask?
EasyTask requires an x86_64 (64-bit) CPU architecture, a stable internet connection, Podman installed and configured as the container runtime, and sufficient user privileges to install packages and manage system services. A supported Linux distribution released in 2020 or later with systemd and OpenSSL 1.1+ is also required for proper operation.
