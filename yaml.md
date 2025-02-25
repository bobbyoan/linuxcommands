---
title: yaml
description: 
published: true
date: 2025-02-25T07:14:19.039Z
tags: 
editor: markdown
dateCreated: 2025-02-25T07:14:17.604Z
---

# YAML

## Basics

### Key-Value Pairs
```yaml
name: John Doe
age: 30
city: New York
```

### Nested Structures
```yaml
person:
  name: John Doe
  age: 30
  address:
    city: New York
    country: USA
```

### Lists (Arrays)
```yaml
fruits:
  - Apple
  - Banana
  - Cherry
```

### Inline Lists
```yaml
fruits: [Apple, Banana, Cherry]
```



## Data Types

### Strings
```yaml
message: "Hello, World!"
multiline_message: |
  This is a multi-line string.
  It preserves new lines.
```

### Numbers
```yaml
integer: 42
float: 3.14
```

### Boolean
```yaml
is_admin: true
is_guest: false
```

### Null Values
```yaml
middle_name: null
nickname: ~
```



## Advanced YAML

### Aliases and Anchors
```yaml
defaults: &default_settings
  timeout: 30
  retries: 5

server1:
  <<: *default_settings
  host: server1.example.com

server2:
  <<: *default_settings
  host: server2.example.com
```

### Merging Lists
```yaml
base:
  - item1
  - item2

override:
  - item3
  - item4

combined:
  - <<: *base
  - <<: *override
```

### Environment Variables
```yaml
env_variable: ${HOME}
```

### Comments
```yaml
# This is a comment
key: value  # Inline comment
```



## YAML in Different Contexts

### Kubernetes Configuration
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
```

### Ansible Playbook
```yaml
- name: Install a package
  hosts: servers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

### Docker Compose
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

