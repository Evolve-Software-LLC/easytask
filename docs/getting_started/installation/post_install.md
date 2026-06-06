---
title: Post-Installation Setup - EasyTask Documentation
description: Configure EasyTask pod autostart on boot using rootless Podman and user-level systemd services.
keywords:
  - easytask post-installation
  - easytask
  - podman autostart
  - systemd service
  - rootless podman
  - pod autostart
---

# 🛠️ Post-Installation: Enable EasyTask Pod Autostart on Boot

Once EasyTask is installed, it's crucial to ensure the application pod starts automatically and remains running — even after a system reboot or user logout.

# 👤 Rootless Podman Setup: Auto-Start EasyTask Pod on Boot (No Root Required)

This guide walks you through configuring your **user-owned EasyTask Podman pod** to start automatically on system boot, 
**without needing root**. This is the preferred method if you're using **rootless Podman**.

---

## 📦 Prerequisites

- EasyTask pod (`easytask_pod`) already created using **non-root Podman**
- Podman installed
- Your user has access to `~/.config/systemd/user/`

---

## ✅ 1. Enable User Lingering

This keeps your user systemd session active even after logout or reboot:

```bash
sudo loginctl enable-linger $USER
```

Verify:

```bash
loginctl show-user $USER | grep Linger
# Output should be: Linger=yes
```

---

## 🛠️ 2. Create a User-Level Systemd Service

```bash
mkdir -p ~/.config/systemd/user
nano ~/.config/systemd/user/easytask-pod.service
```

Paste the following content:

```ini
[Unit]
Description=Start EasyTask Rootless Pod
After=network.target

[Service]
Type=oneshot
RemainAfterExit=true
ExecStart=/usr/bin/podman pod start easytask_pod
ExecStop=/usr/bin/podman pod stop -t 10 easytask_pod

[Install]
WantedBy=default.target
```

> 📝 Replace `/usr/bin/podman` with the correct path (`which podman`) if different.

---

## 🚀 3. Enable and Start the Service

```bash
systemctl --user daemon-reload
systemctl --user enable easytask-pod.service
systemctl --user start easytask-pod.service
```

Check status:

```bash
systemctl --user status easytask-pod.service
```

---

## 🔁 4. Test Autostart on Reboot

Reboot your machine:

```bash
sudo reboot
```

Then confirm:

```bash
podman pod ps
```

You should see `easytask_pod` running automatically.

---

## 🧹 To Disable the Service

```bash
systemctl --user disable easytask-pod.service
```

To remove lingering:

```bash
sudo loginctl disable-linger $USER
```

---

This setup allows EasyTask to run **fully rootless**, persistently, and survive user logouts or system restarts.

---

## Frequently Asked Questions

**What happens if the machine reboots?**
With lingering enabled and the systemd service active, the EasyTask pod starts automatically on boot without manual intervention.

**Can I run EasyTask without rootless Podman?**
EasyTask is designed for rootless operation. This approach is more secure and avoids the need for root privileges.

**How do I check if the pod is running after a reboot?**
Run `podman pod ps` — you should see `easytask_pod` listed with a running status.

---

## Next Steps

- [Verify Your Installation](./verify_install.md) — Confirm agents and pods are running
- [Troubleshooting Guide](./trouble_shoot.md) — Resolve post-installation issues
- [Managing Privileges](./mg_priv.md) — Configure passwordless linger access
