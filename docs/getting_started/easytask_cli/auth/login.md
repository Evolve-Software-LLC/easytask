# Login

The `auth login` command authenticates with EasyTask and stores credentials locally for subsequent CLI commands.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `--username, -u` | Username (prompted if omitted). |
| `--password, -p` | Password (prompted if omitted). |
| `--api-url` | API base URL (env: `EASYTASK_API_URL`). |

## 🖥️ Basic Usage

```bash
easytask auth login -h
```

```
 Usage: easytask auth login [OPTIONS]

 Login to EasyTask and store credentials.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --username   -u      TEXT  Username (prompted if omitted)                   │
│ --password   -p      TEXT  Password (prompted if omitted)                   │
│ --api-url          TEXT  API base URL                                       │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask auth login -u admin -p mypassword
```

```
Logged in as admin
Instance 'default' selected.
```

### **Example — Interactive Login**

```bash
easytask auth login
```

```
Username: admin
Password: ****
Logged in as admin
Instance 'default' selected.
```

### **Example — Custom API URL**

```bash
easytask auth login -u admin -p mypassword --api-url https://easytask.example.com/api/v1
```

---

## ⏭️ Next Steps
- [Who Am I](whoami.md)
- [Health Check](../health.md)
- [List Tasks](../tasks/list.md)
- [CLI Overview](../intro_cli.md)
