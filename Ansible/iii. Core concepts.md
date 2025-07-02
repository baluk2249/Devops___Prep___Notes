# 🧩 Ansible Core Concepts
---

## 1. ✅ Playbooks

- Written in **YAML**.
- Define **tasks** to execute on **target hosts**.
- Central unit of configuration, deployment, and orchestration.

### Example:
```yaml
- name: Install Apache
  hosts: web
  become: true
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```

---

## 2. 🧱 Tasks

- Define individual actions within a playbook.
- Executed **sequentially** on target hosts.

```yaml
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

## 3. 🛠️ Modules

- Reusable units of code that perform specific tasks.
- Hundreds of built-in modules: `copy`, `package`, `user`, `service`, etc.

### Example:
```yaml
- name: Create a user
  user:
    name: deploy
    state: present
```

---

## 4. 🔄 Handlers

- Tasks triggered by **`notify:`** when changes occur.
- Used to perform **idempotent** actions like restarting a service only if config changes.

### Example:
```yaml
  tasks:
    - name: Update nginx config
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Restart nginx

  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
```

---

## 5. 🏷️ Tags

- Run specific parts of a playbook using the `--tags` CLI flag.

### Example:
```yaml
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      tags: nginx
```

Run using:
```bash
ansible-playbook site.yml --tags nginx
```

---

## 6. 🔀 Conditions (`when`)

- Run tasks **conditionally** based on facts or variables.

```yaml
  - name: Install on Debian only
    apt:
      name: apache2
    when: ansible_os_family == "Debian"
```

---

## 7. 🔁 Loops

- Run a task multiple times with different items.

### Example:
```yaml
  - name: Install multiple packages
    apt:
      name: "{{ item }}"
      state: present
    loop:
      - git
      - curl
      - htop
```

---

## 8. 📦 Variables

- Store values for reuse.
- Types: playbook vars, inventory vars, role vars, registered vars, extra vars.

```yaml
  vars:
    app_port: 8080

  tasks:
    - name: Open app port
      ufw:
        rule: allow
        port: "{{ app_port }}"
        proto: tcp
```

---

## 9. 📥 Register

- Capture the **output** of a task into a variable.

```yaml
  - name: Check if user exists
    command: id deploy
    register: user_check
    ignore_errors: yes

  - name: Print user status
    debug:
      msg: "User exists"
    when: user_check.rc == 0
```

---

## 10. 🔍 Facts

- Collected automatically about managed hosts (e.g., OS, IP, memory).
- Use with `ansible_facts` or `ansible_hostname`, `ansible_os_family`, etc.

```yaml
  - name: Show OS family
    debug:
      msg: "This host is {{ ansible_os_family }}"
```

---

## 🧠 Summary Table

| Concept   | Purpose                              |
|-----------|--------------------------------------|
| Playbook | Main file with list of tasks         |
| Task     | Single action to run on a host       |
| Module   | Unit of work like `apt`, `copy`, etc |
| Handler  | Triggered task when changes occur    |
| Tag      | Run specific tasks via CLI flags     |
| When     | Condition to control task execution  |
| Loop     | Repeat task for multiple items       |
| Variable | Store and reuse values               |
| Register | Capture task output as a variable    |
| Facts    | Gathered system info from hosts      |

---
