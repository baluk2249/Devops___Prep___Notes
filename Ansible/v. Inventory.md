# 📋 Ansible Inventory 

---

## 📌 What is an Inventory in Ansible?

An **inventory** is a file that lists the hosts and groups of hosts on which Ansible commands and playbooks will operate.

It can be in **INI**, **YAML**, or **dynamic** (scripted) format.

---

## 📄 INI Inventory Format (Default)

```ini
[web]
web1.example.com
web2.example.com

[db]
db1.example.com

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

---

## 🧾 YAML Inventory Format

```yaml
all:
  vars:
    ansible_user: ubuntu
    ansible_ssh_private_key_file: ~/.ssh/id_rsa
  children:
    web:
      hosts:
        web1.example.com:
        web2.example.com:
    db:
      hosts:
        db1.example.com:
```

Use this format with:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

---

## 🌐 Dynamic Inventory

- Inventory is generated dynamically using a script or cloud API.
- Useful for **cloud environments** (e.g., GCP, AWS).

### Example:
```bash
ansible-inventory -i gcp_compute_inventory.yml --list
```

Dynamic inventories require plugins and credentials.

---

## 🧠 Host Variables

Defined per host to override defaults.

```ini
[web]
web1 ansible_host=192.168.1.10 ansible_user=ubuntu
```

---

## 🧠 Group Variables

Apply common variables to all hosts in a group.

```ini
[web:vars]
app_env=production
```

In directory format:
```
inventory/
├── hosts
├── group_vars/
│   └── web.yml
├── host_vars/
│   └── web1.yml
```

### group_vars/web.yml
```yaml
app_port: 8080
```

---

## 🔍 Ad-Hoc Command with Inventory

```bash
ansible web -i inventory.ini -m ping
```

---

## 🔐 Authentication Options in Inventory

| Option                        | Description                       |
|------------------------------|-----------------------------------|
| `ansible_user`               | SSH username                      |
| `ansible_ssh_pass`           | SSH password                      |
| `ansible_ssh_private_key_file` | Path to private key             |
| `ansible_port`               | SSH port (default: 22)            |
| `ansible_connection`         | Connection type (e.g., ssh, local)|

---

## 🧠 Best Practices

- Use **group_vars/** and **host_vars/** to organize variables.
- Prefer **YAML inventory** for large-scale and readable formats.
- Use **dynamic inventory** for scalable cloud environments.
- Always test your inventory with:

```bash
ansible-inventory -i inventory.ini --list
```

---

## ✅ Summary Table

| Format   | Use Case                                |
|----------|------------------------------------------|
| INI      | Simple, small-scale environments         |
| YAML     | Large, structured inventory              |
| Dynamic  | Cloud & dynamic infrastructures          |
| group_vars | Group-specific configurations         |
| host_vars  | Host-specific customizations          |

---
