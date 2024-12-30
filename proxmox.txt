# Complete List of Proxmox CLI Commands

## General Commands
```bash
# Login to Proxmox CLI
pveum login

# Display Proxmox version
pveversion

# Display detailed version information
pveversion --verbose

# Check system performance
pveperf

# Restart Proxmox services
systemctl restart pveproxy pvedaemon

# Check Proxmox license information
pveproxy --version
```

## Node Management
```bash
# List all nodes in the cluster
pvecm nodes

# Add a new node to the cluster
pvecm add <IP_of_existing_node>

# Remove a node from the cluster
pvecm delnode <node_name>

# Forcefully remove a node from the cluster
pvecm delnode --force <node_name>

# Show cluster status
pvecm status

# Synchronize cluster configuration
pvecm updatecerts
```

## Virtual Machine (VM) Management
```bash
# List all VMs
qm list

# Start a VM
qm start <vmid>

# Stop a VM
qm stop <vmid>

# Shutdown a VM gracefully
qm shutdown <vmid>

# Create a new VM
qm create <vmid> --name <vm_name> --memory <size> --net0 virtio,bridge=vmbr0

# Delete a VM
qm destroy <vmid>

# Clone a VM
qm clone <source_vmid> <target_vmid> --name <new_vm_name>

# Import a VM disk image
qm importdisk <vmid> <image_file> <storage>

# Resize a VM disk
qm resize <vmid> scsi0 <size>

# Show VM configuration
qm config <vmid>

# Set VM options
qm set <vmid> --<option>=<value>

# Remove VM options
qm unset <vmid> --<option>
```

## Container Management
```bash
# List all containers
pct list

# Start a container
pct start <ctid>

# Stop a container
pct stop <ctid>

# Create a new container
pct create <ctid> <template_path> --storage <storage_name> --hostname <hostname>

# Destroy a container
pct destroy <ctid>

# Resize container disk
pct resize <ctid> rootfs <size>

# Show container configuration
pct config <ctid>

# Set container options
pct set <ctid> --<option>=<value>

# Unset container options
pct unset <ctid> --<option>
```

## Storage Management
```bash
# List storage pools
pvesm status

# Add new storage
pvesm add <type> <storage_name> --path <path>

# Remove storage
pvesm remove <storage_name>

# Resize a logical volume
lvresize -L +<size> <volume_path>

# Extend storage
pvesm resize <storage_name> <size>
```

## Backup and Restore
```bash
# List backup files
vzdump --list

# Backup a VM
vzdump <vmid> --dumpdir <path>

# Restore a VM from backup
qmrestore <backup_file> <vmid>

# Backup a container
vzdump <ctid> --dumpdir <path>

# Restore a container from backup
pct restore <ctid> <backup_file>
```

## Networking
```bash
# List network interfaces
ip a

# Restart network services
systemctl restart networking

# Check bridge configuration
cat /etc/network/interfaces

# Apply network configuration changes
ifreload -a
```

## Logs and Troubleshooting
```bash
# View Proxmox logs
journalctl -u pvedaemon

# Check task logs
cat /var/log/pve/tasks/<date>.log

# View system logs
journalctl -f

# Check VM-specific logs
qm showcmd <vmid>

# Check system resource usage
top
htop

# Check disk usage
df -h

# Monitor cluster logs
pvecm log

# Check system uptime
uptime
```

## User and Permission Management
```bash
# List users
pveum user list

# Add a user
pveum user add <user>@<realm> --password <password>

# Remove a user
pveum user delete <user>@<realm>

# List roles
pveum role list

# Add a role
pveum role add <role_name> --privs <privilege_list>

# Assign a role to a user
pveum aclmod / --roles <role_name> --users <user>@<realm>

# Remove a role from a user
pveum acldel / --users <user>@<realm> --roles <role_name>
```

## Advanced Operations
```bash
# Migrate a VM to another node
qm migrate <vmid> <target_node>

# Enable high availability (HA) for a VM or container
ha-manager add <type>:<id>

# Disable high availability (HA) for a VM or container
ha-manager remove <type>:<id>

# Check HA status
ha-manager status

# Reboot a node
reboot

# Shutdown a node
shutdown now
```

