# 📦 MPK Dev Cluster Pre-Requisites – Ansible Automation

This repository contains Ansible playbooks and roles to automate the setup of pre-requisites for onboarding nodes into the MPK management cluster.

---

## 📁 Directory Structure

```plaintext
.
├── group_vars/
│   └── all.yml                # Global variables applied to all hosts
├── inventory/                 # Inventory file(s) defining target hosts
├── roles/                    # Modular roles handling specific tasks
│   ├── apiserver-config/     # Configures kube-apiserver 
│   │   └── tasks/
│   │       ├── main.yml
│   │       ├── report.yml
│   │       └── setup.yml
│   ├── audit-logrotate/      # Manages log rotation policies
│   │   └── tasks/
│   │       ├── main.yml
│   │       ├── report.yml
│   │       └── setup.yml
│   ├── files/                # Shared files used across roles
│   │   ├── staged-audit-policy
│   │   ├── staged-encryption-provider
│   │   └── staged-sysctl
│   ├── final-report/         # Gathers final config reports
│   │   └── tasks/
│   │       ├── gather_config.yml
│   │       ├── main.yml
│   │       └── report.yml
│   ├── package-update/       # Handles package updates
│   │   └── tasks/
│   │       ├── main.yml
│   │       ├── report.yml
│   │       └── setup.yml
│   ├── resize-disk/          # Resizes disk partitions
│   │   └── tasks/
│   │       ├── main.yml
│   │       ├── report.yml
│   │       └── setup.yml
│   └── system-config/        # Configures system-level settings
│       └── tasks/
│           ├── main.yml
│           ├── report.yml
│           └── setup.yml
├── setup.yml                 # Main playbook to run all pre-req roles
└── README.md                 # This file
```

🚀 How to Use

1. Update Inventory
Add your target hosts under the inventory file.

2. Customize Variables
Update group_vars/all.yml with any global variables you want to use across roles.

3. Run the Playbook
```bash
ansible-playbook -i inventory setup.yml
```
✅ Make sure to run with sudo or a user with sufficient privileges if the playbook modifies system settings.

🧩 Role Breakdown

 * **system-config:** Applies system-level configurations (e.g., sysctl settings).
 * **resize-disk:** Ensures disk partitions are properly resized.
 * **package-update:** Updates system packages.
 * **audit-logrotate:** Configures log rotation policies.
 * **final-report:** Collects final configuration states for auditing.
 * **apiserver-config:** Applies API server audit and encryption policies.

Each role includes:

 * **setup.yml –** core tasks to apply the configuration
 * **report.yml –** gathers info or logs after setup
 * **main.yml –** includes both setup and report tasks

🏷️ Running Specific Roles

Use tags to run individual roles:
```bash
ansible-playbook -i inventory setup.yml --tags "resize-disk"
```

📬 Feedback

If you encounter issues or have suggestions, feel free to open an issue or contribute via pull request.
