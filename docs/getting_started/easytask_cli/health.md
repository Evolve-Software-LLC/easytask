# Health Check

The `health` command checks if EasyTask is reachable by verifying the frontend proxy and backend API connectivity.

## 🖥️ Basic Usage

```bash
easytask health -h
```

```
 Usage: easytask health [OPTIONS]

 Check if easytask is reachable.

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --help  -h        Show this message and exit.                               │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask health
```

```
✔ Frontend proxy reachable
✔ Backend reachable
```

---

## ⏭️ Next Steps
- [Login](auth/login.md)
- [List Tasks](tasks/list.md)
- [CLI Overview](intro_cli.md)
