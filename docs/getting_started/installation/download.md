---
title: Download the Installer - EasyTask Documentation
description: Download the EasyTask installer from the Client Portal and choose between cloud or on-premises deployment types.
keywords:
  - download easytask installer
  - easytask
  - easytask deployment
  - cloud installation
  - on-premises installation
---

# :material-download-circle: Download the Installer

After purchasing EasyTask, log in to the **EasyTask Web Console** and navigate to the **Client Portal** dashboard. A download command is displayed there — copy it and run it on the Linux host where you plan to install the agent.

The command downloads the installer and launches it automatically, guiding you through the remaining setup steps.

---

## :material-cloud-outline: Deployment Types

### :material-cloud: Cloud Deployment

- EasyTask manages the host infrastructure for you.
- You only install the **EasyTask Agent** (and optionally the **Integration Server**) on your machines.
- Get started with the [Cloud Installation Guide :material-arrow-right:](./cloud/agent_setup.md).

### :material-server-security: On-Premises Deployment

- Coming soon.

---

## :material-arrow-right-bold-box: Next Steps

Choose your deployment path:

| Deployment Type | Guide |
|-----------------|-------|
| :material-cloud: **Cloud** | [Agent Installation Guide :material-arrow-right:](./cloud/agent_setup.md) |
|| :material-server-security: **On-Premises** | Coming soon |

---

## Frequently Asked Questions

**Where do I find the download command?**
Log in to the EasyTask Web Console, navigate to the Client Portal dashboard, and copy the download command displayed there.

**Does the installer require root privileges?**
No. EasyTask uses rootless Podman and user-level systemd services, so no root access is needed for cloud deployments.

**What operating systems are supported?**
EasyTask supports Linux (Ubuntu 22.04 or later). See the [Cloud Agent Installation](./cloud/agent_setup.md) guide for full prerequisites.

---

## Next Steps

- [Cloud Agent Installation Guide](./cloud/agent_setup.md) — Install agents for cloud deployment
- [Verify Your Installation](./verify_install.md) — Confirm your agents are running correctly
- [Troubleshooting Guide](./trouble_shoot.md) — Resolve common installation issues
