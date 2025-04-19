
# 🌱 Terraform Variables - Detailed Notes

## 🔹 What are Terraform Variables?
Terraform variables are used to **parameterize configurations**, allowing reuse and flexibility. They help avoid hardcoding values directly into configuration files.

---

## 1. 📥 Input Variables

### 📌 Purpose:
Input variables allow **customization** of Terraform modules without altering the source code.

### 📘 Syntax:
```hcl
variable "variable_name" {
  type        = string         # Optional but recommended
  default     = "value"        # Optional
  description = "description"  # Optional
  validation {
    condition     = length(var.variable_name) > 0
    error_message = "Cannot be empty"
  }
}
```

### 🎯 Type Constraints (More below):
- `string`
- `number`
- `bool`
- `list(...)`
- `map(...)`
- `object({...})`
- `tuple([...])`
- `any` (default)

---

## 2. 📤 Output Variables

### 📌 Purpose:
Outputs let you **expose data** from your Terraform configuration.

### 📘 Syntax:
```hcl
output "output_name" {
  value       = var.variable_name
  description = "output description"
  sensitive   = true  # Hide in CLI output
}
```

### 💡 Use Cases:
- Pass info to next stage in CI/CD pipeline
- Debugging
- Share values with other modules

---

## 3. 🧠 Local Variables

### 📌 Purpose:
Locals define **temporary named values** used within a module, primarily for **code simplification and reuse**.

### 📘 Syntax:
```hcl
locals {
  full_name = "${var.first_name} ${var.last_name}"
}
```

### ✅ Usage:
```hcl
resource "example" "this" {
  name = local.full_name
}
```

---

## 4. 📦 Type Constraints

### 🌐 Primitive Types:
- `string`
- `number`
- `bool`

### 📚 Complex Types:
- `list(string)` → `["a", "b"]`
- `map(string)` → `{ "key" = "value" }`
- `set(string)` → similar to list, but no duplicates
- `tuple([string, number])` → fixed types in order
- `object({ name = string, age = number })`

### 🔁 Dynamic Type:
- `any` → any type (least restrictive)

---

## 5. 🧮 Variable Precedence (Highest to Lowest)

When Terraform evaluates variables, it uses the following precedence (top has the highest priority):

| Source                            | Priority |
|----------------------------------|----------|
| **Environment variables** (`TF_VAR_`) | ✅ 1     |
| **CLI `-var` option**            | ✅ 2     |
| **CLI `-var-file` option**       | ✅ 3     |
| **Terraform.tfvars**            | ✅ 4     |
| **Terraform.tfvars.json**       | ✅ 5     |
| **Default value in `variable` block** | ✅ 6     |

> 📝 Note: If the same variable is defined in multiple places, **the one with higher precedence wins**.

---

## ✅ Best Practices

- Always define variable types for better validation and clarity.
- Use `description` for maintainability.
- Keep sensitive values like passwords marked as `sensitive = true`.
- Avoid hardcoding — prefer passing via `.tfvars`, CLI, or environment.
- Use locals for computed expressions to simplify configuration logic.

---
