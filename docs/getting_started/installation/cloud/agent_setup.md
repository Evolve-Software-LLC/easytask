---
title: Cloud Agent Installation - EasyTask Documentation
description: Install EasyTask agents and integration server on Linux hosts using the cloud-based installer with step-by-step instructions.
keywords:
  - easytask cloud installation
  - easytask
  - agent setup
  - integration server
  - cloud deployment
  - linux agent
---

# :cloud: Cloud Agent Installation

This guide covers installing the EasyTask Agent and Integration Server on a Linux host using the cloud-based installer.

---

## :material-clipboard-check: Prerequisites

| Requirement | Details |
|-------------|---------|
| :material-linux: **Operating System** | Linux (Ubuntu 22.04 or later) |
| :material-web: **Network** | Outbound internet access to the EasyTask cloud platform |
| :material-package-variant: **Podman** | Optional — only needed if you plan to run an Integration Server locally |

---

## :material-download: Step 1 — Retrieve the Installer Command

Log in to the **EasyTask Web Console** and navigate to the **Client Portal** dashboard. A download command is displayed there — copy it to your clipboard.

---

## :material-console: Step 2 — Run the Installer

Open a terminal on the target Linux host and paste the command you copied from the portal.

The installer is downloaded and launched automatically. You will see output similar to:

```
============================================================
   EasyTask Agent Installer
============================================================

  Step 1/4: Loading configuration...
```

---

## :material-key-variant: Step 3 — License Verification (First Run Only)

When running the installer for the first time on a host, it will prompt for a one-time password (OTP) to download your license certificates.

```
  Step 2/4: Checking license...

  An OTP has been sent to your registered email.
  Enter OTP: 123456

  License files saved successfully.
```

Enter the 6-digit OTP sent to your registered email address. Once the license has been downloaded for a given host, this step is skipped on subsequent runs.

---

## :material-check-all: Step 4 — Prerequisites Check

The installer validates that all required components are available on the host:

```
  Step 3/4: Checking prerequisites...

  App config loaded from: ~/easytask/config/easytask_config.json
    Broker       ... OK
    Vault        ... OK
    Podman       ... OK (5.4.0)
    Integration Server ... not installed
```

If any prerequisite is missing, the installer warns you and asks whether to proceed.

!!! info ":material-information: Podman is optional"
    Podman is only required for Integration Server installations. The agent installs and runs correctly even without Podman.

---

## :material-format-list-numbered: Step 5 — Select Installation Option

The installer presents an interactive menu:

```
  What would you like to do?

    1. Install Agent
    2. Install Integration Server
    3. Install Both (Agent + Integration Server)
    4. Uninstall Agent
    5. Uninstall Integration Server

  Enter choice [1-5]:
```

---

## :material-robot: Installing an Agent

Select **1** from the menu and provide a name for the agent node:

```
  Enter choice [1-5]: 1

  Enter agent node names (comma-separated): prod-worker-01
  Installing agent(s): prod-worker-01

  Agent installation complete.
```

### :material-robot-outline: Installing Multiple Agents on the Same Host

You can deploy several agents in a single pass by providing comma-separated names:

```
  Enter agent node names (comma-separated): agent-01, agent-02, agent-03
  Installing agent(s): agent-01, agent-02, agent-03

  Agent installation complete.
```

!!! tip ":material-lightbulb-on: Choosing agent names"
    Pick names that are descriptive and easy to identify — for example, based on the hostname, environment, or workload type (e.g. `prod-etl-worker`, `uat-sftp-agent`).

---

## :material-server: Installing the Integration Server

Select **2** from the menu and specify the port for the Integration Server (press Enter to accept the default of 9001):

```
  Enter choice [1-5]: 2

  Enter integration server port [9001]:
  Integration server installation complete.
```

!!! warning ":material-alert: One Integration Server per host"
    Only a single Integration Server can run on a given host. If one is already present, the menu will reflect its installed status.

### :material-server-plus: Installing Both Agent and Integration Server

Select **3** to install both components in a single run. You will be prompted for agent names first, then the Integration Server port:

```
  Enter choice [1-5]: 3

  Enter agent node names (comma-separated): prod-worker-01
  Installing agent(s): prod-worker-01

  Agent installation complete.

  Enter integration server port [9001]:
  Integration server installation complete.

============================================================
   Installation Summary
============================================================
  Agent:               OK
  Integration Server:  OK
============================================================
```

---

## :material-delete-outline: Uninstalling an Agent

Select **4** from the menu. The installer lists installed agents and prompts you to specify which ones to remove:

```
  Enter choice [1-5]: 4

  Installed agents: agent-01, agent-02
  Enter agent node names to uninstall (comma-separated): agent-02

  Agent uninstall complete.
```

---

## :material-server-remove: Uninstalling the Integration Server

Select **5** from the menu:

```
  Enter choice [1-5]: 5

  Integration server uninstalled.
```

---

## :material-shield-check: Verify Installation

### :material-heart-pulse: Check Agent Status

```bash
systemctl --user status easytask-agent-<NODE_NAME>
```

### :material-text-box-search: View Agent Logs

```bash
tail -f ~/easytask/worker_agent/worker_<NODE_NAME>.log
```

### :material-docker: Check Integration Server

```bash
podman ps | grep easytask-intserver
```

---

## :material-arrow-right: Next Steps

With your agents installed and running:

1. :material-monitor-dashboard: **Confirm in the Web Console** — Log in to the EasyTask portal and verify your agents show an online status.
2. :material-pipe: **Configure integrations** — Set up connections to the external systems your workflows depend on.
3. :material-cogs: **Build your workflows** — Start creating tasks, defining schedules, and orchestrating your business processes.

---

## Frequently Asked Questions

**Can I install multiple agents on the same host?**
Yes. When prompted for agent node names, provide comma-separated names (e.g., `agent-01, agent-02, agent-03`) to install several agents in a single run.

**Is Podman required for agent installation?**
No. Podman is only required if you plan to run an Integration Server. The agent installs and runs correctly even without Podman.

**How does license verification work?**
On the first run, the installer sends a one-time password (OTP) to your registered email. Enter the 6-digit OTP to download your license certificates. Subsequent runs on the same host skip this step.

---

## Next Steps

- [Verify Your Installation](../verify_install.md) — Confirm agents and integration server are running
- [Post-Installation Setup](../post_install.md) — Configure pod autostart on boot
- [Task Definition](../../tasks/task.md) — Learn how to create and schedule tasks
