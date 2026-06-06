---
title: Scheduler Instance - EasyTask Documentation
description: Understand EasyTask scheduler instances, namespace-based load balancing, and how to scale to 100K+ tasks with multiple isolated instances.
keywords:
  - scheduler instance
  - easytask
  - namespace load balancing
  - task scaling
  - scheduler namespace
---

## 🏷️ Scheduler Instance

A **scheduler instance** provides a logical namespace where specific tasks and groups are isolated for execution.

- 🔄 Task Segmentation & Isolation — Tasks only run within their instance based on task definitions.
- 📦 Namespace-Based Execution — Dedicated execution space for grouped tasks.
- ⚙️ Scalability — Supports multiple instances for large workloads.
- 📊 Dynamic Task Distribution — Optimizes load across instances.

> 💡 **Note:** The system includes a pre-configured default instance. Tasks and groups are assigned to this by default unless otherwise specified.

---

## 📈 Scaling with Multiple Instances (Namespace-Based Load Balancing)

EasyTask supports running **multiple scheduler instances** simultaneously, each operating within its own **isolated namespace**. This architecture enables horizontal scaling and intelligent load distribution across your infrastructure.

### How Namespace-Based Load Balancing Works

Each scheduler instance is assigned a unique namespace (e.g., `finance`, `reporting`, `batch`). Tasks and task groups are mapped to specific namespaces, ensuring they are picked up only by the scheduler instance that owns that namespace.

```
Host A: Scheduler Instance (namespace: finance)    → manages ~10K finance tasks
Host B: Scheduler Instance (namespace: reporting)  → manages ~10K reporting tasks
Host C: Scheduler Instance (namespace: batch)      → manages ~10K batch jobs
```

### Benefits of Multi-Instance Scheduling

- **Load Distribution** — Spread task execution across multiple hosts to prevent any single scheduler from becoming a bottleneck.
- **Namespace Isolation** — Tasks in one namespace are unaffected by issues in another, improving fault tolerance.
- **Horizontal Scaling** — Add more instances as workload grows. A fleet of 10 instances can comfortably manage 100K+ tasks.
- **Operational Flexibility** — Restart, patch, or upgrade individual instances without impacting the entire scheduling fleet.
- **Resource Optimization** — Assign namespaces based on host capacity — powerful hosts handle heavy task groups, lighter hosts handle smaller workloads.

### Example: Scaling to 100K Tasks

| Instances | Hosts | Tasks per Instance | Total Capacity |
|-----------|-------|--------------------|----------------|
| 1         | 1     | 10,000             | 10K            |
| 5         | 5     | 10,000             | 50K            |
| 10        | 10    | 10,000             | 100K+          |

> **Best Practice:** Distribute instances across separate physical or virtual hosts. This provides both load balancing and high availability — if one host fails, only its namespace's tasks are temporarily affected.

---

## ➕ Create a scheduler Instance

A scheduler instance can be createed using CLI or the web UI. 

Refer to Web UI documentation

🔗 [🌐 web UI](../components/web_scheduler.md) 

---

## 🚀 Managing Scheduler Instances

| Action                | Method                               |
|-----------------------|-------------------------------------|
| 🆕 Start Instance     | CLI or Web UI → launch scheduler    |
| 🛑 Stop Instance      | CLI or Web UI → stop scheduler      |
| 🔄 Restart Instance   | CLI or Web UI → restart scheduler   |

---

## Frequently Asked Questions

**Q: What is a scheduler instance and why do I need one?**
A: A scheduler instance provides a logical namespace where specific tasks and groups are isolated for execution. The system includes a pre-configured default instance. You need additional instances when you want to distribute workload across multiple hosts or isolate task execution by team, function, or environment.

**Q: How many tasks can a single scheduler instance handle?**
A: A single scheduler instance can comfortably manage approximately 10,000 tasks. For larger workloads, you can run multiple instances with namespace-based load balancing — for example, 10 instances can manage 100K+ tasks.

**Q: Can I restart one scheduler instance without affecting others?**
A: Yes. Each scheduler instance operates independently within its own namespace. You can restart, patch, or upgrade individual instances without impacting the rest of the scheduling fleet, which is a key benefit of the multi-instance architecture.

## Next Steps

- [Scheduler Overview](./scheduler_new.md)
- [Scheduler Management](./scheduler_management.md)
- [Worker Agent Management](./worker_agent_management.md)
