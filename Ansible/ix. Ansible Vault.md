# 🔐 Ansible Vault

---

## 📌 What Is Ansible Vault?

**Ansible Vault** is a feature used to **encrypt sensitive data** (like passwords, API keys, certificates) in playbooks, variable files, or roles.

Vault allows you to store secrets **securely** and **version control** them without exposing plain text.

---

## 🔑 Creating an Encrypted File

```bash
ansible-vault create secrets.yml
```
- Opens editor to input content
- Saves content encrypted with a password

---

## 🔁 Encrypt an Existing File

```bash
ansible-vault encrypt file.yml
```

### 🔓 Decrypt a File
```bash
ansible-vault decrypt file.yml
```

### 🔄 Re-key a Vault File
```bash
ansible-vault rekey secrets.yml
```

---

## 🛠️ Editing a Vault File

```bash
ansible-vault edit secrets.yml
```
- Opens the encrypted file in your default text editor for secure editing.

---

## 🔍 View Encrypted File (without decrypting permanently)

```bash
ansible-vault view secrets.yml
```

---

## 🔐 Encrypting Variables

### Inside `group_vars/all/vault.yml`
```yaml
vault_db_password: mysecretpassword
```
Encrypt this file:
```bash
ansible-vault encrypt group_vars/all/vault.yml
```

Use in playbook:
```yaml
- name: Use DB password
  debug:
    msg: "The password is {{ vault_db_password }}"
```

---

## 🔧 Using Vault in Playbooks

Run playbook and prompt for password:
```bash
ansible-playbook site.yml --ask-vault-pass
```

Use password file:
```bash
ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt
```

---

## 📁 Using Vault with Roles

Encrypt sensitive defaults, vars, or templates within a role:
```bash
ansible-vault encrypt roles/app/vars/secrets.yml
```

---

## 🔐 Best Practices

- Store **vault password file** securely and outside version control.
- Use **separate vault files** per environment (e.g., prod, dev).
- Combine with `group_vars`, `host_vars`, or role-specific files.
- Use **Ansible Vault IDs** for managing multiple vaults.

---

## 🧠 Vault IDs (Advanced)

Allow managing multiple encrypted sources (e.g., dev/prod):
```bash
ansible-vault encrypt --vault-id dev@prompt dev_secrets.yml
ansible-vault encrypt --vault-id prod@prompt prod_secrets.yml
```
Run with multiple IDs:
```bash
ansible-playbook site.yml --vault-id dev@prompt --vault-id prod@prompt
```

---

## ✅ Summary Table

| Command                                | Description                          |
|----------------------------------------|--------------------------------------|
| `ansible-vault create`                 | Create and encrypt new file          |
| `ansible-vault encrypt file.yml`       | Encrypt existing file                |
| `ansible-vault decrypt file.yml`       | Decrypt file                         |
| `ansible-vault edit file.yml`          | Edit encrypted file                  |
| `ansible-vault view file.yml`          | View contents of vault file          |
| `--ask-vault-pass`                     | Prompt password for decryption       |
| `--vault-password-file`                | Use password file                    |
| `--vault-id`                           | Manage multiple vaults               |

---
