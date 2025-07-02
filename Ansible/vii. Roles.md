# 📦 Ansible Roles & Reusability

---

## 📌 What Are Ansible Roles?

**Roles** are a way of organizing playbooks and related files into **reusable and maintainable components**.
They help you:
- Break down complex playbooks
- Reuse code across environments or teams
- Separate configuration logic cleanly

---

## 🗂️ Default Directory Structure

Ansible expects a specific structure under the `roles/` directory:

```
roles/
├── webserver/
│   ├── defaults/
│   │   └── main.yml
│   ├── files/
│   │   └── index.html
│   ├── handlers/
│   │   └── main.yml
│   ├── meta/
│   │   └── main.yml
│   ├── tasks/
│   │   └── main.yml
│   ├── templates/
│   │   └── nginx.conf.j2
│   ├── vars/
│   │   └── main.yml
```

---

## 📁 Role Subdirectories Explained

| Directory     | Purpose                                       |
|---------------|-----------------------------------------------|
| `tasks/`      | Main list of tasks                            |
| `handlers/`   | Handlers for events like service restart      |
| `defaults/`   | Default variables (lowest precedence)         |
| `vars/`       | Variables with higher precedence              |
| `files/`      | Static files to copy                          |
| `templates/`  | Jinja2 templates                              |
| `meta/`       | Role dependencies                            |

---

## 🧪 Sample Role Task File

**roles/webserver/tasks/main.yml**
```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present

- name: Deploy index.html
  copy:
    src: index.html
    dest: /var/www/html/index.html

- name: Start nginx
  service:
    name: nginx
    state: started
    enabled: true
```

---

## ▶️ Using Roles in Playbooks

```yaml
- name: Configure Web Server
  hosts: web
  become: true
  roles:
    - webserver
```

---

## ➕ Creating a Role

```bash
ansible-galaxy init myrole
```
This creates the complete directory structure automatically.

---

## 🔗 Role Dependencies (meta/main.yml)

```yaml
---
dependencies:
  - { role: common }
  - { role: firewall }
```

---

## 🔁 Reusability Benefits

- Standardized and consistent configuration.
- Easier collaboration across teams.
- Encapsulated logic, minimal duplication.
- Ideal for managing application stacks (e.g., LAMP, ELK).

---

## 🌐 Using Roles from Ansible Galaxy

Search & install reusable community roles:
```bash
ansible-galaxy install geerlingguy.nginx
```

In playbook:
```yaml
roles:
  - geerlingguy.nginx
```

---

## ✅ Best Practices

- Use roles for any reusable component.
- Keep role responsibilities focused (1 app or service per role).
- Use `defaults/` for configurable values.
- Test roles independently.
- Document purpose and variables inside each role.

---

## 🧠 Summary Table

| Feature         | Purpose                                |
|----------------|----------------------------------------|
| Role            | Reusable config unit                   |
| `tasks/`        | Main tasks file                        |
| `handlers/`     | Triggered events (e.g., restart)       |
| `defaults/`     | Lowest priority vars                   |
| `templates/`    | Dynamic config files                   |
| `meta/`         | Dependency definition                  |

---
