# 🐞 Ansible Debugging & Error Handling

---

## 🔍 Why Debugging Matters

Debugging and error handling in Ansible ensures:
- Easier troubleshooting
- More resilient playbooks
- Clear visibility during execution

---

## 🧪 Debug Module

### 📌 Purpose
- Print messages or variable values during playbook execution.

### ✅ Usage Examples
```yaml
- name: Print a static message
  debug:
    msg: "This is a debug message"

- name: Print variable
  debug:
    var: ansible_hostname
```

You can also use conditional debugging:
```yaml
- debug:
    msg: "This only shows if in prod"
  when: env == "production"
```

---

## 📥 Register & Inspect Output

Register output of a task and debug it:
```yaml
- name: Check date
  command: date
  register: result

- name: Show date
  debug:
    var: result.stdout
```

---

## ❌ Error Handling

### 1. `ignore_errors`
- Ignores failure and continues with playbook execution.
```yaml
- name: Attempt to restart a service
  service:
    name: notarealservice
    state: restarted
  ignore_errors: yes
```

---

### 2. `failed_when`
- Define custom failure conditions.
```yaml
- name: Custom failure
  shell: cat /etc/passwd
  register: output
  failed_when: "'root' not in output.stdout"
```

---

### 3. `rescue` & `always` Blocks

Use block-level error handling:
```yaml
- name: Handle errors with rescue
  block:
    - name: Try a risky command
      command: /bin/false
  rescue:
    - name: Handle the failure
      debug:
        msg: "The command failed, but I handled it."
  always:
    - name: Always run this
      debug:
        msg: "Cleanup or notify."
```

---

## 🧪 Test with `check` Mode

Run playbooks in dry-run mode:
```bash
ansible-playbook play.yml --check
```
Does not make any changes, useful for testing logic.

---

## 📝 Verbose Output

Add `-v`, `-vv`, or `-vvv` to increase logging detail.
```bash
ansible-playbook site.yml -vvv
```

---

## 📄 Logging Output

To log output to a file:
```ini
[defaults]
log_path = /var/log/ansible.log
```
In `ansible.cfg`

---

## 🧠 Summary Table

| Feature         | Purpose                            |
|----------------|------------------------------------|
| `debug`        | Print messages/variables            |
| `register`     | Capture task output                |
| `ignore_errors`| Ignore failed task and continue     |
| `failed_when`  | Define custom failure logic         |
| `block/rescue` | Structured error handling           |
| `--check`      | Dry-run playbooks                   |
| `-vvv`         | Increase output verbosity           |
| `log_path`     | Save output to log file             |

---

## ✅ Best Practices

- Use `register` + `debug` to inspect logic and outputs.
- Prefer `failed_when` over blindly ignoring errors.
- Use `rescue` blocks for cleanup and alternative logic.
- Enable logging for long-running or critical playbooks.
- Use verbose mode during development or troubleshooting.

---
