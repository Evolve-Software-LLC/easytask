---
title: Task Runs and Dependencies - EasyTask Documentation
description: Monitor real-time task execution, view historical run outcomes, and visualize task dependency graphs in EasyTask.
keywords:
  - task runs
  - easytask
  - task execution
  - dependency graph
  - run history
  - task monitoring
---

### 🏃‍♂️ Runs

Monitor real-time task execution; filter by status, name, time.
The Runs page shows the execution history and live status of tasks.

✅ What it does:

Monitor currently running tasks.   

View historical runs and their outcomes.   

Filter runs by date, status, task name, or group.   

💡 Example:   

Check why the Data_Backup task failed last night.   

Filter to see only failed runs in the last 7 days.  

### 🔗 Dependency

  

The Dependency page visualizes task relationships.   

✅ What it does:   

Display which tasks depend on others.   

Show execution progress in the dependency graph.   

Help identify bottlenecks or failed upstream tasks.   

💡 Example:   

Visualize Generate_Invoice → Send_Email_Invoice.   

See that the email task is waiting on the invoice generation.   

View dependency graphs and progress trackers to visualize workflows.

---

## Frequently Asked Questions

**Q: How do I check why a task failed?**
A: Go to the Runs page and filter by the task name and status "Failed" to see the execution details. You can also filter by date range to narrow down to a specific time period, such as the last 7 days.

**Q: What does the Dependency page show?**
A: The Dependency page visualizes task relationships and execution progress in a dependency graph. It helps you identify bottlenecks, failed upstream tasks, and understand which tasks depend on others.

**Q: Can I see real-time task execution status?**
A: Yes. The Runs page shows currently running tasks and their live status. You can monitor active executions and view historical runs and their outcomes with filtering options.

## Next Steps

- [Web Tasks](./web_tasks.md)
- [Web Component Overview](./web_component.md)
- [Web Scheduler](./web_scheduler.md)
