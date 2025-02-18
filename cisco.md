---
title: cisco
description: 
published: true
date: 2025-02-18T10:03:04.153Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:12.212Z
---

# Cisco Commands
## Configuration Commands 
### Basic Configuration
These are used in global configuration mode (configure terminal).
```bash
hostname <name>: Sets the hostname of the device.
enable secret <password>: Sets an encrypted enable password.
no ip domain-lookup: Disables DNS lookup to prevent accidental hostname resolution delays.
banner motd #<message>#: Configures a message of the day banner.
service password-encryption: Encrypts plain-text passwords in the configuration.
```

### Interface Configuration
```bash
interface <type> <number>: Accesses the interface (e.g., interface GigabitEthernet0/1).
ip address <IP> <subnet>: Assigns an IP address and subnet mask.
no shutdown: Enables the interface.
description <text>: Adds a description to the interface.
speed <value>: Sets the interface speed (10, 100, 1000 Mbps).
duplex <mode>: Sets the duplex mode (auto, full, half).
```

### Routing

```bash
ip route <network> <mask> <next-hop>: Configures a static route.
router ospf <process-id>: Enters OSPF configuration mode.
router eigrp <AS-number>: Enters EIGRP configuration mode.
network <network> <wildcard-mask>: Defines networks for a routing protocol.
VLAN
vlan <id>: Creates a VLAN.
name <vlan-name>: Assigns a name to the VLAN.
interface vlan <id>: Configures the VLAN interface.
```


## Show Commands
Used for troubleshooting and monitoring.

```bash
show running-config: Displays the current configuration.
show startup-config: Displays the configuration saved in NVRAM.
show version: Displays IOS version, hardware details, and uptime.
show ip interface brief: Summarizes IP addresses and interface status.
show interfaces: Provides detailed interface statistics.
show vlan brief: Displays VLAN information.
show mac address-table: Displays the MAC address table.
show ip route: Displays the routing table.
show protocols: Displays the status of network layer protocols.
```

## Debug Commands
These commands enable real-time troubleshooting.

```bash
debug ip ospf events: Monitors OSPF events.
debug ip eigrp: Monitors EIGRP operations.
debug ip packet: Monitors IP packet activity (use with caution).
undebug all or no debug all: Turns off all debugging.
```

## Privileged EXEC Mode Commands
Available after entering enable mode.

```bash
reload: Reboots the device.
copy running-config startup-config: Saves the running configuration to NVRAM.
erase startup-config: Erases the saved configuration in NVRAM.
write memory: Saves the current configuration (alternative to copy).
ping <IP>: Sends an ICMP echo to test connectivity.
traceroute <IP>: Traces the route to a destination.
```

## Access Control Commands
For configuring access control lists (ACLs).

```bash
access-list <number> permit/deny <conditions>: Configures a standard ACL.
ip access-list standard/extended <name>: Configures a named ACL.
ip access-group <ACL-number/name> in/out: Applies an ACL to an interface.
show access-lists: Displays configured ACLs.
```

## Security Commands
For enhancing device security.

```bash
line vty <start> <end>: Configures remote access lines.
password <password>: Sets a password for a line.
login: Enables password checking on a line.
service ssh: Enables SSH service.
crypto key generate rsa: Generates an RSA key pair for SSH.
```

## Switching-Specific Commands
For Layer 2 configurations.

```bash
spanning-tree mode <mode>: Configures spanning-tree mode (e.g., PVST, RSTP).
spanning-tree vlan <id> root primary: Configures the switch as the root bridge.
switchport mode access: Sets the interface as an access port.
switchport mode trunk: Configures the interface as a trunk.
switchport access vlan <id>: Assigns a VLAN to an access port.
show spanning-tree: Displays spanning-tree details.
```

## QoS Commands
For quality of service.

```bash
mls qos: Enables QoS globally on the switch.
class-map <name>: Defines a class of traffic.
policy-map <name>: Defines a QoS policy.
service-policy <policy>: Applies a QoS policy to an interface.
```

## NAT Commands
For configuring Network Address Translation.

```bash
ip nat inside: Configures an interface for inside NAT.
ip nat outside: Configures an interface for outside NAT.
ip nat pool <name> <start-IP> <end-IP> netmask <mask>: Creates a NAT pool.
ip nat inside source list <number> pool <name>: Maps a NAT pool to ACL traffic.
show ip nat translations: Displays NAT translations.
```

## Logging and Monitoring

```bash
logging console: Enables console logging.
logging buffered <size>: Configures the logging buffer size.
logging <IP>: Sends logs to a syslog server.
show logging: Displays log messages.
```