# 🧰 Introduction to Ansible

---

## 📘 What is Ansible?

**Ansible** is an open-source automation tool developed by Red Hat used for:
- Configuration management
- Application deployment
- Infrastructure as Code (IaC)
- Orchestration
- Provisioning

It uses simple **YAML** files called **playbooks** and connects to nodes over **SSH** (no agents needed).

---

## 💡 Key Features

- **Agentless**: No software needs to be installed on managed nodes.
- **Declarative**: Describes the desired state of the system.
- **Idempotent**: Running a task multiple times gives the same result.
- **Simple syntax**: Uses YAML for human-readable playbooks.
- **Extensible**: Use custom modules, roles, plugins.
- **Push-based**: Executes changes from the control node.

---

## 🏗️ Ansible Architecture

| Component       | Description |
|----------------|-------------|
| **Control Node** | The machine where Ansible is installed and commands are run |
| **Managed Nodes** | Target systems (e.g., servers, VMs) to be configured |
| **Inventory**     | List of target hosts (can be static or dynamic) |
| **Modules**       | Units of work (e.g., install package, copy file) |
| **Playbooks**     | YAML files that define tasks to run on hosts |
| **Plugins**       | Extend functionality (callbacks, lookups, etc.) |

---

## 🧪 Why Use Ansible?

- Automate repetitive tasks (install packages, patching)
- Enforce configuration consistency across environments
- Easy to learn and deploy
- Integrates well with CI/CD tools like Jenkins, GitHub Actions

---

## 📦 Typical Use Cases

- Installing and configuring web servers (e.g., Nginx, Apache)
- Managing users and SSH keys
- Automating deployments for Java, Python apps
- Provisioning cloud infrastructure (e.g., GCP, AWS, Azure)
- Patching and maintaining VMs

---

## 📜 Example: Simple Playbook
```yaml
- name: Install and start Apache web server
  hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present

    - name: Ensure Apache is running
      service:
        name: apache2
        state: started
        enabled: yes
```

---

## ⚙️ Command Basics

| Command | Description |
|---------|-------------|
| `ansible` | Run ad-hoc tasks on target nodes |
| `ansible-playbook` | Run full playbooks (YAML files) |
| `ansible-doc` | View documentation for modules |
| `ansible-inventory` | View/manage inventory file |

---

## 🔐 Connection & Authentication

- Uses **SSH** by default
- Can use passwordless **SSH keys**
- Supports sudo access with `become: yes`

---

## 🧠 Summary

| Feature | Value |
|---------|-------|
| Language | YAML |
| Transport | SSH |
| Agent | None (agentless) |
| OS Support | Linux, macOS, Windows (control node on Linux/macOS) |
| Integration | Jenkins, Terraform, Docker, Kubernetes |

Ansible is a powerful tool for automating infrastructure and applications across environments with minimal setup and a flat learning curve.

---
