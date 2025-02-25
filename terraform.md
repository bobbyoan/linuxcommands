---
title: terraform
description: 
published: true
date: 2025-02-25T07:14:54.687Z
tags: 
editor: markdown
dateCreated: 2025-02-25T07:11:24.008Z
---

# Terraform

## Installation

### Install Terraform
```sh
# Install on Ubuntu/Debian
sudo apt update && sudo apt install -y terraform

# Install on RHEL/CentOS
sudo dnf install -y terraform

# Install on macOS
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

### Verify Installation
```sh
terraform version
```



## Terraform Basics

### Initialize Terraform
```sh
terraform init
```

### Format Terraform Configuration
```sh
terraform fmt
```

### Validate Configuration
```sh
terraform validate
```

### Plan Infrastructure Changes
```sh
terraform plan
```

### Apply Changes
```sh
terraform apply
```

### Destroy Infrastructure
```sh
terraform destroy
```



## Terraform Configuration File (`.tf`)
```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```



## Terraform Proxmox Provider

### Install the Proxmox Provider
```hcl
terraform {
  required_providers {
    proxmox = {
      source  = "Telmate/proxmox"
      version = "2.9.11"
    }
  }
}
```

### Configure Proxmox Provider
```hcl
provider "proxmox" {
  pm_api_url      = "https://proxmox.example.com:8006/api2/json"
  pm_user         = "root@pam"
  pm_password     = "yourpassword"
  pm_tls_insecure = true
}
```

### Create a VM in Proxmox
```hcl
resource "proxmox_vm_qemu" "vm_example" {
  name        = "terraform-vm"
  target_node = "proxmox-node"
  clone       = "ubuntu-template"
  memory      = 2048
  cores       = 2
  sockets     = 1
  disk {
    size    = "20G"
    type    = "virtio"
    storage = "local-lvm"
  }
  network {
    model  = "virtio"
    bridge = "vmbr0"
  }
}
```

### Apply the Configuration
```sh
terraform init
terraform apply
```



## Terraform State Management

### View Current State
```sh
terraform show
```

### List Resources in State
```sh
terraform state list
```

### Remove a Resource from State (without destroying it)
```sh
terraform state rm <resource_name>
```

### Manually Import an Existing Resource
```sh
terraform import <resource_type>.<resource_name> <resource_id>
```



## Terraform Variables

### Define Variables
```hcl
variable "instance_type" {
  description = "Instance type for EC2"
  type        = string
  default     = "t2.micro"
}
```

### Use Variables
```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```

### Pass Variables via CLI
```sh
terraform apply -var "instance_type=t3.small"
```

### Variable Files (`.tfvars`)
```hcl
instance_type = "t3.micro"
```
Apply using a variable file:
```sh
terraform apply -var-file="variables.tfvars"
```



## Outputs

### Define Outputs
```hcl
output "instance_ip" {
  description = "Public IP of the instance"
  value       = aws_instance.example.public_ip
}
```

### View Outputs
```sh
terraform output
```



## Terraform Modules

### Create a Module
```sh
mkdir -p modules/ec2
```
Inside `modules/ec2/main.tf`:
```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```
Inside `modules/ec2/variables.tf`:
```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```
Inside `modules/ec2/outputs.tf`:
```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```

### Use a Module
```hcl
module "ec2" {
  source        = "./modules/ec2"
  instance_type = "t3.small"
}
```



## Terraform Debugging

### Enable Debug Logs
```sh
TF_LOG=DEBUG terraform apply
```

### Check Terraform Graph
```sh
terraform graph | dot -Tpng > graph.png
```


