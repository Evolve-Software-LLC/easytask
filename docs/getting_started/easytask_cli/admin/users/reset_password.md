# Reset Password

The `admin users reset-password` command resets a user's password. Requires **admin** role or higher. Superadmin accounts cannot be modified by non-superadmin users. If `--password` is omitted, you will be prompted to enter it securely.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `KC_ID` | Keycloak user ID (required, positional). |
| `--password, -p` | New password (prompted if omitted). |
| `--temporary` | Require change on next login. |

## 🖥️ Basic Usage

```bash
easytask admin users reset-password -h
```

```
 Usage: easytask admin users reset-password [OPTIONS] KC_ID

 Reset a user's password.

╭─ Arguments ─────────────────────────────────────────────────────────────────╮
│ *  kc_id      TEXT  Keycloak user ID [required]                             │
╰─────────────────────────────────────────────────────────────────────────────╯
╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --password   -p      TEXT  New password (prompted if omitted)               │
│ --temporary               Require change on next login                      │
│ --help       -h            Show this message and exit.                      │
╰─────────────────────────────────────────────────────────────────────────────╯
```

### **Example**

```bash
easytask admin users reset-password abc123-def456 -p NewSecurePass456!
```

```
Password reset for user abc123-def456.
```

### **Example — Temporary Password**

```bash
easytask admin users reset-password abc123-def456 -p TempPass123! --temporary
```

```
Password reset for user abc123-def456.
User will be required to change password on next login.
```

### **Example — Interactive Password**

```bash
easytask admin users reset-password abc123-def456
```

```
New password: ****
Confirm password: ****
Password reset for user abc123-def456.
```

---

## ⏭️ Next Steps
- [Get User](get.md)
- [List Users](list.md)
- [CLI Overview](../../intro_cli.md)
