---
title: Command Execution Styles - EasyTask Documentation
description: Professional Markdown command display patterns for EasyTask technical documentation including tabs, copy buttons, and expandable outputs.
keywords:
  - easytask documentation style
  - easytask
  - markdown commands
  - mkdocs code blocks
  - documentation formatting
---

# 💻 Command Execution Styles in Markdown

This guide showcases multiple professional ways to display commands and their outputs in Markdown — ideal for developer documentation or instructional content where users need to copy-paste terminal commands easily.

---

## ✅ Basic Shell Block (Most Common)

```bash
$ easytaskctl init --config /etc/easytask/config.yaml

Initializing scheduler...
✓ Configuration loaded
✓ Scheduler started
```

- Simple, readable, copy-paste ready.
- `$` indicates command line prompt.

---

## 🧾 Split Command and Output (Clearer Separation)

```bash
# Command:
easytaskctl status
```

```text
# Output:
Scheduler is running
Agents: 5 active, 2 idle
Next task: task_104 scheduled at 14:00 UTC
```

- Highlights input vs. output.
- Great for technical tutorials.

---

## 🧪 Tabs for OS Variants (MkDocs Only)

````markdown
=== "Linux / macOS"

    ```bash
    ./install.sh
    ```

=== "Windows"

    ```powershell
    install.bat
    ```
````

> Requires `pymdownx.tabbed` in `mkdocs.yml`.

---

## 📋 With Copy Button (MkDocs Material)

```html
<div class="codehilite">
  <button class="copy-button">Copy</button>
  <pre><code class="language-bash">$ easytaskctl deploy --env prod</code></pre>
</div>
```

- Requires enabling the `copy-button` plugin in MkDocs Material.
- Excellent for UI-friendly docs.

---

## 🔽 Expandable Output (Clean UX for Long Output)

````markdown
??? example "Show Output"

    ```text
    Agent initialized
    Connected to Redis backend
    Listening on port 8793
    ```
````

> Requires `admonition` and `pymdownx.details`.

---

## 🎯 With Icon & Caption (Material Icons)

:material-console: **Run This Command**

```bash
easytaskctl start --debug
```

> Use Material Design Icons in MkDocs for a polished feel.

---

## 🧩 Recommendation

Use:

- **Fenced `bash` blocks** for most users.
- **Tabs** for multi-OS support.
- **Expandable blocks** for long outputs.
- **Copy buttons** for UI polish in MkDocs.

---

## Frequently Asked Questions

**What is the recommended way to display commands in EasyTask docs?**
Use fenced `bash` code blocks for most commands. For multi-OS support, use MkDocs tabs, and for long outputs, use expandable admonition blocks.

**Does MkDocs Material support copy buttons on code blocks?**
Yes, enable the `copy-button` feature in your `mkdocs.yml` configuration to add one-click copy functionality to all code blocks.

**How do I create expandable output sections?**
Use the `??? example` admonition syntax with `pymdownx.details` extension enabled in your MkDocs configuration.

---

## Next Steps

- [Download the Installer](./download.md) — Get started with EasyTask installation
- [Troubleshooting Guide](./trouble_shoot.md) — Common issues and solutions
- [Cloud Agent Installation](./cloud/agent_setup.md) — Full cloud deployment guide

