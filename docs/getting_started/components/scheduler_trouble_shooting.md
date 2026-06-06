---

## 🛡️ Troubleshooting

- ❌ DB/Broker not connected → Check configs, logs.
- ⏳ Task not triggered → Verify triggers and dependencies.
- 🔗 Unmet dependency → Examine dependency graph.
- 📡 Agent not receiving → Check agent status and connectivity.
- 🔄 Retry not working → Review retry policies and logs.

- Scheduler instance not coming up
		- Broker settings
		- Database settings
	- Task not getting Triggered
		-check task definition, check TZ, dependencies etc etc
	- Task not being submitted to agent
		-check agent queue, check if trigger happened, check if agent is in breached list,check agent aggregator(call home )
	- Task submitted but not receiving status updates back
		-check heartbeat of scheduler subscriber thread , restart scheduler if not updating.
	- Task Dependecys not being met
		-enable debug, check offending task

> 💬 Visit the EasyTask Documentation Portal or contact support for help.
