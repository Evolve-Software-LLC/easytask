---
description: "EasyTask task lifecycle — complete end-to-end flow from task creation through scheduling, agent execution, status reporting, and final results. Trace task states in scheduler, agent, and UI logs."
keywords: "EasyTask task lifecycle, task states, task execution flow, scheduler logs, agent logs, task status, IDLE, ACTIVE, RUNNING, SUCCESS, FAILED"
---

# :material-rocket-launch: End-to-End Task Flow

This page describes the complete lifecycle of a task in the system — from creation, through scheduling, execution by an agent, and final status updates shown in the UI.

---

## :material-pencil: 1. Task Creation

A task is created by the user through the UI or API.

Example task definition:

```json
{
  "tid": 1000002,
  "name": "task2",
  "task_owner": "admin",
  "cmd": "ls -l ; sleep 120; ls -l ",
  "run_on_host": "192.168.1.28",
  "max_run_time": 300,
  "description": "A Stray task : Run an ls command",
  "retry_attempts": 3,
  "stderr": "task1.out",
  "stdout": "task1.err",
  "timezone": "US/Eastern",
  "active": true,
  "calendar": "US_HOLIDAYS",
  "instance": "default",
  "day_of_week": "1111111",
  "trigger_times": "08:30",
  "task_accept_expiry_time": 100
}
```

- **UI**: Enter task details using a form or upload a JSON file.
  

- :material-console: **EasyTask CLI**:

```bash
./easytask.bin database task insert --file /tmp/task2.json
```

- **CLI Output Example**:

```
[INFO] [easytask_cli:insert_task:260] task['tid'] = 1000002
[INFO] [easytask_cli:validate_task:234] Validating task: {'tid': 1000002, 'name': 'task2', 'task_owner': 'admin', 'cmd': 'ls -l ; sleep 120; ls -l ', 'run_on_host': '192.168.1.28', 'max_run_time': 300, 'description': 'A Stray task : Run an ls command', 'retry_attempts': 3, 'stderr': 'task1.out', 'stdout': 'task1.err', 'timezone': 'US/Eastern', 'active': True, 'calendar': 'US_HOLIDAYS', 'instance': 'default', 'day_of_week': '1111111', 'trigger_times': '08:30', 'task_accept_expiry_time': 100} for INSERT
[INFO] [task_validator:init:48] task_instance default
[INFO] [buildgraph:build_validation_graph:836] Found 2 tasks and 1 taskgroups
[INFO] [buildgraph:build_validation_graph:853] Task Validations done
[INFO] [easytask_cli:insert_task:283] Task inserted successfully.
[INFO] [easytask_cli:insert_task:300] Calculating hash task={'tid': 1000002, 'name': 'task2', 'task_owner': 'admin', 'cmd': 'ls -l ; sleep 120; ls -l ', 'run_on_host': '192.168.1.28', 'description': 'A Stray task : Run an ls command', 'stderr': 'task1.out', 'stdout': 'task1.err', 'timezone': 'US/Eastern', 'active': True, 'instance': 'default'}
2025-05-09 09:03:28.269599 [INFO] [easytask_cli:insert_task:302] task_hash='c68a4d7c711afffb4f62aa3a393c3921cbf6772a7f4fc143091ea52058812d45'
[INFO] [easytask_cli:print_failures:380] Insert Completed!

```

---

## :material-clock: 2. Scheduler Picks Up the Task

The scheduler periodically polls the task queue and:

- Checks **dependencies**
- Validates **time windows**

:material-check: The task status changes from ``IDLE`` -> ``ACTIVE`` -> ``TRIGGER`` in the UI.

---

## :material-package-variant: 3. Task Sent to Agent

The scheduler dispatches the task to the target agent:

- Agent receives task via internal message broker.
- Status updates from ``TRIGGER`` -> ``STARTING``

:material-check: The UI shows **Dispatched to Agent**.

---

## :material-cog: 4. Agent Executes the Task

The agent:

- Runs the command.
- Captures `stdout` and `stderr`.
- Monitors task completion or failure.
- Status updates from ``RUNNING`` -> ``SUCCESS`` or a ``FAILED`` state

:material-check: Live logs or progress can be viewed in the UI.

---

## :material-bullhorn: 5. Agent Reports Status to Scheduler

Once execution completes:

- Agent sends result (success, failure, timeout) back to scheduler.
- Scheduler updates the task record.

:material-check: The UI shows the final status:
- **:material-check: Success**
- **:material-close: Failed**
- **:material-timer-sand: Timed Out**

---

## :material-magnify: Checking Task States in Scheduler Logs

:material-console: Check scheduler logs to trace task progression and state updates:

```bash
podman logs -f easytask-scheduler
```

Sample scheduler log output:

```

[INFO] [base:evaluate_trigger:114] Task Triggered : task_id=1000002
[DEBUG] [mpu:mpu_trigger_processor:1582] trigger queue {'taskqueue': [], 'triggerqueue': ['1000002:TRIGGER:0:0:20250509 12,30,00.055701']} 1000002:TRIGGER:0:0:20250509 12,30,00.055701 20250509 12,30,00.055701
[DEBUG] [mpu:trigger_consumer:1410] trigger consumer: received ['1000002:TRIGGER:0:0:20250509 12,30,00.055701']
[DEBUG] [mpu:submit_celery_task:1279] task_name:task2
[DEBUG] [mpu:submit_celery_task:1303] _retry_attempts=3, _max_run_time=300, _host_key='192.168.1.28', _stdout='task1.err', _stderr='task1.out'
[DEBUG] [mpu:submit_celery_task:1327] Sending Task :{'cmd': ['bash', '-c', 'ls -l ; sleep 120; ls -l '], 'stdout': 'task1.err', 'stderr': 'task1.out', 'profile': None, 'max_retries': 3, 'task_name': 'task2', 'task_id': 1000002, 'alert': {}, 'run_as_user': None}
[DEBUG] [mpu:submit_celery_task:1332] e5035e1d-7b38-40d7-aa7a-1ff3d6f307f5
[DEBUG] [mpu:submit_celery_task:1334] _uuid_key='e5035e1d-7b38-40d7-aa7a-1ff3d6f307f5'
[DEBUG] [subscriber:update_event:193] Received event: event={'hostname': 'celery@VMware-Virtual-Platform', 'utcoffset': 4, 'pid': 6402, 'clock': 1169, 'uuid': 'e5035e1d-7b38-40d7-aa7a-1ff3d6f307f5', 'name': 'easytask.run_cmd', 'args': '()', 'kwargs': "{'cmd': ['bash', '-c', 'ls -l ; sleep 120; ls -l '], 'stdout': 'task1.err', 'stderr': 'task1.out', 'profile': None, 'max_retries': 3, 'task_name': 'task2', 'task_id': 1000002, 'alert': {}, 'run_as_user': None}", 'root_id': 'e5035e1d-7b38-40d7-aa7a-1ff3d6f307f5', 'parent_id': None, 'retries': 0, 'eta': None, 'expires': '2025-05-09T12:31:40.251098+00:00', 'timestamp': 1746779400.3499613, 'type': 'task-received', 'local_received': 1746793800.3521929}
[DEBUG] [subscriber:update_event:213] Status Updated to STARTED
[DEBUG] [subscriber:update_event:217] Status Updated to RUNNING
[DEBUG] [adapter:insert_one:172] Record: {'date': '20250509', 'tid': '1000002', 'name': 'task2', 'task_group': '', 'pid': '33550', 'job_id': '', 'day_of_week': '1111111', 'local_trigger_times': '09/05/2025 08:30', 'trigger_times': '09/05/2025 12:30', 'start_time': '2025-05-09 12:30:00.352794', 'end_time': '2025-05-09 12:32:00.443509', 'status': 'SUCCESS', 'duration': '120.08368694199999', 'ret_code': '0', 'dependency': '', 'timezone': 'US/Eastern', 'host_name': 'celery@VMware-Virtual-Platform'}

```

---

## :material-wrench: Checking Task States in Agent Logs

:material-console: Agent logs show command execution details:

```bash
cd easytask/easytask-agent
tail -f agent.log
```

Sample agent log output:

```

[INFO] [workeragent:publish_heartbeat:334] heartbeat hash key: easytask_agent:heartbeat:VMware-Virtual-Platform
[INFO] [workeragent:run_cmd:459] Received Task-{'cmd': ['bash', '-c', 'ls'], 'stdout': '/tmp/task1.err', 'stderr': '/tmp/task1.out', 'profile': None, 'max_retries': 3, 'task_name': 'task1', 'task_id': 1000001, 'alert': {}, 'run_as_user': None}
[INFO] [workeragent:run_cmd:460] Task ID: 1000001 UUID -7916c496-49c7-4f38-906b-28b90a13f0ab
[INFO] [workeragent:run_cmd:461] Task execution received at - 2025-05-08 13:14:00.170846
[INFO] [workeragent:run_cmd:462] False
[INFO] [workeragent:run_cmd:486] Interpolated cmd: ID:1000001 ls => ls
[INFO] [workeragent:run_cmd:487] Interpolated stdout: ID:1000001 /tmp/task1.err => /tmp/task1.err
[INFO] [workeragent:run_cmd:488] Interpolated stderr: ID:1000001 /tmp/task1.out => /tmp/task1.out
[INFO] [workeragent:run_cmd:501] Running ls
[INFO] [bash:run_command:41] Running task 1000001 (task1): ls
[INFO] [bash:run_command:42] Task execution started at: 2025-05-08 13:14:00.177871
[INFO] [bash:run_command:66] Task 1000001 (task1) execution finished at: 2025-05-08 13:14:00.187695
[INFO] [bash:run_command:67] Return code: 0, PID: 56929
[INFO] [workeragent:run_cmd:509] Task ID: 1000001 UUID: 7916c496-49c7-4f38-906b-28b90a13f0ab cmd ret code:0 cmd pid: 56929

```

---

## :material-monitor: Checking Task States in the UI

---

## :material-lightbulb: Summary

This flow ensures:

- :material-magnify: **Traceability** — Clear visibility of every task step.
- :material-swap-horizontal: **Real-time updates** — Instant feedback in UI and logs.
- :material-lock: **Reliability** — Robust execution and error handling.

---

## :material-help-circle: Frequently Asked Questions

### What states does a task go through during execution?
A task progresses through these states: IDLE (created but inactive) -> ACTIVE (enabled and being evaluated) -> TRIGGER (scheduled time arrived) -> STARTING (dispatched to agent) -> RUNNING (executing on agent) -> SUCCESS or FAILED or TERMINATED (final state). If retry is configured, a FAILED task may be resubmitted automatically.

### How can I monitor a task's progress in real time?
You can monitor tasks in three ways: the web console shows live status updates and real-time log streaming, scheduler logs (`podman logs -f easytask-scheduler`) show trigger and dispatch events, and agent logs (`tail -f agent.log`) show command execution details including stdout and stderr output.

### What happens when a task fails?
When a task fails, the agent reports the failure status and non-zero return code back to the scheduler. If the task has `retry_attempts` configured, the scheduler will automatically resubmit the task up to the configured number of retries. All attempts are logged with timestamps and output for debugging. If all retries are exhausted, the task remains in FAILED state and alerts are triggered if configured.

---

## :material-arrow-right: Next Steps

- [Task Definition](../tasks/task.md) — how to create and configure tasks
- [Task Groups](../tasks/task_group.md) — organize tasks into managed groups
- [Scheduler Component](scheduler.md) — understand the scheduling engine
- [Worker Agent](worker_agent.md) — how agents execute tasks
- [Troubleshooting](scheduler_trouble_shooting.md) — diagnose common issues
