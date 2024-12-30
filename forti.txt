### 1. General System Commands

# Displays the system status, firmware version, and device information.
get system status

# Configures global system settings.
config system global
set hostname MyFortiGate
set timezone 04
end

# Reboots the FortiGate device.
execute reboot

# Shuts down the FortiGate device.
execute shutdown

### 2. Interface Configuration

# Configures network interfaces.
config system interface
edit port1
set ip 192.168.1.1 255.255.255.0
set allowaccess ping https ssh
set mode static
end

# Displays interface details.
get system interface

### 3. Firewall Configuration

# Configures firewall policies.
config firewall policy
edit 1
set name "Allow-Web-Traffic"
set srcintf "port1"
set dstintf "port2"
set srcaddr "all"
set dstaddr "all"
set action accept
set schedule "always"
set service "HTTP"
set logtraffic all
end

# Displays the configured firewall policies.
show firewall policy

### 4. Routing Configuration

# Configures static routes.
config router static
edit 1
set gateway 192.168.1.254
set device "port1"
set dst 0.0.0.0 0.0.0.0
end

# Displays the current routing table.
get router info routing-table all

### 5. User and Authentication

# Creates local user accounts.
config user local
edit "admin"
set type password
set passwd "securepassword"
end

# Displays local user account information.
get user local

### 6. VPN Configuration

# Configures Phase 1 of IPsec VPN.
config vpn ipsec phase1-interface
edit "VPN1"
set interface "port1"
set proposal aes256-sha1
set remote-gw 192.168.2.1
set psksecret "vpnpassword"
end

# Configures Phase 2 of IPsec VPN.
config vpn ipsec phase2-interface
edit "VPN1"
set phase1name "VPN1"
set proposal aes256-sha1
set src-subnet 192.168.1.0 255.255.255.0
set dst-subnet 192.168.2.0 255.255.255.0
end

# Displays the status of IPsec tunnels.
get vpn ipsec tunnel summary

### 7. Logging and Monitoring

# Filters logs by category.
execute log filter category "traffic"

# Displays filtered logs.
execute log display

# Displays the list of active sessions.
get system session list

### 8. Troubleshooting Commands

# Sends an ICMP echo request to test connectivity.
execute ping 8.8.8.8

# Traces the route to a destination.
execute traceroute 8.8.8.8

# Enables debugging mode.
diagnose debug enable

# Adds timestamps to debug output.
diagnose debug console timestamp enable

### 9. Backup and Restore

# Backs up the configuration file.
execute backup config tftp 192.168.1.10 config_backup.conf

# Restores the configuration file.
execute restore config tftp 192.168.1.10 config_backup.conf

### 10. High Availability (HA)

# Configures HA settings.
config system ha
set mode a-p
set group-name "MyHAGroup"
set password "hapassword"
set priority 200
set monitor "port1"
end

# Displays the HA status.
get system ha status
