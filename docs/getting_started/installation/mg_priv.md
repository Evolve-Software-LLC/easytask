---
title: Managing Privileges - EasyTask Documentation
description: Configure passwordless sudo access for loginctl enable-linger on Linux systems used by EasyTask.
keywords:
  - easytask privileges
  - easytask
  - sudo configuration
  - loginctl linger
  - passwordless sudo
  - linux permissions
---

# 🛡️ Managing Privileges

## 🔐 Allow a User to Run `sudo loginctl enable-linger <username>` Without a Password

This guide explains how to configure a Linux system so a specific user can run:

```bash
sudo loginctl enable-linger <username>
```

without entering their password. It includes optional steps for installing `sudo` on various Linux distributions and follows best practices for system security.

---

## 📋 Prerequisites

- 🔑 Administrative access to the Linux system  
- 🖥️ Terminal access  
- ✍️ A terminal text editor (`nano`, `vim`, etc.)

---

## 🛠️ Step 1: (Optional) Install `sudo` if Not Available

If running `sudo` gives `command not found`, install it as follows:

### 🐧 Debian/Ubuntu/Mint
```bash
su -
apt update
apt install sudo
```

### 🎩 CentOS/RHEL/Fedora/AlmaLinux
```bash
su -
yum install sudo
```

Or for newer systems:
```bash
su -
dnf install sudo
```

### 🏹 Arch/Manjaro
```bash
su -
pacman -S sudo
```

### ✅ Check Installation
```bash
sudo -V
```

If you see version information, `sudo` is installed correctly.

---

## 🖥️ Step 2: Open the Terminal

Press **Ctrl + Alt + T** or open your terminal via application launcher.

---

## 💾 Step 3: Backup the Sudoers File

Always backup before modifying system-critical files.

```bash
sudo cp /etc/sudoers /etc/sudoers.bak
```

---

## ✏️ Step 4: Edit the Sudoers File Safely

Use `visudo` to edit with syntax validation:

```bash
sudo visudo
```

---

## ⚙️ Step 5: Add the Passwordless Rule

Scroll to the end and add (replace `yourusername`):

```bash
yourusername ALL=(ALL) NOPASSWD: /usr/bin/loginctl enable-linger *
```

📌 Make sure `/usr/bin/loginctl` is the actual path. Verify with:

```bash
which loginctl
```

---

## 💾 Step 6: Save and Exit `visudo`

### If you're in `nano`:
- Press **Ctrl + O**, then **Enter** to save  
- Press **Ctrl + X** to exit

### If you're in `vim`:
- Press **Esc**, type `:wq`, then press **Enter**

---

## 🧪 Step 7: Test Your Setup

Run:

```bash
sudo loginctl enable-linger yourusername
```

✅ You should **not** be asked for a password.

---

## 🔄 Restore the Backup in Case of Failures:

If needed, restore your original sudoers file:

```bash
sudo cp /etc/sudoers.bak /etc/sudoers
```

---

## 🛡️ Best Practices and Caution

### ✅ Do:
- Restrict to specific commands
- Use `visudo` for safe edits
- Double-check paths and usernames
- Maintain backups

### ❌ Don’t:
- Use variables like `$USER` in `sudoers`
- Edit the file with a normal text editor
- Give blanket access with `NOPASSWD: ALL`

---

## 👥 Multiple Users? Use Groups

To allow a group:

```bash
%sudo ALL=(ALL) NOPASSWD: /usr/bin/loginctl enable-linger *
```

---

## 🎉 You're Done!

Your user can now run the specific `loginctl` command without being prompted for a password. You've also learned how to install `sudo` if needed and follow best practices when editing sensitive system files.

---

## Frequently Asked Questions

**Why does EasyTask need `loginctl enable-linger`?**
Lingering keeps the user's systemd session active after logout, which is required for the EasyTask pod to survive reboots and user logouts.

**Is it safe to add a NOPASSWD rule to sudoers?**
Yes, when restricted to a specific command like `/usr/bin/loginctl enable-linger *`. Always use `visudo` to edit the file and avoid giving blanket `NOPASSWD: ALL` access.

**What if I need to configure this for multiple users?**
Use a group-based sudoers rule instead (e.g., `%sudo ALL=(ALL) NOPASSWD: /usr/bin/loginctl enable-linger *`) to avoid managing individual entries.

---

## Next Steps

- [Post-Installation Setup](./post_install.md) — Configure EasyTask pod autostart on boot
- [Verify Your Installation](./verify_install.md) — Confirm everything is running correctly
- [Troubleshooting Guide](./trouble_shoot.md) — Diagnose common setup issues
