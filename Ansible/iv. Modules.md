# 🛠️ Ansible Modules 

---

## 📌 What are Modules in Ansible?

Modules are the **building blocks** of Ansible tasks. They are standalone units of code used to perform actions like:
- Installing packages
- Creating files and users
- Managing services
- Interacting with the cloud (GCP, AWS, etc.)

Ansible comes with hundreds of **core modules** and supports **custom modules** as well.

---

## 🧱 Syntax of Using Modules

```yaml
- name: Task description
  module_name:
    option1: value
    option2: value
```

---

## 🔝 Most Commonly Used Modules

### 1. ✅ `ping`
Check connectivity to the target hosts.
```bash
ansible all -m ping
```

### 2. 🖥️ `command`
Run commands on remote machines (does not use a shell).
```yaml
- name: Check uptime
  command: uptime
```

### 3. 🐚 `shell`
Run shell commands (uses shell features like redirection).
```yaml
- name: Run a shell command
  shell: "echo $HOME > /tmp/homepath"
```

### 4. 📦 `apt` / `yum`
Install packages on Debian/RedHat-based systems.
```yaml
- name: Install nginx (Debian)
  apt:
    name: nginx
    state: present
    update_cache: yes

- name: Install httpd (RedHat)
  yum:
    name: httpd
    state: latest
```

### 5. 🧑‍💻 `user`
Create, modify, or delete system users.
```yaml
- name: Create deploy user
  user:
    name: deploy
    state: present
```

### 6. 📂 `file`
Set file properties, create directories, change permissions.
```yaml
- name: Ensure /opt/app directory exists
  file:
    path: /opt/app
    state: directory
    mode: '0755'
```

### 7. 📄 `copy`
Copy files from the control node to managed hosts.
```yaml
- name: Copy app config
  copy:
    src: ./app.conf
    dest: /etc/app/app.conf
```

### 8. 📬 `fetch`
Copy files from managed nodes to the control node.
```yaml
- name: Fetch logs
  fetch:
    src: /var/log/syslog
    dest: ./logs/
    flat: yes
```

### 9. 🛎️ `service`
Manage services (start, stop, restart, enable).
```yaml
- name: Restart Nginx
  service:
    name: nginx
    state: restarted
```

### 10. 🔑 `authorized_key`
Add SSH public keys for a user.
```yaml
- name: Add SSH key for deploy user
  authorized_key:
    user: deploy
    key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
```

---

## 🔐 Security-Related Modules

- `ansible.builtin.seboolean`: Manage SELinux booleans
- `ansible.builtin.ufw`: Configure UFW firewall
- `ansible.posix.firewalld`: Manage firewalld rules

---

## ☁️ Cloud Provider Modules (GCP, AWS, Azure)

- `gcp_compute_instance` (via community collections)
- `ec2`, `s3`, `rds` for AWS
- `azure_rm_virtualmachine`, `azure_rm_storageaccount` for Azure

```yaml
- name: Launch GCP instance
  gcp_compute_instance:
    name: demo-vm
    machine_type: e2-medium
    zone: us-central1-a
```

> ✅ Note: These require cloud SDK setup and authentication.

---

## 🧠 Summary Table

| Module          | Purpose                         |
|------------------|----------------------------------|
| `ping`           | Check connection                |
| `command`        | Run command (no shell)          |
| `shell`          | Run shell command               |
| `apt`/`yum`      | Install packages                |
| `copy`           | Copy files                      |
| `file`           | File and directory management   |
| `user`           | Manage system users             |
| `service`        | Manage system services          |
| `authorized_key` | Manage SSH keys                 |
| `fetch`          | Copy remote files to local      |

---
