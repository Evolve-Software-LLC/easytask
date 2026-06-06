---
title: Web Component Overview - EasyTask Documentation
description: Complete guide to the EasyTask Web Component including login, task management, event monitoring, agent management, administration, and real-time log streaming.
keywords:
  - web component
  - easytask
  - web UI
  - task management
  - dashboard
  - user interface
---

# 🌐 Web Component Documentation

## ✨ Introduction

The **Web Component** is a modern, user-friendly front-end interface designed to deliver a seamless and interactive experience. It enables users to efficiently manage tasks, configure system settings, monitor events, and handle integrations — all from a centralized dashboard.

Each page within the Web Component serves a dedicated purpose, ensuring that users can easily navigate, monitor, and control operations with confidence.

---

## 🔐 Login

The login page is the gateway to the system.

- Enter your **username** (easytask_superuser is the default admin account ) and **password**.
- Click **Login** to access the dashboard.
- If enabled, **multi-factor authentication (MFA)** will prompt you for an additional verification code.

---

## 📋 Key Features

- **Task Management:** Create, modify, and monitor tasks.
- **System Configuration:** Manage agents, schedulers, calendars, and environment settings.
- **Event Monitoring:** Get real-time insights into task execution, alerts, and system health.
- **User Management:** Handle user roles and security access control.
- **Task Logs:** Track task execution logs for troubleshooting.
- **Real-Time Log Streaming:** Watch task execution output live as it happens. Stream logs from any agent or task directly in the browser.
- **Historical Log Viewer:** Browse and search past task execution logs with filtering by date, task, status, and agent. Drill into individual runs for full output and exit codes.
- **Adhoc Command Console:** Execute one-off commands on individual agents or broadcast across the fleet. View real-time output from each agent in an aggregated dashboard.
- **AI Support Chatbot:** Interact with an intelligent assistant to create tasks, update schedules, configure alerts, and manage the platform through natural conversation.

---

## 🧭 Navigation Overview

The navigation bar gives you quick access to major sections:

- 📊 **Client Portal**
- 💼 **Tasks** (Dashboard, Definitions, Runs)
- ⚙️ **Scheduler** (Status)
- 👥 **Agents** (Status)
- 🔌 **Integrations**
- 🛡️ **Administration** (Users, Holidays)

---

## 🛠️ Task Operations
 
Beyond basic definition, the system supports advanced task operations designed for operational flexibility and deep observability.
 
### Ad-hoc Execution
The Ad-hoc Execution feature allows authorized users to bypass the standard schedule and trigger tasks immediately. This is a powerful tool for remediation and testing.
 
- **Permissions:** Restricted to users with **Admin** or **Operator** roles. Viewers cannot initiate ad-hoc runs.
- **Targeting Flexibility:** Executions are not bound to their default hosts. You can opt to run a task against:
    - Its specific primary agent.
    - A selectable list of alternative agents.
    - The **entire agent base**, allowing for broad system-wide maintenance or broadcast commands.
- **Use Cases:** immediate disaster recovery, validating a new task definition against a sandbox agent, or running system-wide diagnostics.
 
### Task Log Viewing
The system implements a sophisticated log retrieval mechanism that provides visibility into distributed processes without requiring direct access to remote servers.
 
- **Retrieval Logic:** When a log is requested, the system dynamically queries the specific execution agent.
    - **Live Streaming*:** A feature that is actively being developed. It will be
    introduced in a future release.
    - **On-Demand Access:** To optimize performance, retrieved logs are cached on-demand, ensuring that subsequent views are instant and do not burden the remote agents.
- **Stream Separation:** The viewer automatically parses and separates **Standard Output (STDOUT)** and **Standard Error (STDERR)**, making it easier to distinguish between normal application flow and critical errors.
- **Limitations:**
    - **Agent Connectivity:** Since logs are fetched directly from the source, the executing agent must be online and reachable to retrieve fresh logs.
    - **Retention:** While historical logs are accessible, they rely on the retention policies configured on the agent nodes.
    - **Size Limit:** Log retrieval is capped at **10MB** by default to prevent browser performance issues. This limit is configurable via the worker agent's configuration file (`.ini`).

 
---

## 🛡️ System Monitoring & Operations

### Agent Management
The Agents section provides deep visibility into your execution infrastructure:
- **Status Monitoring:** Real-time health checks (CPU, Memory, Uptime) for all connected agents.
- **Breached Agents:** A dedicated security view highlights "breached" agents (nodes that violate security policies or connection parameters), allowing for immediate isolation and response.

### Scheduler Container Management
For advanced system administrators, the Scheduler interface allows direct control over the underlying container infrastructure:
- **Container Control:** Start, stop, or restart scheduler containers directly from the UI.
- **Health Checks:** Monitor the connectivity and service status of the scheduler's Podman or Docker environment.

---


---
 
## 🛡️ Administration
 
### Manage Users
User access is governed by a secure, role-based system powered by Keycloak. Administrators can create and manage users, assigning them to one of four distinct roles:
- **Admin:** Full access to all system features.
- **Operator:** Can manage tasks and executions but cannot change system configurations.
- **User:** Standard access for task viewing and limited interactions.
- **Viewer:** Read-only access for monitoring purposes.
 
### Manage Holiday Calendar
The system includes a robust calendar management module that directly influences task scheduling.
- **Holiday Management:** Administrators can define holidays (single dates or ranges) to prevent task executions on specific non-working days.
- **Calendar Organization:** Holidays are grouped by "Calendar Name," allowing for region-specific or team-specific schedules.
- **Integration:** Changes to the holiday calendar trigger an automatic system refresh, ensuring the scheduler immediately respects the new blocked dates.
 
> **Note for On-Premises Deployments:** Clients hosting the solution on-premise have access to an additional **LDAP Federation** module. This feature facilitates the seamless migration and synchronization of users from existing corporate LDAP directories directly into the system's Keycloak authentication provider.
 
---
 
## 💬 Tips for Users

- Use the **search bar** to quickly find tasks or events.
- Check the **notification bell** for system alerts and updates.
- Customize your **profile settings** under the user menu.

---

## ✅ Summary

The Web Component empowers users to:

- 🚀 **Boost productivity** through automation.
- 🛡️ **Improve system reliability** with real-time monitoring.
- 🧩 **Extend functionality** through integrations.

For any issues, refer to the Help section or contact your system administrator.

---

---

## Frequently Asked Questions

**Q: How do I access the EasyTask Web UI?**
A: Open your browser and navigate to the Web Component URL. Enter your username and password on the login page. If MFA is enabled, you will also be prompted for a verification code. The default admin account is `easytask_superuser`.

**Q: Can I view task execution logs in real time?**
A: Yes. The Web Component supports real-time log streaming, allowing you to watch task execution output live in the browser. You can also browse historical logs with filtering by date, task, status, and agent. Note that live streaming is being actively developed for future enhancements.

**Q: What is the Adhoc Command Console?**
A: The Adhoc Command Console allows authorized users (Admin or Operator roles) to execute one-off commands on individual agents or broadcast commands across the entire agent fleet, with real-time output aggregated in a dashboard.

## Next Steps

- [Web Tasks](./web_tasks.md)
- [Web Scheduler](./web_scheduler.md)
- [Web Administration](./web_administration.md)
