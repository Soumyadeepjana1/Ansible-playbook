# 🚀 Ansible Automation & DevOps Lab

<div align="center">

### ⚙️ Infrastructure Automation • Configuration Management • DevOps

[![Ansible](https://img.shields.io/badge/Ansible-Automation-black?style=for-the-badge\&logo=ansible\&logoColor=white)](https://www.ansible.com/)
[![Linux](https://img.shields.io/badge/Linux-Ubuntu-orange?style=for-the-badge\&logo=ubuntu\&logoColor=white)](https://ubuntu.com/)
[![YAML](https://img.shields.io/badge/YAML-Configuration-red?style=for-the-badge\&logo=yaml\&logoColor=white)](https://yaml.org/)
[![Git](https://img.shields.io/badge/Git-Version_Control-black?style=for-the-badge\&logo=git\&logoColor=white)](https://git-scm.com/)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?style=for-the-badge\&logo=github)](https://github.com/)

**A practical Ansible automation repository for learning, experimenting, and building production-style DevOps automation.**

</div>

---

## 📌 Overview

This repository contains **Ansible playbooks, inventories, roles, variables, handlers, templates, and automation experiments** designed to build strong practical knowledge of Ansible and Infrastructure as Code.

The repository progresses from:

```text
Basic YAML
    ↓
Ansible Ad-Hoc Commands
    ↓
Inventory Management
    ↓
Playbooks
    ↓
Variables & Facts
    ↓
Handlers
    ↓
Templates
    ↓
Roles
    ↓
Secrets Management
    ↓
Multi-Server Automation
    ↓
CI/CD Integration
```

---

# 🏗️ Architecture

```text
                         ┌───────────────────────┐
                         │       Developer       │
                         │      Git / GitHub     │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │   Ansible Controller  │
                         │                       │
                         │  Playbooks            │
                         │  Inventory            │
                         │  Variables            │
                         │  Roles                │
                         │  Templates            │
                         └───────────┬───────────┘
                                     │
                    ┌────────────────┼────────────────┐
                    │                │                │
                    ▼                ▼                ▼
              ┌──────────┐    ┌──────────┐    ┌──────────┐
              │ Web Node │    │ App Node │    │ DB Node  │
              │  Nginx   │    │  App     │    │ Database │
              └──────────┘    └──────────┘    └──────────┘
                    │                │                │
                    └────────────────┼────────────────┘
                                     ▼
                           Automated Infrastructure
```

### 🔄 Automation Flow

```text
Developer
   │
   ▼
Git Push
   │
   ▼
Ansible Repository
   │
   ▼
Inventory
   │
   ▼
Playbook
   │
   ▼
Tasks
   │
   ├── Install Packages
   ├── Configure Services
   ├── Create Users
   ├── Manage Files
   ├── Deploy Applications
   └── Restart Services
   │
   ▼
Target Servers
```

---

# 🎯 Objectives

The main objectives of this repository are:

* 🐧 Linux server automation
* ⚙️ Configuration management
* 📦 Package installation
* 👤 User and permission management
* 🌐 Web-server deployment
* 🔐 Secure infrastructure configuration
* 📄 Configuration templating
* 🔄 Service management
* 🧩 Role-based automation
* ☁️ Cloud infrastructure automation
* 🔁 CI/CD integration
* 📊 Monitoring automation

---

# 🛠️ Technology Stack

| Technology | Purpose                               |
| ---------- | ------------------------------------- |
| Ansible    | Automation & configuration management |
| YAML       | Playbook configuration                |
| Linux      | Target operating system               |
| SSH        | Remote server communication           |
| Git        | Version control                       |
| GitHub     | Source-code management                |
| Nginx      | Web server                            |
| Docker     | Container automation                  |
| AWS        | Cloud infrastructure                  |
| Jenkins    | CI/CD automation                      |
| Terraform  | Infrastructure provisioning           |

---

# 📂 Project Structure

```text
ansible/
│
├── inventory/
│   ├── hosts
│   └── production
│
├── playbooks/
│   ├── install_nginx.yml
│   ├── system_info.yml
│   ├── users.yml
│   ├── packages.yml
│   └── deploy.yml
│
├── roles/
│   ├── nginx/
│   │   ├── tasks/
│   │   ├── handlers/
│   │   ├── templates/
│   │   ├── files/
│   │   ├── vars/
│   │   └── defaults/
│   │
│   └── application/
│
├── group_vars/
│   ├── all.yml
│   └── web.yml
│
├── host_vars/
│
├── templates/
│
├── files/
│
├── handlers/
│
├── ansible.cfg
├── requirements.yml
└── README.md
```

---

# ⚡ Installation

### Install Ansible

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install ansible -y
```

Verify:

```bash
ansible --version
```

Example:

```text
ansible [core 2.x.x]
python version = 3.x
```

---

# 🔑 SSH Configuration

Ansible normally communicates with Linux machines using SSH.

Generate an SSH key:

```bash
ssh-keygen
```

Copy the key:

```bash
ssh-copy-id user@SERVER_IP
```

Test the connection:

```bash
ssh user@SERVER_IP
```

---

# 📋 Inventory

Example inventory:

```ini
[web]
web01 ansible_host=192.168.1.10
web02 ansible_host=192.168.1.11

[app]
app01 ansible_host=192.168.1.20

[database]
db01 ansible_host=192.168.1.30

[production:children]
web
app
database
```

Test connectivity:

```bash
ansible all -i inventory/hosts -m ping
```

Expected:

```text
web01 | SUCCESS => {
    "ping": "pong"
}
```

---

# 🧪 Ansible Ad-Hoc Commands

### Ping servers

```bash
ansible all -m ping
```

### Check uptime

```bash
ansible all -m command -a "uptime"
```

### Check memory

```bash
ansible all -m shell -a "free -h"
```

### Check disk

```bash
ansible all -m shell -a "df -h"
```

### Install Git

```bash
ansible all -b -m apt -a "name=git state=present"
```

---

# 📜 Playbook Example

```yaml
---
- name: Install and configure Nginx
  hosts: web
  become: true

  tasks:

    - name: Update apt cache
      apt:
        update_cache: true

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: true
```

Run:

```bash
ansible-playbook -i inventory/hosts playbooks/install_nginx.yml
```

---

# 🧠 Important Ansible Concepts

```text
                    ANSIBLE
                       │
       ┌───────────────┼────────────────┐
       │               │                │
   Inventory        Playbook          Modules
       │               │                │
    Servers          Tasks          apt/service
       │               │                │
       └───────────────┼────────────────┘
                       │
                  Variables
                       │
                   Templates
                       │
                    Handlers
                       │
                     Roles
                       │
                 Automation
```

---

# 📦 Modules

Some commonly used modules:

| Module      | Purpose                   |
| ----------- | ------------------------- |
| `apt`       | Package management        |
| `yum`       | RPM package management    |
| `copy`      | Copy files                |
| `file`      | File/directory management |
| `service`   | Service management        |
| `systemd`   | Systemd services          |
| `user`      | User management           |
| `group`     | Group management          |
| `command`   | Execute commands          |
| `shell`     | Execute shell commands    |
| `debug`     | Display information       |
| `template`  | Jinja2 templates          |
| `git`       | Git repository management |
| `uri`       | HTTP/API requests         |
| `unarchive` | Extract archives          |

---

# 🔄 Variables

Example:

```yaml
---
- name: Variable demonstration
  hosts: web

  vars:
    package_name: nginx
    service_name: nginx

  tasks:

    - name: Install package
      become: true
      apt:
        name: "{{ package_name }}"
        state: present

    - name: Start service
      become: true
      service:
        name: "{{ service_name }}"
        state: started
```

Run:

```bash
ansible-playbook playbook.yml
```

Override a variable:

```bash
ansible-playbook playbook.yml -e "package_name=git"
```

---

# 🔔 Handlers

Handlers are triggered only when a task reports a change.

```yaml
tasks:

  - name: Update Nginx configuration
    template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
    notify:
      - Restart Nginx

handlers:

  - name: Restart Nginx
    service:
      name: nginx
      state: restarted
```

Flow:

```text
Task
 │
 ├── Changed?
 │
 ├── NO ───────► Nothing
 │
 └── YES
      │
      ▼
   Handler
      │
      ▼
Restart Service
```

---

# 🎨 Jinja2 Templates

Example:

```jinja2
server {
    listen {{ nginx_port }};

    server_name {{ server_name }};

    root {{ web_root }};
}
```

Variables:

```yaml
vars:
  nginx_port: 80
  server_name: example.com
  web_root: /var/www/html
```

This allows one template to configure multiple environments.

---

# 🧩 Ansible Roles

Roles provide a scalable project architecture.

```text
roles/
└── nginx/
    │
    ├── defaults/
    │   └── main.yml
    │
    ├── vars/
    │   └── main.yml
    │
    ├── tasks/
    │   └── main.yml
    │
    ├── handlers/
    │   └── main.yml
    │
    ├── templates/
    │   └── nginx.conf.j2
    │
    ├── files/
    │
    └── meta/
        └── main.yml
```

Use a role:

```yaml
---
- name: Configure Web Servers
  hosts: web

  roles:
    - nginx
```

---

# 🔐 Privilege Escalation

Use:

```yaml
become: true
```

Example:

```yaml
- name: Install package
  apt:
    name: nginx
    state: present
  become: true
```

Run with password prompt:

```bash
ansible-playbook playbook.yml --ask-become-pass
```

---

# 🔒 Ansible Vault

Never store passwords or secrets directly inside Git.

Create encrypted variables:

```bash
ansible-vault create secrets.yml
```

Edit:

```bash
ansible-vault edit secrets.yml
```

Run:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

Encrypt an existing file:

```bash
ansible-vault encrypt secrets.yml
```

Decrypt:

```bash
ansible-vault decrypt secrets.yml
```

---

# 🌍 Environment Strategy

A production-style structure:

```text
environments/
│
├── development/
│   ├── inventory
│   └── group_vars/
│
├── staging/
│   ├── inventory
│   └── group_vars/
│
└── production/
    ├── inventory
    └── group_vars/
```

Deployment:

```text
                    Git
                     │
                     ▼
              ┌─────────────┐
              │ Development │
              └──────┬──────┘
                     │
                     ▼
                ┌─────────┐
                │ Staging │
                └────┬────┘
                     │
                     ▼
               ┌────────────┐
               │ Production │
               └────────────┘
```

---

# 🚀 Production Automation Workflow

```text
                    Developer
                        │
                        ▼
                   Git Commit
                        │
                        ▼
                  GitHub Repository
                        │
                        ▼
                    CI Pipeline
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
          YAML Lint          Ansible Lint
              │                   │
              └─────────┬─────────┘
                        ▼
                  Syntax Check
                        │
                        ▼
                  Ansible Playbook
                        │
                        ▼
                 Target Infrastructure
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
       Web Server    App Server    Database
```

---

# 🧪 Testing

Check playbook syntax:

```bash
ansible-playbook --syntax-check playbook.yml
```

Perform a dry run:

```bash
ansible-playbook playbook.yml --check
```

Show differences:

```bash
ansible-playbook playbook.yml --check --diff
```

Verbose execution:

```bash
ansible-playbook playbook.yml -vv
```

More verbose:

```bash
ansible-playbook playbook.yml -vvv
```

---

# 📊 Ansible Facts

View facts:

```bash
ansible localhost -m setup
```

Useful variables:

```yaml
{{ ansible_hostname }}
{{ ansible_distribution }}
{{ ansible_os_family }}
{{ ansible_architecture }}
{{ ansible_default_ipv4.address }}
```

Example:

```yaml
- name: Display server information
  debug:
    msg:
      - "Hostname: {{ ansible_hostname }}"
      - "OS: {{ ansible_distribution }}"
      - "IP: {{ ansible_default_ipv4.address }}"
```

---

# ⚡ Idempotency

One of Ansible's most important concepts.

```text
First Run
    │
    ▼
Changes Required
    │
    ▼
Configuration Applied
    │
    ▼
Second Run
    │
    ▼
No Changes
```

Example:

```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present
```

Running the playbook multiple times should not repeatedly modify the system unnecessarily.

---

# 🛡️ Ansible Best Practices

### ✅ Use meaningful names

```yaml
- name: Install Nginx web server
```

Instead of:

```yaml
- name: task1
```

### ✅ Prefer modules over shell

Prefer:

```yaml
apt:
  name: git
  state: present
```

Instead of:

```yaml
shell: apt install git -y
```

### ✅ Use variables

```yaml
name: "{{ package_name }}"
```

### ✅ Use handlers for service restarts

```yaml
notify:
  - Restart Nginx
```

### ✅ Keep secrets encrypted

```text
Ansible Vault
     ↓
Encrypted Secrets
     ↓
Git Repository
```

### ✅ Use roles for large projects

```text
Playbook
   ↓
Roles
   ↓
Reusable Automation
```

---

# 🧰 Useful Commands

### List inventory

```bash
ansible-inventory --list
```

### Graph inventory

```bash
ansible-inventory --graph
```

### Test connection

```bash
ansible all -m ping
```

### Run playbook

```bash
ansible-playbook -i inventory/hosts playbook.yml
```

### Check syntax

```bash
ansible-playbook --syntax-check playbook.yml
```

### Dry run

```bash
ansible-playbook playbook.yml --check
```

### List tasks

```bash
ansible-playbook playbook.yml --list-tasks
```

### List hosts

```bash
ansible-playbook playbook.yml --list-hosts
```

---

# 🔧 Configuration

Example `ansible.cfg`:

```ini
[defaults]

inventory = ./inventory/hosts
remote_user = ubuntu
host_key_checking = False
retry_files_enabled = False
interpreter_python = auto_silent

[privilege_escalation]

become = True
become_method = sudo
become_ask_pass = False
```

---

# ☁️ Cloud Automation

Ansible can automate cloud environments such as:

```text
             Ansible
                 │
       ┌─────────┼─────────┐
       │         │         │
       ▼         ▼         ▼
      AWS      Azure      GCP
       │         │         │
       ▼         ▼         ▼
     EC2       VM       Compute
       │
       ▼
   Applications
```

Typical workflow:

```text
Terraform
    │
    ▼
Provision Infrastructure
    │
    ▼
AWS EC2
    │
    ▼
Ansible
    │
    ▼
Configure Server
    │
    ▼
Deploy Application
```

---

# 🔗 DevOps Integration

This repository can be extended into a complete DevOps pipeline:

```text
GitHub
   │
   ▼
GitHub Actions / Jenkins
   │
   ├── YAML Validation
   ├── Ansible Lint
   ├── Security Scan
   └── Automated Tests
   │
   ▼
Ansible
   │
   ▼
Docker / AWS / Kubernetes
   │
   ▼
Monitoring
   │
   ├── Prometheus
   └── Grafana
```

---

# 📈 Learning Roadmap

```text
LEVEL 01
Linux + SSH
     ↓
LEVEL 02
YAML
     ↓
LEVEL 03
Ad-Hoc Commands
     ↓
LEVEL 04
Inventory
     ↓
LEVEL 05
Playbooks
     ↓
LEVEL 06
Variables + Facts
     ↓
LEVEL 07
Conditionals + Loops
     ↓
LEVEL 08
Handlers + Templates
     ↓
LEVEL 09
Roles
     ↓
LEVEL 10
Ansible Vault
     ↓
LEVEL 11
AWS Automation
     ↓
LEVEL 12
CI/CD Integration
     ↓
LEVEL 13
Production Automation
```

---

# 🏆 Skills Demonstrated

This repository demonstrates practical knowledge of:

* [x] YAML
* [x] Linux
* [x] SSH
* [x] Ansible Inventory
* [x] Ad-Hoc Commands
* [x] Playbooks
* [x] Modules
* [x] Variables
* [x] Facts
* [x] Conditionals
* [x] Loops
* [x] Handlers
* [x] Templates
* [x] Jinja2
* [x] Roles
* [x] Ansible Vault
* [x] Idempotency
* [x] Privilege Escalation
* [x] AWS Automation
* [x] CI/CD Integration

---

# 💻 Example Project

### Automated Nginx Deployment

```text
GitHub
   │
   ▼
Ansible Controller
   │
   ▼
Inventory
   │
   ▼
Nginx Playbook
   │
   ├── Update Packages
   ├── Install Nginx
   ├── Configure Nginx
   ├── Copy Website
   ├── Enable Service
   └── Restart Nginx
   │
   ▼
Web Server
   │
   ▼
🌐 Application Online
```

---

# 🐛 Troubleshooting

### SSH connection failure

```bash
ansible all -m ping -vvv
```

Check:

```bash
ssh user@SERVER_IP
```

### Permission denied

Use:

```bash
--ask-become-pass
```

or configure appropriate sudo permissions.

### Check inventory

```bash
ansible-inventory --graph
```

### Check playbook syntax

```bash
ansible-playbook --syntax-check playbook.yml
```

### Debug variables

```yaml
- name: Debug variable
  debug:
    var: variable_name
```

---

# 📚 Official Documentation

* Ansible Documentation — https://docs.ansible.com/
* Ansible Community — https://forum.ansible.com/
* YAML Specification — https://yaml.org/spec/
* Jinja Documentation — https://jinja.palletsprojects.com/

---

# 👨‍💻 Author

**Soumyadeep Jana**

MCA — Cloud Computing & DevOps

Focused on:

```text
Cloud ☁️
DevOps ⚙️
Linux 🐧
Automation 🤖
AWS 🚀
Kubernetes ☸️
Infrastructure as Code 🏗️
```

---

<div align="center">

### ⭐ If you find this repository useful, consider giving it a star!

**Automate Everything. Deploy Faster. Build Better. 🚀**

</div>
