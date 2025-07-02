# 🧠 Ansible Variables & Facts

---

## 📌 What Are Variables in Ansible?

**Variables** store values that can be reused throughout your playbooks, tasks, and templates.
They help write cleaner, more maintainable, and DRY (Don't Repeat Yourself) code.

---

## 📦 Types of Variables

### 1. **Playbook Variables**
Defined inside playbooks using `vars:` block.
```yaml
- hosts: web
  vars:
    app_port: 8080
  tasks:
    - name: Print port
      debug:
        msg: "App running on port {{ app_port }}"
```

---

### 2. **Extra Variables (Highest Priority)**
Passed via CLI using `--extra-vars` (or `-e`).
```bash
ansible-playbook playbook.yml -e "env=prod region=us"
```

---

### 3. **Inventory Variables**
Defined in inventory files.
```ini
[web]
web1 ansible_user=ubuntu app_env=dev
```

---

### 4. **Host and Group Variables**
Stored in directory structure:
```
inventory/
├── group_vars/
│   └── web.yml
├── host_vars/
│   └── web1.yml
```

**group_vars/web.yml**
```yaml
app_name: myapp
```

**host_vars/web1.yml**
```yaml
hostname: web1-prod
```

---

### 5. **Facts**
Automatically gathered system information.
```yaml
  tasks:
    - name: Show hostname
      debug:
        msg: "Hostname is {{ ansible_hostname }}"
```

---

### 6. **Registered Variables**
Capture task output using `register`.
```yaml
  tasks:
    - name: Get date
      command: date
      register: result

    - name: Print date
      debug:
        var: result.stdout
```

---

### 7. **Default Variables (in Roles)**
Defined in `roles/<role_name>/defaults/main.yml`. Lowest priority.
```yaml
# defaults/main.yml
app_port: 3000
```

---

## ⚖️ Variable Precedence (High to Low)

| Level                          | Method                        |
|-------------------------------|-------------------------------|
| 1                             | Extra Vars (`--extra-vars`)   |
| 2                             | Task-level vars               |
| 3                             | Block-level vars              |
| 4                             | Role vars                     |
| 5                             | Play vars                     |
| 6                             | Inventory vars                |
| 7                             | Fact variables                |
| 8                             | Role defaults                 |

---

## 🔍 Facts in Ansible

- Gathered using `setup` module (default).
- Can be filtered for performance.

### List all facts:
```bash
ansible all -m setup
```

### Filter specific fact:
```bash
ansible all -m setup -a 'filter=ansible_memory_mb'
```

### Disable fact gathering:
```yaml
- hosts: all
  gather_facts: no
```

---

## 🧠 Commonly Used Facts

| Fact Name            | Description                     |
|----------------------|---------------------------------|
| `ansible_hostname`   | Hostname of the machine         |
| `ansible_os_family`  | OS Family (e.g., Debian, RedHat)|
| `ansible_ip_addresses` | List of IP addresses         |
| `ansible_processor`  | CPU details                     |
| `ansible_architecture`| System architecture           |

---

## ✅ Best Practices

- Use `group_vars` and `host_vars` to organize values.
- Prefer `--extra-vars` only for one-time or CLI overrides.
- Use `register` to capture and reuse task results.
- Avoid hardcoding values – use variables and facts.
- Keep sensitive variables encrypted using **Ansible Vault**.

---
