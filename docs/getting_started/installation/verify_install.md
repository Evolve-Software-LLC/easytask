---
title: Verifying Your Installation - EasyTask Documentation
description: Verify that your EasyTask agents and integration server are running correctly after installation.
keywords:
  - easytask verify installation
  - easytask
  - agent status
  - installation check
  - health check
---

# Verifying Your Installation

After installing EasyTask agents, verify that everything is running correctly.

---

## Check Agent Status

```bash
systemctl --user status easytask-agent-<NODE_NAME>
```

Replace `<NODE_NAME>` with the name you gave the agent during installation.

---

## View Agent Logs

```bash
tail -f ~/easytask/worker_agent/worker_<NODE_NAME>.log
```

---

## Check Integration Server

If you installed the Integration Server:

```bash
podman ps | grep easytask-intserver
```

You should see the `easytask-intserver` container in **Up** status.

---

## Verify in the Web UI

Log in to the EasyTask portal and check that your agents appear as **online** in the dashboard.

---

## Troubleshooting

If an agent is not showing up:

- Check the agent log for errors
- Make sure the host has internet access
- See the [Troubleshooting Guide](./trouble_shoot.md)

---

## Frequently Asked Questions

**How do I check if my agent is running?**
Run `systemctl --user status easytask-agent-<NODE_NAME>` (replace `<NODE_NAME>` with your agent name) — it should show an active status.

**Where are the agent logs located?**
Agent logs are stored at `~/easytask/worker_agent/worker_<NODE_NAME>.log`. Use `tail -f` to follow them in real time.

**Why doesn't my agent show up in the Web UI?**
Check the agent log for errors, ensure the host has internet access, and verify the agent service is running. See the [Troubleshooting Guide](./trouble_shoot.md) for detailed steps.

---

## Next Steps

- [Post-Installation Setup](./post_install.md) — Configure pod autostart on boot
- [Troubleshooting Guide](./trouble_shoot.md) — Resolve common issues
- [Cloud Agent Installation](./cloud/agent_setup.md) — Review full installation instructions
