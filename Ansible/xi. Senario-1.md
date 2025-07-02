# 🔄 Rolling Updates on GCP MIGs with Ansible, Terraform & Jenkins

---

## ✅ 1. Ansible Playbook: Create Custom Image

Save as `create_custom_image.yml`

```yaml
- name: Install App and Create Custom Image
  hosts: all
  become: true
  vars:
    app_url: "https://example.com/myapp.war"
    jboss_version: "7.4.0.Final"
    install_dir: "/opt/jboss"
    disk_name: "{{ ansible_hostname }}"
    zone: "us-central1-a"
    image_name: "jboss-app-{{ lookup('pipe', 'date +%Y%m%d%H%M') }}"
    project_id: "your-gcp-project-id"

  tasks:

    - name: Install Java
      apt:
        name: openjdk-11-jdk
        state: present
        update_cache: yes

    - name: Setup JBoss and deploy WAR
      block:
        - name: Create install dir
          file:
            path: "{{ install_dir }}"
            state: directory
            mode: '0755'

        - name: Download and extract JBoss
          unarchive:
            src: "https://download.jboss.org/wildfly/{{ jboss_version }}/wildfly-{{ jboss_version }}.tar.gz"
            dest: "{{ install_dir }}"
            remote_src: yes

        - name: Download WAR file
          get_url:
            url: "{{ app_url }}"
            dest: "{{ install_dir }}/wildfly-{{ jboss_version }}/standalone/deployments/myapp.war"

    - name: Create GCP custom image
      shell: |
        gcloud compute images create {{ image_name }} \
          --source-disk={{ disk_name }} \
          --source-disk-zone={{ zone }} \
          --family=jboss-app-family \
          --project={{ project_id }} \
          --quiet
      register: image_result

    - debug: var=image_result.stdout
```

---

## ✅ 2. Terraform Code: Rolling Update to MIG

Save as `main.tf`

```hcl
variable "image_family" {
  default = "jboss-app-family"
}

resource "google_compute_instance_template" "jboss_template" {
  name_prefix   = "jboss-template-"
  machine_type  = "e2-medium"
  region        = "us-central1"

  disk {
    source_image = data.google_compute_image.latest_custom.self_link
    auto_delete  = true
    boot         = true
  }

  network_interface {
    network = "default"
    access_config {}
  }

  metadata_startup_script = <<-EOT
    #!/bin/bash
    echo "Instance started with latest image"
  EOT
}

data "google_compute_image" "latest_custom" {
  family  = var.image_family
  project = "your-gcp-project-id"
}

resource "google_compute_region_instance_group_manager" "jboss_mig" {
  name               = "jboss-mig"
  region             = "us-central1"
  base_instance_name = "jboss"

  version {
    instance_template  = google_compute_instance_template.jboss_template.self_link
    name               = "jboss-v1"
  }

  target_size = 2

  update_policy {
    type                     = "ROLLING_UPDATE"
    minimal_action           = "REPLACE"
    max_surge_fixed          = 1
    max_unavailable_fixed    = 0
    min_ready_sec            = 60
  }
}
```

---

## ✅ 3. Jenkins Pipeline (Optional)

```groovy
pipeline {
  agent any

  environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }

  stages {
    stage('Build Custom Image with Ansible') {
      steps {
        sh 'ansible-playbook -i inventory.ini create_custom_image.yml'
      }
    }

    stage('Apply Terraform') {
      steps {
        dir('terraform') {
          sh 'terraform init'
          sh 'terraform apply -auto-approve'
        }
      }
    }
  }
}
```

---

## 🔁 How It Works

1. **Ansible** installs JBoss and app, then creates a new custom image.
2. Image is pushed to GCP under a common **image family**.
3. **Terraform** references latest image in the family and triggers a **rolling update**.
4. (Optional) **Jenkins** automates this end-to-end process.

---

