---
description: "Complete glossary of EasyTask terminology — definitions for tasks, schedulers, agents, triggers, dependencies, task lifecycle states, and key platform concepts."
keywords: "EasyTask glossary, task scheduling terminology, workflow orchestration terms, task lifecycle, scheduler definitions, enterprise automation concepts"
---

# :material-book-open-page-variant: EasyTask Terminology & Glossary

A comprehensive reference for every term and concept used across the EasyTask platform. Use this page to look up definitions for tasks, schedulers, agents, integrations, and task lifecycle states.

---

## :material-cog: Core Concepts

**Task**
: A discrete unit of work defined in EasyTask that executes a command on a target agent at a scheduled time or in response to an event. Tasks support retry policies, timeout limits, dependency chains, and calendar-aware scheduling.

**Task Group**
: A named collection of related tasks that are managed together. Task groups allow you to organize workflows by function, department, or business process and apply shared scheduling or dependency rules across all tasks within the group.

**Scheduler**
: The core orchestration engine in EasyTask that evaluates task definitions, manages trigger conditions, dispatches work to agents, and tracks execution status. Multiple schedulers can run with isolated namespaces for load balancing across large deployments.

**Worker Agent**
: A lightweight process deployed on a target host that receives task commands from the scheduler and executes them locally. Agents report execution status, stream real-time logs, and support adhoc command execution for on-the-fly operations.

**Integration Server**
: The component that handles connections between EasyTask and external systems such as databases, messaging platforms, CI/CD tools, and cloud services. EasyTask includes 40+ pre-built integrations managed through the integration server.

**Workflow**
: A multi-step automation sequence composed of tasks linked by dependencies, triggers, and conditional logic. Workflows in EasyTask can span multiple agents, integrate with external systems, and include error handling with automatic retries.

**Dependency**
: A relationship between tasks that determines execution order. If Task B depends on Task A, the scheduler will not trigger Task B until Task A completes successfully. Dependencies enable complex multi-step workflows with guaranteed execution sequencing.

**Trigger**
: An event or condition that causes a task to execute. EasyTask supports time-based triggers (cron schedules), event-driven triggers (external system events), and dependency triggers (completion of upstream tasks).

**Command**
: The shell command or script that a task executes on the target agent. Commands can be shell scripts, Python programs, SQL queries, or any executable available on the agent host. Commands support variable interpolation using environment profiles.

**Calendar**
: A configurable business calendar that defines working days, holidays, and non-working periods. Tasks can be assigned to a calendar so they only execute on valid business days, skipping weekends and configured holidays.

**Task Definition**
: The complete JSON specification of a task, including its command, schedule, target agent, retry policy, timeout, dependencies, calendar, timezone, and alerting rules. Task definitions are stored in the EasyTask database and can be managed via the web UI or CLI.

---

## :material-calendar-clock: Scheduling & Timing

**Cron Expression**
: A time-based scheduling pattern using the standard cron syntax. EasyTask uses trigger times and day-of-week patterns to define when tasks execute, supporting recurring schedules such as daily at 08:30, every weekday at 09:00, or custom time windows.

**Trigger Time**
: The specific time or times at which a task is scheduled to execute on a given day. A task can have multiple trigger times (for example, 08:30 and 14:00) to run at different points throughout the day.

**Day of Week**
: A seven-character binary string (for example, `1111100`) that specifies which days of the week a task is allowed to run. Each position represents Monday through Sunday, where `1` means active and `0` means inactive.

**Timezone**
: The time zone applied to a task's trigger times. EasyTask stores and evaluates schedules using the configured timezone, ensuring tasks fire at the correct local time regardless of where the scheduler is hosted.

**Max Run Time**
: The maximum allowed duration (in seconds) for a single task execution. If a task exceeds this limit, it is automatically terminated. This prevents runaway processes from consuming system resources indefinitely.

**Business Calendar Awareness**
: The ability of a task to skip execution on non-business days such as weekends and public holidays. Calendars are configured per task and ensure tasks only run when the business is operational.

---

## :material-swap-vertical: Task Lifecycle States

**IDLE**
: The initial state of a newly created task that has not yet been activated. The task exists in the database but is not being evaluated by the scheduler for execution.

**ACTIVE**
: The task is enabled and the scheduler is evaluating its trigger conditions. An active task will transition to TRIGGER when its scheduled time arrives and all preconditions are met.

**TRIGGER**
: The scheduler has determined that the task should execute. The task has been moved into the trigger queue and is waiting to be dispatched to an agent.

**STARTING**
: The task has been dispatched to a worker agent and the agent is preparing to execute the command. This is a transitional state between dispatch and actual execution.

**RUNNING**
: The task command is actively executing on the worker agent. The agent is capturing stdout, stderr, and monitoring the process for completion or timeout.

**SUCCESS**
: The task completed successfully. The command exited with a return code of 0 and the agent has reported the result back to the scheduler.

**FAILED**
: The task execution failed. The command exited with a non-zero return code, timed out, or encountered an error. Depending on the retry policy, the scheduler may attempt re-execution.

**TERMINATED**
: The task was manually stopped or killed before it could complete naturally. Termination can be initiated by a user through the web UI, CLI, or API.

**FROZEN**
: A temporary state where the task is paused and will not be evaluated by the scheduler. Frozen tasks retain all their configuration and can be unfrozen to resume normal scheduling.

---

## :material-server: Infrastructure & Deployment

**Namespace**
: An isolated partition within the EasyTask scheduler that groups related tasks and task groups. Namespaces enable multi-tenant or multi-team deployments where different groups have independent scheduling environments on the same platform.

**Instance**
: A running scheduler process operating within a specific namespace. EasyTask supports multiple scheduler instances to distribute workloads horizontally, with each instance handling a dedicated set of tasks.

**Podman**
: The container runtime required by EasyTask for running scheduler and agent components. EasyTask uses Podman (not Docker) for its rootless container architecture, providing enhanced security for enterprise deployments.

**Container Image**
: A pre-packaged EasyTask component (scheduler, agent, integration server) distributed as a Podman container image. Images are pulled from the EasyTask registry during installation.

**Host**
: A physical or virtual machine running one or more EasyTask components. The scheduler, agents, and integration servers can be deployed on the same host or distributed across multiple hosts for scalability.

**Agent Heartbeat**
: A periodic signal sent by each worker agent to the scheduler confirming the agent is alive and ready to accept tasks. If an agent misses heartbeats, the scheduler marks it as unreachable and reroutes tasks to available agents.

**Load Balancing**
: The distribution of tasks across multiple scheduler instances and worker agents to prevent bottlenecks. EasyTask's namespace-based architecture allows horizontal scaling by assigning tasks to specific scheduler instances.

---

## :material-monitor: Monitoring & Observability

**Real-Time Log Streaming**
: The live transmission of task execution output (stdout and stderr) from the worker agent to the web console as the task runs. Users can observe execution progress without logging into the agent host.

**Historical Log**
: A persistent record of a completed task execution, including start time, end time, exit code, duration, and full output. Historical logs are stored in the data store and can be browsed, searched, and filtered.

**Task Run**
: A single execution record of a task. Each time a task is triggered, a new task run is created capturing the execution timeline, status, duration, return code, host, and output. Task runs provide a complete audit trail.

**Audit Trail**
: A chronological record of all actions performed in the EasyTask system, including task creation, modification, execution, status changes, and user operations. Audit trails support compliance and regulatory requirements.

**Alert**
: A notification sent when a task or system event matches a configured condition. Alerts can be delivered via email, Slack, Microsoft Teams, webhooks, or other integration channels.

**Adhoc Command**
: A one-off command executed on demand without defining a task. Adhoc commands can be sent to a single agent, a group of agents, or broadcast across the entire agent fleet for diagnostics, patches, or emergency operations.

---

## :material-connection: Integration & Connectivity

**Integration**
: A pre-built connector that enables EasyTask to interact with an external system such as a database, messaging platform, CI/CD tool, or cloud service. EasyTask includes 40+ integrations covering PostgreSQL, MySQL, Kafka, RabbitMQ, Slack, Jira, ServiceNow, and more.

**Webhook**
: An HTTP callback that sends real-time data to an external system when an event occurs in EasyTask. Webhooks enable event-driven integration with third-party services and custom applications.

**API**
: The REST API exposed by EasyTask for programmatic access to task management, scheduling, monitoring, and configuration. The API supports all operations available in the web UI and CLI.

**Profile**
: A set of environment variables that can be referenced in task commands using interpolation syntax such as `${YYYYMMDD}`. Profiles enable dynamic, context-aware task execution without hardcoding values.

---

## :material-shield-lock: Security & Access

**Role-Based Access Control (RBAC)**
: A permission model that restricts access to EasyTask features and data based on user roles. RBAC ensures that users can only view and manage the tasks, agents, and configurations appropriate to their role.

**Authentication**
: The process of verifying user identity when accessing the EasyTask web console or API. EasyTask supports local authentication and enterprise identity providers via LDAP and SSO integration.

**Client Portal**
: A dedicated interface for external clients or teams to view their own task execution status, logs, and reports without accessing the full administration console.

---

## :material-robot: AI & Automation

**AI Support Chatbot**
: An intelligent assistant built into the EasyTask platform that can create tasks, update schedules, modify configurations, and manage alerts through natural language conversation. The chatbot understands your environment context and translates requests into immediate actions.

---

## :material-arrow-right: Next Steps

- [Getting Started Guide](getting_started/getting_started_intro.md) — walk through your first EasyTask deployment
- [Task Lifecycle](getting_started/components/task_lifecycle.md) — understand how tasks flow through the system
- [Integrations](integrations/integrations_intro.md) — explore 40+ pre-built connectors
- [Beginner's Guide](beginner-guide.md) — plain-language introduction to EasyTask concepts
