---
title: Integration Server Troubleshooting - EasyTask Documentation
description: Troubleshoot common Integration Server issues in EasyTask including startup failures, connection errors, and performance problems with step-by-step solutions.
keywords:
  - integration server troubleshooting
  - easytask
  - integration server errors
  - integration server logs
  - integration server restart
---

# 🔧 EasyTask Integration Server Troubleshooting

This guide helps you diagnose and resolve common issues with the EasyTask Integration Server.

---

## 🐛 Common Issues and Solutions

| # | Issue | Possible Cause | Solution |
|---|-------|---------------|----------|
| 1 | Server fails to start | Port 8008 already in use | Check for conflicting processes: `lsof -i :8008` or `ss -tlnp \| grep 8008`. Kill the conflicting process or change the port in configuration. |
| 2 | Message broker connection failed | Broker service not running | Verify the message broker (e.g., Redis, RabbitMQ) is running and accessible. Check broker URL and credentials in the configuration file. |
| 3 | Integration requests timing out | Network or firewall issues | Ensure the Integration Server can reach external services. Check firewall rules and DNS resolution. |
| 4 | Heartbeat not being sent | Scheduler unreachable | Verify the scheduler is running and the heartbeat channel is configured correctly. Check message broker connectivity. |
| 5 | SSL/TLS certificate errors | Expired or invalid certificates | Renew or update the certificates in the configuration. Verify the certificate paths are correct. |
| 6 | High memory usage | Too many concurrent integrations | Reduce the number of simultaneous integration requests or increase the container memory limit. |
| 7 | Container exits immediately | Configuration file errors | Check the configuration file for syntax errors or missing required fields. Review container logs for details. |

---

## 📋 Checking Integration Server Logs

Logs are your primary tool for diagnosing issues. Use the following commands:

### View Live Logs

```bash
podman logs -f easytask-intserver
```

### View Recent Logs (Last 100 Lines)

```bash
podman logs --tail 100 easytask-intserver
```

### Search for Errors

```bash
podman logs easytask-intserver 2>&1 | grep -i "error"
```

### Search for Specific Integration Activity

```bash
podman logs easytask-intserver 2>&1 | grep -i "integration"
```

### Key Log Patterns to Watch

| Log Message | Meaning | Action |
|-------------|---------|--------|
| `Uvicorn running on http://0.0.0.0:8008` | Server started successfully | No action needed |
| `MessageBroker client setup successful` | Broker connected successfully | No action needed |
| `Connection refused` | Cannot reach broker or external service | Check service availability |
| `Application shutdown complete.` | Clean shutdown confirmed | Expected during stop |
| `Received signal 15, initiating shutdown` | SIGTERM received | Expected during graceful stop |

---

## 🔄 Restart Procedures

### Standard Restart

```bash
podman stop easytask-intserver
sleep 5
podman start easytask-intserver
```

### Force Restart (if standard stop hangs)

```bash
podman kill easytask-intserver
sleep 3
podman start easytask-intserver
```

### Verify Restart Success

After restarting, confirm the server is healthy:

```bash
podman logs --tail 20 easytask-intserver
```

Look for the line:
```
Uvicorn running on http://0.0.0.0:8008 (Press CTRL+C to quit)
```

---

## 🔍 Diagnostic Checklist

When troubleshooting, follow this checklist:

1. **Check container status**: `podman ps -a | grep easytask-intserver`
2. **Check recent logs**: `podman logs --tail 50 easytask-intserver`
3. **Verify message broker**: Ensure the broker is running and reachable
4. **Verify network connectivity**: Test DNS and port reachability to external services
5. **Check resource usage**: `podman stats easytask-intserver` (CPU, memory)
6. **Review configuration**: Ensure all required settings are present and valid
7. **Check disk space**: Insufficient disk space can cause failures

---

## Frequently Asked Questions

**Q: The Integration Server starts but immediately exits. What should I check?**
A: Check the container logs using `podman logs easytask-intserver` for error messages. The most common cause is a configuration error or the message broker being unreachable. Verify all connection settings in the configuration file and ensure the broker service is running.

**Q: How do I know if the Integration Server is healthy?**
A: Look for the `Uvicorn running on http://0.0.0.0:8008` message in the logs. You can also check that the heartbeat mechanism is active — the server periodically sends health status to the message broker. Use `podman logs -f easytask-intserver` to monitor in real time.

**Q: Integration requests are returning errors. How do I debug them?**
A: First, check the Integration Server logs for detailed error messages. Enable debug mode if available for more verbose output. Verify that the target external service is reachable from the Integration Server container. Check API keys, credentials, and endpoint URLs in the integration configuration.

---

## Next Steps

- [Integration Server Overview](./integration_server.md)
- [Integration Server Management](./integration_server_management.md)
- [Web Component Troubleshooting](./web_trouble_shooting.md)
