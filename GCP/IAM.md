# GCP IAM Notes

## GCP IAM Overview
Google Cloud Identity and Access Management (IAM) allows you to control access to cloud resources by defining **who** (identity) has **what permissions** (roles) on **which resources**.

## Identity in GCP IAM
Identities in GCP can be categorized as follows:

- **Google Account / Cloud Identity**: Personal or corporate accounts associated with Google services.
- **Service Account**: A special type of account used by applications or VMs to interact with Google Cloud services.
- **Google Group**: A collection of Google accounts with shared permissions.
- **All Authenticated Users**: Any user who has signed in with a Google account.
- **All Users**: Any user on the internet, including unauthenticated users.

## IAM Roles
Roles define **what actions** an identity can perform on a resource.

### 1. Basic Roles (Legacy)
- **Viewer**: Read-only access.
- **Editor**: Read and write access.
- **Owner**: Full control, including managing permissions.

### 2. Predefined Roles
Google provides predefined roles with specific permissions tailored for different services.
Examples:
- **roles/storage.admin** → Full control over Cloud Storage.
- **roles/compute.instanceAdmin** → Admin access to Compute Engine instances.
- **roles/bigquery.dataViewer** → Read-only access to BigQuery data.

### 3. Custom Roles
- Created by administrators to provide **fine-grained access control**.
- Defined at the organization, folder, or project level.
- Allows **specific permissions** tailored to an organization’s needs.

## Resources in GCP IAM
IAM policies are applied at different **resource levels** in the GCP hierarchy:

1. **Organization** (Highest level) → Policies inherited by all projects.
2. **Folders** → Used to group projects, policies inherited from the organization.
3. **Projects** → Individual units for billing and resource management.
4. **Resources** → Specific GCP services (Compute Engine, Cloud Storage, etc.).

## Key Concepts
- **IAM Policy**: A collection of role bindings that define permissions for identities.
- **Principals**: The entities that can be assigned permissions (users, groups, service accounts).
- **Policy Inheritance**: IAM roles assigned at a higher level (e.g., organization) **propagate** down to lower levels (e.g., projects and resources).
- **Least Privilege Principle**: Grant only the necessary permissions to users or services.

---
### 📌 Best Practices
✅ Use **IAM conditions** to enforce context-aware access.
✅ Prefer **predefined roles** over basic roles for better security.
✅ Regularly **audit IAM policies** using `gcloud iam policies list`.
✅ Apply **the principle of least privilege** when assigning roles.
✅ Use **service accounts** instead of personal accounts for automation.


