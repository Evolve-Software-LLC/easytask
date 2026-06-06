---
title: Web Component Troubleshooting - EasyTask Documentation
description: Troubleshoot common EasyTask Web Component issues including login problems, UI errors, connection failures, and performance issues with practical solutions.
keywords:
  - web component troubleshooting
  - easytask
  - web ui errors
  - web component logs
  - easytask web restart
---

# 🔧 EasyTask Web Component Troubleshooting

This guide helps you diagnose and resolve common issues with the EasyTask Web Component.

---

## 🐛 Common Issues and Solutions

| # | Issue | Possible Cause | Solution |
|---|-------|---------------|----------|
| 1 | Web UI not accessible | Container not running or port blocked | Check container status: `podman ps -a \| grep easytask-web`. Verify port 8002 is open: `ss -tlnp \| grep 8002`. |
| 2 | Login page does not load | Gunicorn workers crashed | Check logs: `podman logs easytask-web`. Restart if workers have exited unexpectedly. |
| 3 | Authentication failures | Keycloak service issue | Verify the Keycloak authentication service is running. Check user credentials and role assignments in the Administration panel. |
| 4 | Task dashboard not updating | Message broker disconnected | Ensure the message broker (e.g., Redis) is accessible from the web container. Check broker connection settings. |
| 5 | Slow page load times | High memory usage or too few workers | Monitor resource usage: `podman stats easytask-web`. Consider increasing worker count or container memory. |
| 6 | 502 Bad Gateway | Backend process crashed | Restart the web container. Check logs for Python/Gunicorn errors. |
| 7 | LDAP federation not working | Incorrect LDAP configuration | Verify LDAP URL, Bind DN, credentials, and User DN. Use the "Test LDAP Connection" button before saving. |
| 8 | Cannot view task logs | Agent unreachable | The target worker agent must be online. Check agent connectivity and ensure the agent is registered with the scheduler. |

---

## 📋 Checking Web Component Logs

### View Live Logs

```bash
podman logs -f easytask-web
```

### View Recent Logs (Last 100 Lines)

```bash
podman logs --tail 100 easytask-web
```

### Search for Errors

```bash
podman logs easytask-web 2>&1 | grep -i "error"
```

### Search for Worker Issues

```bash
podman logs easytask-web 2>&1 | grep -i "worker"
```

### Key Log Patterns to Watch

| Log Message | Meaning | Action |
|-------------|---------|--------|
| `Listening at: http://0.0.0.0:8002` | Web server started successfully | No action needed |
| `Worker exiting (pid: ...)` | Gunicorn worker shutting down | Normal during stop; investigate if unexpected |
| `Shutting down: Master` | Master process shutting down | Expected during graceful stop |
| `Handling signal: term` | SIGTERM received | Expected during stop |
| `Connection refused` | Cannot reach backend service | Check dependent services (database, broker, Keycloak) |

---

## 🔄 Restart Procedures

### Standard Restart

```bash
podman stop easytask-web
sleep 5
podman start easytask-web
```

### Force Restart (if standard stop hangs)

```bash
podman kill easytask-web
sleep 3
podman start easytask-web
```

### Verify Restart Success

After restarting, confirm the web component is healthy:

```bash
podman logs --tail 20 easytask-web
```

Look for the line:
```
Listening at: http://0.0.0.0:8002
```

Then open your browser and navigate to the web UI to confirm the login page loads.

---

## 🔍 Diagnostic Checklist

When troubleshooting, follow this checklist:

1. **Check container status**: `podman ps -a | grep easytask-web`
2. **Check recent logs**: `podman logs --tail 50 easytask-web`
3. **Verify port accessibility**: Ensure port 8002 is open and not blocked by firewall
4. **Check dependent services**: Verify database, message broker, and Keycloak are all running
5. **Check resource usage**: `podman stats easytask-web` (CPU, memory)
6. **Test browser connectivity**: Clear browser cache and try accessing the UI in an incognito window
7. **Review authentication**: Ensure Keycloak is running and user accounts are properly configured

---

## Frequently Asked Questions

**Q: The Web UI shows a blank page or fails to load. What should I do?**
A: First, check if the container is running with `podman ps -a | grep easytask-web`. If the container is running, check the logs for errors with `podman logs --tail 50 easytask-web`. Verify that port 8002 is accessible and no firewall rules are blocking it. Try clearing your browser cache or using an incognito window.

**Q: I can log in but the dashboard shows no data or task information.**
A: This usually indicates a message broker connectivity issue. Ensure the message broker (Redis) is running and the web component can reach it. Check the scheduler status as well — if the scheduler is down, task data may not be available. Also verify your user role has permission to view the relevant tasks.

**Q: How do I check if the web component is communicating with the scheduler and agents?**
A: Check the web component logs for any connection errors. Use `podman logs easytask-web 2>&1 | grep -i "broker"` to see message broker connection status. You can also visit the Scheduler Status page in the UI — if it shows instance details and connected workers, communication is working correctly.

---

## Next Steps

- [Web Component Overview](./web_component.md)
- [Web Management Guide](./web_management.md)
- [Integration Server Troubleshooting](./integration_server_trouble_shooting.md)
