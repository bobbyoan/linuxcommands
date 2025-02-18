---
title: forti
description: 
published: true
date: 2025-02-18T09:48:27.276Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:16.426Z
---

# Fortigate Commands

## General System Settings

```bash
get system status                       # Displays the system status, firmware version, and device information
config system global                     # Configures global system settings
set hostname <hostname>                   # Sets hostname
set timezone <timezone>                    # Sets timezone
execute reboot                            # Reboots the FortiGate device
execute shutdown                          # Shuts down the FortiGate device
```

## Interface Configuration

```bash
config system interface                   # Configures network interfaces
edit port1
set ip 192.168.1.1 255.255.255.0          # Sets IP address and subnet mask
set allowaccess ping https ssh            # Sets allowed access methods
set mode static                           # Sets interface mode to static
get system interface                      # Displays interface details
```

## Firewall Configuration

```bash
config firewall policy                     # Configures firewall policies
edit 1
set name "Allow-Web-Traffic"               # Sets policy name
set srcintf "port1"                        # Sets source interface
set dstintf "port2"                        # Sets destination interface
set srcaddr "all"                          # Sets source address
set dstaddr "all"                          # Sets destination address
set action accept                          # Sets action to accept traffic
set schedule "always"                      # Sets schedule
set service "HTTP"                         # Defines allowed service
set logtraffic all                         # Enables logging for all traffic
show firewall policy                       # Displays configured firewall policies
```

## Routing Configuration

```bash
config router static                        # Configures static routes
edit 1
set gateway 192.168.1.254                   # Sets the gateway
set device "port1"                          # Sets the interface for routing
set dst 0.0.0.0 0.0.0.0                     # Configures default route
get router info routing-table all          # Displays the current routing table
```

## User and Authentication

```bash
config user local                          # Creates local user accounts
edit "admin"
set type password                          # Sets account type as password-based
set passwd "securepassword"                # Sets user password
get user local                             # Displays local user account information
```


## VPN Configuration

```bash
config vpn ipsec phase1-interface           # Configures Phase 1 of IPsec VPN
edit "VPN1"
set interface "port1"                       # Sets the interface for the VPN
set proposal aes256-sha1                    # Sets encryption and authentication methods
set remote-gw 192.168.2.1                   # Sets remote gateway IP
set psksecret "vpnpassword"                 # Sets pre-shared key
config vpn ipsec phase2-interface           # Configures Phase 2 of IPsec VPN
edit "VPN1"
set phase1name "VPN1"                       # Associates with Phase 1
set proposal aes256-sha1                    # Sets encryption and authentication methods
set src-subnet 192.168.1.0 255.255.255.0    # Defines source subnet
set dst-subnet 192.168.2.0 255.255.255.0    # Defines destination subnet
get vpn ipsec tunnel summary               # Displays the status of IPsec tunnels
```

## Logging and Monitoring

```bash
execute log filter category "traffic"       # Filters logs by category
execute log display                         # Displays filtered logs
get system session list                     # Displays the list of active sessions
```

## Troubleshooting Commands

```bash
execute ping 8.8.8.8                        # Sends an ICMP echo request to test connectivity
execute traceroute 8.8.8.8                   # Traces the route to a destination
diagnose debug enable                       # Enables debugging mode
diagnose debug console timestamp enable     # Adds timestamps to debug output
```

## Backup and Restore

```bash
execute backup config tftp 192.168.1.10 config_backup.conf  # Backs up the configuration file
execute restore config tftp 192.168.1.10 config_backup.conf  # Restores the configuration file
```

## High Availability (HA)

```bash
config system ha                            # Configures HA settings
set mode a-p                                # Sets HA mode to Active-Passive
set group-name "MyHAGroup"                  # Sets HA group name
set password "hapassword"                    # Sets HA group password
set priority 200                            # Sets HA priority
set monitor "port1"                         # Monitors interface for HA
get system ha status                        # Displays the HA status
```