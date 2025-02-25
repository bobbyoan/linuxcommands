---
title: ansible
description: 
published: true
date: 2025-02-25T07:04:24.711Z
tags: 
editor: markdown
dateCreated: 2025-02-25T07:00:46.510Z
---

# Ansible

## Installation

### Install Ansible
```sh
# Install Ansible on Ubuntu/Debian
sudo apt update && sudo apt install -y ansible

# Install Ansible on RHEL/CentOS
sudo dnf install -y ansible

# Install Ansible on macOS
brew install ansible
```

### Verify Installation
```sh
ansible --version
```



## Configuration
- Default config file: `/etc/ansible/ansible.cfg`
- Custom config: Set `ANSIBLE_CONFIG=/path/to/ansible.cfg`
- Modify default inventory file: `/etc/ansible/hosts`



## Inventory File

Inventory files define target hosts for Ansible commands.
```ini
# Example inventory file: /etc/ansible/hosts
[webservers]
web01 ansible_host=192.168.1.10 ansible_user=root
web02 ansible_host=192.168.1.11 ansible_user=root

[dbservers]
db01 ansible_host=192.168.1.20 ansible_user=root
```

Use a custom inventory file:
```sh
ansible all -m ping -i inventory.ini
```



## Running Ad-Hoc Commands

Execute quick commands without writing a playbook.
```sh
# Check connectivity
ansible all -m ping

# Run a command on all hosts
ansible all -m command -a "uptime"

# Check disk usage
ansible all -m shell -a "df -h"

# Get system information
ansible all -m setup
```



## Playbooks

### Writing Playbooks
Playbooks define Ansible automation workflows.
```yaml
- name: Install Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```
Run the playbook:
```sh
ansible-playbook site.yml -i inventory.ini
```



## Variables in Ansible
```yaml
- name: Example with Variables
  hosts: webservers
  vars:
    package_name: nginx
  tasks:
    - name: Install package
      apt:
        name: "{{ package_name }}"
        state: present
```



## Handlers
Handlers allow actions to execute only when notified.
```yaml
- name: Restart Nginx when needed
  hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      notify: Restart Nginx
  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
```



## Loops
Run a task multiple times with different values.
```yaml
- name: Install multiple packages
  hosts: webservers
  tasks:
    - name: Install packages
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - nginx
        - curl
        - git
```



## Conditionals
```yaml
- name: Install Apache only on Ubuntu
  hosts: webservers
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
      when: ansible_facts['os_family'] == 'Debian'
```



## Roles
```sh
# Create a new role
ansible-galaxy init myrole
```

Using a role in a playbook:
```yaml
- hosts: webservers
  roles:
    - myrole
```



## Ansible Vault (Encrypt Sensitive Data)
```sh
# Create an encrypted file
ansible-vault create secrets.yml

# Edit an encrypted file
ansible-vault edit secrets.yml

# Run a playbook using Vault
ansible-playbook site.yml --ask-vault-pass
```



## Debugging & Dry Run
```sh
# Dry run (Check what would be changed)
ansible-playbook site.yml --check

# Show debug output
ansible-playbook site.yml -vvv
```



## Facts
Gather system facts for decision-making.
```sh
ansible all -m setup | less
```



## Tags (Run Specific Tasks in a Playbook)
```yaml
- name: Install packages
  hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
      tags: nginx

    - name: Install MySQL
      apt:
        name: mysql-server
        state: present
      tags: mysql
```
Run only the Nginx task:
```sh
ansible-playbook site.yml --tags nginx
```



## Common Modules
```yaml
- name: Copy a file
  copy:
    src: /local/file
    dest: /remote/path

- name: Download a file
  get_url:
    url: https://example.com/file
    dest: /remote/path

- name: Create a user
  user:
    name: johndoe
    state: present

- name: Manage a service
  service:
    name: nginx
    state: started
```

## Troubleshooting
```sh
# Test connection to hosts
ansible all -m ping

# Run a task with debug output
ansible-playbook site.yml -vvv

# Check syntax before running
ansible-playbook site.yml --syntax-check
```

