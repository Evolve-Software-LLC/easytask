---
description: "Complete reference for the EasyTask CLI — manage tasks, groups, events, agents, scheduler, and admin from the command line."
keywords: "EasyTask CLI, command line, task management, CLI reference, workflow orchestration CLI"
---

# EasyTask CLI Documentation

Welcome to the **EasyTask CLI Documentation**! The EasyTask CLI is a powerful command-line tool that lets you manage tasks, groups, events, agents, and the scheduler directly from your terminal. Use it to automate workflows, script bulk operations, and integrate EasyTask into your CI/CD pipelines.

## 🖥️ EasyTask CLI Overview

```bash
easytask -h
```

```
 Usage: easytask [OPTIONS] COMMAND [ARGS]...

 EasyTask CLI — manage tasks, groups, events, agents, and scheduler.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ──────────────────────────────────────────────────────────────────╮
│ health      Check if easytask is reachable.                                 │
│ auth        Authentication commands.                                        │
│ tasks       Task management.                                                │
│ groups      Group management.                                               │
│ events      Event and action commands.                                      │
│ scheduler   Scheduler operations.                                           │
│ agents      Agent management.                                               │
│ admin       Admin — user and role management.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

## 🖥️ Command Groups

### Health

- [Health Check](health.md) — Check if EasyTask is reachable.

### Authentication

Commands for logging in, logging out, and managing your session.

- [Login](auth/login.md) — Login to EasyTask and store credentials.
- [Logout](auth/logout.md) — Logout and clear stored credentials.
- [Who Am I](auth/whoami.md) — Show current user profile.
- [Refresh Token](auth/refresh.md) — Refresh the authentication token.
- [Switch Instance](auth/switch_instance.md) — Switch to a different instance.

### Tasks

Manage tasks — list, create, update, delete, export, and import.

- [List Tasks](tasks/list.md) — List tasks.
- [Get Task](tasks/get.md) — Get task details.
- [Create Task](tasks/create.md) — Create a task from inline parameters or a JSON file.
- [Update Task](tasks/update.md) — Update a task from inline parameters or a JSON file.
- [Delete Task](tasks/delete.md) — Delete a task.
- [Export Tasks](tasks/export.md) — Export all tasks and groups as JSON.
- [Import Tasks](tasks/import.md) — Import tasks and groups from a JSON file.

### Groups

Manage task groups — list, create, update, and delete.

- [List Groups](groups/list.md) — List groups.
- [Get Group](groups/get.md) — Get group details.
- [Create Group](groups/create.md) — Create a group from inline parameters or a JSON file.
- [Update Group](groups/update.md) — Update a group from inline parameters or a JSON file.
- [Delete Group](groups/delete.md) — Delete a group.

### Events

Event and action commands — force run, enable/disable, freeze/unfreeze, refresh, and more.

- [List Events](events/list.md) — List events.
- [Get Event](events/get.md) — Get event details.
- [Ack Event](events/ack.md) — Poll for event ACK status.
- [Force Run](events/force_run.md) — Force execute a task.
- [Enable Task](events/enable.md) — Enable a task on the scheduler.
- [Disable Task](events/disable.md) — Disable a task on the scheduler.
- [Freeze Task](events/freeze.md) — Freeze a task.
- [Unfreeze Task](events/unfreeze.md) — Unfreeze a task.
- [Terminate Task](events/terminate.md) — Terminate a running task.
- [Modify Status](events/modify_status.md) — Modify a task's status.
- [Refresh Task](events/refresh_task.md) — Reload task definition on scheduler.
- [Refresh Group](events/refresh_group.md) — Reload group definition on scheduler.
- [Refresh Graph](events/refresh_graph.md) — Refresh the dependency graph on scheduler.
- [Refresh Calendar](events/refresh_calendar.md) — Refresh holiday calendars on scheduler.
- [Adhoc Command](events/adhoc.md) — Execute an adhoc command on worker queues.

### Scheduler

Scheduler operations — health, task runs, logs, upcoming tasks, and more.

- [Health](scheduler/health.md) — Check scheduler health.
- [Task Runs](scheduler/task_runs.md) — List task runs with lifecycle.
- [Task Run Logs](scheduler/task_run_logs.md) — Get logs for a task run.
- [Upcoming Tasks](scheduler/upcoming.md) — Show upcoming scheduled tasks.
- [Task Statuses](scheduler/task_statuses.md) — Show latest status per task.
- [State Codes](scheduler/state_codes.md) — List task state codes.
- [Logs](scheduler/logs.md) — List scheduler run logs.

### Agents

Agent management — list, get details, restart, and monitor workers and queues.

- [List Agents](agents/list.md) — List all agents.
- [Get Agent](agents/get.md) — Get agent details.
- [Restart Agent](agents/restart.md) — Send restart action to an agent.
- [Task Stats](agents/task_stats.md) — Get Celery task stats for an agent.
- [Workers](agents/workers.md) — List active Celery workers.
- [Queues](agents/queues.md) — Show worker-to-queue mapping.

### Admin

Admin — user and role management.

- [List Users](admin/users/list.md) — List all users.
- [Get User](admin/users/get.md) — Get user details.
- [Create User](admin/users/create.md) — Create a new user from a JSON file.
- [Update User](admin/users/update.md) — Update a user from a JSON file.
- [Delete User](admin/users/delete.md) — Delete a user.
- [Reset Password](admin/users/reset_password.md) — Reset a user's password.
- [User Roles](admin/users/roles.md) — Get a user's roles.
- [Set Roles](admin/users/set_roles.md) — Add or remove roles for a user.
- [Roles List](admin/roles_list.md) — List available EasyTask roles.

---

## ❓ Frequently Asked Questions

### How do I install the EasyTask CLI?

The EasyTask CLI is installed as part of the EasyTask agent setup. Follow the [installation guide](../installation/download.md) to download and install the CLI on your system. After installation, verify with `easytask health`.

### Do I need to authenticate before using the CLI?

Yes. Run `easytask auth login` to authenticate and store your credentials locally. Once logged in, all subsequent commands use your stored session. You can check your current session with `easytask auth whoami`.

### Can I use the CLI in CI/CD pipelines?

Absolutely. The CLI supports non-interactive login via `--username` and `--password` flags, making it ideal for automated environments. You can also set the `EASYTASK_API_URL` environment variable to configure the API endpoint without passing `--api-url` each time.

### What output formats does the CLI support?

Most list and get commands support `--output table|json|yaml` (default: table). Use JSON or YAML output for scripting and automation, for example: `easytask tasks list --output json`.

### How do I manage multiple EasyTask instances?

Use `easytask auth switch-instance` to switch between registered instances. You can also specify `--api-url` on any command to target a different instance temporarily.

### Can I import and export tasks in bulk?

Yes. Use `easytask tasks export` to export all tasks and groups as JSON, and `easytask tasks import` to import them. This is useful for migrating task definitions between environments or backing up your configuration.

### What roles and permissions does the CLI enforce?

The CLI enforces the same role-based access control as the EasyTask web interface. Admin commands (under `easytask admin`) require the **admin** role or higher. Non-superadmin users cannot assign the superadmin role. Use `easytask admin roles-list` to view available roles.

---

## ⏭️ Next Steps

- [Health Check](health.md) — Verify your CLI connection to EasyTask.
- [Login](auth/login.md) — Authenticate and start using the CLI.
- [List Tasks](tasks/list.md) — Browse your existing tasks.
- [Force Run](events/force_run.md) — Trigger a task execution immediately.
- [List Agents](agents/list.md) — Monitor your registered agents.
- [Task Definition](../tasks/task.md) — Learn about task structure and configuration.
- [Complete User Guide](../../complete-user-guide.md) — Full walkthrough of EasyTask features.
