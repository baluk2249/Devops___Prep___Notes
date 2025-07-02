# ⚡ Ansible Ad-Hoc Commands
---

## 📌 What Are Ad-Hoc Commands?

**Ad-hoc commands** in Ansible are used to perform quick, one-off tasks on target machines **without writing a playbook**.
They are executed directly from the command line using the `ansible` command.

---

## 📦 Syntax

```bash
ansible <host-pattern> -m <module> -a "arguments" [-i inventory] [options]
```

### 🔍 Example:
```bash
ansible webservers -m ping
```
> Pings all hosts in the 'webservers' group using the `ping` module.

---

## 🔧 Commonly Used Options

| Option | Description |
|--------|-------------|
| `-m`   | Module to use (e.g., ping, shell, copy) |
| `-a`   | Arguments to pass to the module |
| `-i`   | Inventory file location |
| `-u`   | Remote SSH user |
| `-b`   | Use privilege escalation (sudo/become) |
| `-k`   | Prompt for SSH password |
| `--ask-become-pass` | Prompt for sudo password |

---

## ✅ Most Common Ad-Hoc Commands

### 1. 🔍 Ping All Hosts
```bash
ansible all -m ping
```

### 2. 🖥️ Run a Shell Command
```bash
ansible all -m shell -a "uptime"
```

### 3. 📁 Copy a File to Remote Hosts
```bash
ansible all -m copy -a "src=/etc/hosts dest=/tmp/hosts"
```

### 4. 📂 Fetch a File from Remote to Local
```bash
ansible all -m fetch -a "src=/etc/hosts dest=/tmp/ flat=yes"
```

### 5. 🔧 Install a Package
```bash
ansible all -b -m apt -a "name=htop state=present update_cache=true"
```

### 6. 🔄 Restart a Service
```bash
ansible all -b -m service -a "name=apache2 state=restarted"
```

### 7. 👤 Create a User
```bash
ansible all -b -m user -a "name=deploy state=present"
```

### 8. 🔑 Add SSH Key
```bash
ansible all -b -m authorized_key -a "user=ubuntu key='{{ lookup('file', '/home/localuser/.ssh/id_rsa.pub') }}'"
```

### 9. 🔒 Change File Permissions
```bash
ansible all -m file -a "path=/var/www/html mode=0755 recurse=yes"
```

---

## 🧠 Pro Tips

- Use `--limit` to restrict execution to a single host:
```bash
ansible all -m ping --limit web01
```

- Combine with `--tags` or `--check` for dry runs or selective operations.

- Prefer ad-hoc commands for **one-time** tasks; use playbooks for **repeatable** tasks.

---

## 📌 Summary Table

| Module      | Use Case                     |
|-------------|------------------------------|
| `ping`      | Test connectivity            |
| `shell`     | Run shell commands           |
| `command`   | Run basic Linux commands     |
| `copy`      | Copy files to hosts          |
| `fetch`     | Download files from hosts    |
| `apt`/`yum` | Install packages             |
| `service`   | Manage services              |
| `user`      | Manage users                 |
| `file`      | Set file permissions         |
| `authorized_key` | Manage SSH keys         |

---
