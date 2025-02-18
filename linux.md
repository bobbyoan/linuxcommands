---
title: linux
description: 
published: true
date: 2025-02-18T11:38:27.965Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:21.990Z
---


# Linux Commands

## Fundamentals

```bash
cd - change directory
ls - list content
pwd - print working directory
touch - creates a new file
clear - clears the screen
exit - exits out of the shell
script [logname] - saves all your shell activity in a log file
history - shows commands that were executed; -c clears history
cp - copies a file / directory
cp -rv [path]/* [destination_path]/ - copies content of a folder in another folder
vi - opens Vi text editor; also creates a new file
rm - removes a file
rm -r - removes a directory
rmdir - removes a directory
mv - moves a file / renames a file
mkdir - creates a new directory
find - finds files in filesystem
locate - locates files in filesystem using a database of stored locations (It is a best practice to execute updatedb before running this command)
updatedb - updates the db where locate stores the file locations
ln - hard link (creates a "shortcut" to the file contents on the hard drive)
ln - s - soft link (creates a shortcut to the file location)
chmod - modifies permissions of files (can be used -ugo rwx or with octal notation)
chmod [ugo] + s - assign special permissions at u/g/o level; to remove -s; run a program with the effective user/group id of the owner instead of the executor
chmod +t - add sticky bit; only root user can delete the file
chown - changes the owner of the file
chgrp - changes the group of the file
host - displays information about site IP address and MX record
whatis [command] - short description of the command
[command] --help - longer description of the command
man [command] - full description of the command
tee - outputs on screen and in file
tee -a - appends text to an existing file
cat - displays the content of a file
more - displays content of a file page by page
less - displays content of a file page by page, but you can navigate up and down
head - displays first x lines from a file, where x is a number specified after the command
tail - displays	last x	lines from a file, where x is a	number specified after the command
tail -f [file] shows latest lines from the file, also updating the output as the file gets modified 
cut - displays filtered content based on -c - characters -b - bytes -d - delimiter
awk - displays filtered content based on columns
grep - filters text based on ONE parameter ; -w - searches for the EXACT match
egrep - filters text based on multiple parameters
wc - word count (-l -> no of lines; -c -> no of bytes; -m -> no of characters; -w -> no of words)
diff - compares two files line by line
cmp - compares two files byte by byte
tar cvf - compresses file using tar
tar xvf - extracts tarred file
tar czvf - compresses file using gzip
tar xzvf - extracts gzip file
gzip [filename] - compresses file using gzip
gzip -d / gunzip - extracts gzipped file
truncate -s [no of bytes] - truncates the file to the specified value
alias - create shortcut for longer commands
unalias [alias name] - removes the alias
pushd - adds directories to the directory stack 
popd - removes directories from the directory stack
yum install [package] - installs a package
yum remove [package] - removes a package
yum update - updates all outdated packages while keeping the old versions
yum upgrade - updates all outdated packages while removing older versions
```


## Access Control List

```bash
1) setfacl -m u:user:rwx /path/to/file - add permission for user
2) setfacl -m g:group:rwx /path/to/file - add permission for group
3) setfacl -Rm "entry" /path/to/file - allow all files or directories to inherit ACL entries from the directory it is within
4) setfacl -x u:user /path/to/file - remove a specific entry
5) setfacl -b path/to/file - remove all entries
6) getfacl - gets ACL info on file
```

## System Administration

```bash
vi - openes Vi text editor
	i - insert
	Esc - escapes any mode
	r - replace
	d - delete entire line
	dd - deletes entire line + space between other lines
	u - undo
	x - delete char by char
	o - new line + insert mode
	:q! - quits without saving
	:wq! - quit and save
	/ - search
sed - text manipulation tool; -i -> makes the changes permanent
	's/[text_to_be_replaced]/[new_text]/g' [filename] - substitutes text
	's/[text_to_be_deleted]//g' [filename] - removes text
	'/[text_to_be_deleted]/d' [filename] - deletes the line containing text_to_be_deleted
	'/^$/d' [filename] - deletes empty lines
	'1d' [filename] - deletes the first line
	'1,2d' [filename] - deletes first two lines
	's/\t/ /g' - replaces Tabs with Spaces
	-n [starting line],[finishing line]p [filename] - shows lines from the interval selected
	[starting line],[finishing line]d [filename] - shows all lines except of the interval selected
	G - adds empty lines between each line of text
	'[exception!]s/[text_to_be_replaced]/[new_text]/g' - replaces text except the exception defined
users - shows users that are logged in the system
wall - broadcast messages to all logged users; insert text then Ctrl + D
write [username] - broadcast message to a specific user 
date - shows the date 
uptime - how long since the system booted up
hostname - shows the hostname of the machine
uname -a - prints the name, version and other details about the current machine and the OS running on it.
which - location of the command that you run
cal - calendar - cal [month][year] / cal [year]
bc - calculator
systemctl start|stop|restart|reload|status|enable|disable - services
systemctl list-units --all - shows all services available
systemctl get-default - shows the current run level
systemctl set-default [new target] - sets the system run level in newer versions of Linux 
ps - process status; displays all the proceses currently running in the shell
ps -e - shows all running processes
ps aux - shows all running processes in BSD format
ps -ef - shows all running processes in full format listing 
ps -u [username] - shows all running processes by the specified user
top - Linux Task Manager
top -u [username] - shows running processes / user
top -d [seconds] - delays the top refresh by the no of seconds inserted
top + C key - shows absolute path of the running processes
top + K key - kills a process by introducing PID in the prompt
top + M + P - sort processes by RAM usage
kill - l - get a list of all signal names or signal number
kill [PID] - kill a process with default signal 
kill -1 [PID] - restart
kill -2 [PID] - interrupt from the keyboard just like Ctrl + C
kill -9 [PID] - forcefully kill the process
kill -15 [PID] - kill a process gracefully
shutdown - shuts down the Linux Machine
init 0-6 - system runlevels
reboot - reboots the Linux Machine
halt - force shutdown the Linux Machine without considering other running processes
hostname - displays the hostname of the Linux Machine
hostnamectl - displays Linux Machine information
hostnamectl set-hostname [hostname] - changes the hostname of the Linux Machine 
uname -a - displays kernel version, date/time, CPU arch, OS
dmidecode - information about the Linux Machine (equivalent with systeminfo in Windows)
arch - displays system architecture (x86 / x64 / arm etc)
sos report - generates a report to be sent to RH for diagnostics
echo $0 - shows the shell
&> /dev/null - does not show the output on screen
mpstat - shows CPU usage; 
mpstat -P ALL - command to display detailed statistics about each individual CPU or processor core present in the system
sar -u - used to display CPU utilization statistics collected by the System Activity Reportershows CPU usage	for all	cores
scp -P [port_nr] [file_to_transfer] [user]@[ip]:[path] - Secure	Copy Protocol syntax
rsync -zvh [file] [destination] - transfer a file using rsync on the local machine
rsync -azvh [folder] [destination] - transfer a folder using rsync on the local machine
rsync -avz [file] [user@ip:[location]] - transfer a file to a remote machine
rsync -rzv -e 'ssh -p [port]' --progress [file] [user@ip:[location]] - transfer a file to / from a remote machine specifying the port
```

## User Account Management

```bash
useradd [username] - adds a new user
groupadd [groupname] - adds a new group
userdel [username] - deletes a user; -r - deletes the home/[username] folder
groupdel [groupname] - deletes a group
usermod [username] - modifies a user
useradd -g [groupname] -s /bin/bash -c [description] -m -d /home/[username] [username] - complete command for adding a user
chage [-m mindays] [-M maxdays] [-d lastday] [-I inactive] [-E expiredate] [-W warndays] [username] - change password aging for a specific user
usermod -aG wheel [username] - add user to wheel group meaning providing root access for that user
who - shows who is logged in at that moment
who -r - shows which run level you are currently in
last - shows all users that have logged in that system since the beginning
w - more detail than who
pinky - print user information
id [username] - identifies if the user exists
```

## Crontab

```bash
crontab  - [-e edit] [-l list] [-r remove] [crond - cron daemon]
[minute (0 - 59)] [hour (0 - 23)] [day of the month (1-31)] [month (1-12)] [day of the week (0 - 6)] <command to execute> - crontab table columns
at - program a task to run only once
at HH:MM AM/PM - schedules commands to run just once
at 2:45 AM 101621 - schedule a job for 16th October 2021
at 4PM + 4 days - schedule a job at 4pm four days from now
at now + 5 hours - schedule a job 5 hours from now
at 8:00 AM Sun - schedule a job to 8AM on coming Sunday
at 10:00AM next month - schedule a job to 10AM next month
atq - displays all at entries
atrm # - removes an at entry based on the number added
atd - at daemon
```

## Process Management

```bash
Ctrl + Z - pauses / stops a running process
jobs - shows all processes running or paused in the bash shell
bg - starts the process in the background
fg - brings back the process to the foreground
nohup [command] & - executes a command in the background without being attached to the shell (meaning it will continue to work even if you close the terminal)
nohup [command] > /dev/null 2>&1 & - just like above, but without showing details on screen
nice -n [value: -20 -> 19] [command] - prioritizes the execution of the command; -20 - highest priority; 19 - lowest priority
perf - performance statistics
perf stat -p [PID] - performance statistics for a specific process ID
perf top - provides a real-time top-like interface showing the most CPU-consuming functions
perf trace -p [PID] - traces syscalls for the process with PID
perf list - displays a list of events that can be monitored
sysctl - view, set and manage kernel parameters
sysctl -a - displays all kernel parameters
sysctl -w [parameter_name]=[value] - temporarily modifies a parameter
sysctl -p - makes the modifications persistent
```

## System Monitoring

```bash
top - Linux Task Manager
df - shows available space (common usage: df -h | sort -r)
du - shows used space (common usage: du -sh * | sort -hr)
dmesg - displays boot information and error messages 
iostat 1 - displays usage information on CPU and storage devices
netstat - displays network information (-rnv)
free - displays available and used RAM and Swap memory
```

## Disk Management

```bash
df - outputs the amount of available disk space (-h - human readable; -i - inodes; -t [type] - displays the partitions of [type] type; -T - displays all partitions and their filesystem
cfdisk - fdisk with GUI - partition manager
fdisk -l - shows info about the partitions available
fdisk [/dev/sd[x]] - starts the fdisk utility for partitioning
	help - to see all available options
	n - new partition
	w - write modifications to partition table
	t - changes partition's system ID
mkfs.xfs - sets the filesystem to xfs
mount [/dev/sd[x]] /[folder_name]
vi /etc/fstab -> [/dev/sd[x]]	/[folder_name]	xfs	defaults	0	0 - set persistent mounting point
umount [folder_name] - unmount partition
mount -a - checks fstab and mounts all partitions that are written there
pvcreate [/dev/sd[x]] - creates a physical volume
pvdisplay - shows all physical volumes (pvs - shorted version)
vgcreate [name] [/dev/sd[x]] - creates a volume group
vgdisplay [name] - information about the volume group
vgextend [name] [partition_that_extends_vg] - extends the volume group
lvcreate -n [name] --size [size_of_pv] [vg_name]
lvdisplay - displays logical volumes
lvextend -L+[size] [lv_path]
mkfs.xfs [vg_name]/[lv_name]
mount [vg_name]/[lv_name] /[folder_name_to_mount]
xfs_growfs [lv_path] - extends the filesystem
free -m - display amount of free memory
fsck - for ext2, ext3, ext4 - check and repair utility; should be executed on an unmounted filesystem; -f - to force check filesystem; -y - to auto fix issues
xfs_repair - for xfs filesystem - check and repair utility
dd if=[source_path] of=[destination_path] - backup drives / partitions
dd if=[/root/sd[x]1.img] of=/dev/sd[y] - restore from backup
```

## fsck Exit Codes

```bash
0 - no errors
1 - filesystem eroors corrected
2 - system should be rebooted
4 - filesystem errors left uncorrected
8 - operational errors
16 - usage or syntax error
32 - fsck canceled by user request
128 - shared library error
```

## Create Swap Partition===

```bash
dd if=/dev/zero of=/[name_of_new_swap] bs=1M count=1024 - allocates space for new swap partition
chmod go-r [name_of_new_swap] - remove read permissions for group and others 
mkswap /[name_of_new_swap] - create swap partition
swapon /[name_of_new_swap] - extends the swap memory
swapoff /[name_of_new_swap] - removes the added swap
/etc/fstab - /[name_of_new_swap]	swap	swap	defaults	0	0
```

## Advanced Storage Using Stratis

```bash
yum/dnf install stratis-cli stratisd
systemctl enable stratisd - enable Stratis Daemon
systemctl start stratisd - starts the Stratis Daemon
lsblk - list block disks
stratis pool create pool 1 /dev/sd[x] - create a new Stratis pool
stratis pool list - verify the Stratis pool created
stratis pool add-data pool1 /dev/sd[y] - extend the pool
stratis pool list - verify the extended pool
stratis filesystem create pool1 fs1 - create a new filesystem using Stratis
stratis filesystem list - verify the filesystem
mkdir /bigdata - create a directory for mount point
mount /dev/stratis/pool1/fs1 /bigdata - mount the filesystem to the bigdata file
stratis filesystem snapshot pool1 fs1 [snapshot_name] - create a snapshot
UUID="[UUID_Code]" /bigdata xfs defaults,x-systemd.requires=stratisd.service	0	0 - add entry to /etc/fstab to mount at boot
```

## System Run Levels

```bash
init 0 - shutdown or halt the system
init 1 - single user mode; usually aliased with s or S
init 2 - multiuser mode without networking
init 3 - multiuser mode with networking
init 4 - not defined
init 5 - multiuser mode with networking and GUI
init 6 - reboot the system
```

## Custom

strace -e open [command] - shows what file is accessed when executing a command
su - switch user (to change user to root run su -)
rpm -qa [packet name] - queries installed package
rpm -ihv [packet name] - installs a local package
rpm -e [package name] - removes a local package 
find / -perm /6000 -type f - finds all executables in Linux with setuid and setgid permissions

## Linux Boot Process -old- before CentOS/RedHat7

```bash
BIOS - Basic Input / Output System executes MBR
MBR - Master Boot Record executes GRUB
GRUB - Grand Unified Bootloader executes Kernel
Kernel - executes /sbin/init
Init - executes runlevel programs
Runlevel - runlevel programs are executed from /etc/rc.d/rc*.d/
```

## Linux Boot Process -new-

```bash
BIOS -> POST (Power On Self Test)
MBR - saved in the first sector of the HDD - stores location of the GRUB2
GRUB2 - loads the Kernel (/boot/grub2/grub.cfg)
Kernel - loads the drivers from initrd.img - starts the first system process (systemd)
systemd - system daemon (PID 1) - reads (/etc/systemd/system/default.target) to bring the system to run-level (7 run-levels - 0-6)
```

## Customize MOTD

```bash
1) Create new file in /etc/profile.d/motd.sh
2) Add desired commands in mothd.sh file
3) Modify the /etc/ssh/sshd_config file (#PrintMotd yes -> PrintMotd no)
4) Restart sshd.service
```

## Files

```bash
/etc/passwd - stores password info and shell information
/etc/group - stores group info
/etc/shadow - stores stores hashed passwords
/etc/login.defs - change password aging settings for all users that are created
/etc/cron.____(directory) [hourly, daily, weekly, monthly]
/etc/anacrontab - the timing for each cron job except daily
/etc/cron.d/0hourly - the timing for the daily cron jobs
/proc/cpuinfo - information about CPU
/proc/meminfo - information about RAM
/etc/[OS]-release - shows information about Linux Distro installed
/etc/shells - shows available shells
/home/user/.bashrc - user level aliases
/etc/bashrc - global level aliases
/etc/inittab - modifies run-level
/etc/motd - message of the day
/etc/nsswitch.conf - nameserver setting
/etc/hostname - hostname
/etc/sysconfig/network
/etc/sysconfig/network-scripts/ifcfg-nic
/etc/resolv.conf
```

## Logs

```bash
/var/log - log directory
boot - boot info
chronyd - an implementation of NTP (Network Time Protocol)
cron - cron execution
maillog - mail logs
secure - saves info about users login
messages - stores all information about hardware, software, applications 
httpd - Apache Web Server logs
```

## Environment Variables

```bash
printenv / env - displays all environment variables
echo $[ENVVAR] - displays ONE environment variable
export [ENVVAR]=[value] - set the environment variable
vi .bashrc - to set the environment variable permanently ([ENVVAR]=[value]; export [ENVVAR])
vi /etc/profile or /etc/bashrc - to globally set the environment variable permanently ([ENVVAR]=[value]; export [ENVVAR])
HISTCONTROL - history recording; ignorespace - doesn't save command if there is a space before the command; ignoredups - doesn't record duplicates; ignoreboth - ignorespace & ignoredups
```

## Terminal Control Keys

```bash
Ctrl + U - erases everything you typed on the command line
Ctrl + C - stops / kills a command
Ctrl + Z - suspend a command
Ctrl + D - exit from an interactive program (signals end of data)
```

## Networking

```bash
ping - sends a series of packages to test connectivity to a specified host
ifconfig - utility to display network information
ip a - newer version of ifconfig
ifup - starts a network interface
ifdown - stops a network interface
netstat - network statistics; shows what ports are connected; live network traffic (-rnv - shows what interfaces are in use; how traffic is flowing etc)
tcpdump - creates a live dump of network traffic
ethtool - utility that provides NIC information 
nmtui - network manager text user interface
nmcli - network manager command line interface
nm-connection-editor - full graphical management tool providing access to NetworkManager configuration options; can only be accessed through GUI
wget - downloads files from internet
curl - test functionality of a webpage; -o - downloads files from internet (like wget)
```

## Creating a VLAN

```bash
1) ip link show - list all available interfaces
2) ip link add link [interface_name] name [interface_name.id] type vlan id [id] - create vlan interface
3) ip link set dev [interface_name.id] up - set vlan interface active
4a) ip addr add 192.168.10.2/24 dev [interface_name.id] - manual set ip address
4b) dhclient [interface_name.id] - automatic set ip address using dhcp 
5) ip addr show [interface_name.id] - check vlan config

To make vlan persistent:

*) For Debian based distros:
1) Edit /etc/network/interfaces
	auto [interface_name.id]
	iface [interface_name.id] inet static
	address 192.168.10.2
	netmask 255.255.255.0
	vlan-raw-device [interface_name]

*) For RHEL based distros:
1) Edit /etc/sysconfig/network-scripts:
	DEVICE=[interface_name.id]
	BOOTPROTO=static
	IPADDR=192.168.10.2
	NETMASK=255.255.255.0
	ONBOOT=yes
	VLAN=yes
```

## Add a service under systemctl management

```bash
Create a unit file in /etc/systemd/system/servicename.service
```

## Change ROOT Password

```bash
01) Reboot
02) Press e when the OS and rescue partitions are shown
03a) Replace ro with rw init=/sysroot/bin/sh after root=/dev/mapper/[OS]-root - RHEL v8 and below
03b) Add rd.break at the end of linux ($root) - RHEL v9
04) Ctrl + X
05) chroot /sysroot
06) mount -o remount,rw /
07) passwd root
08) touch /.autorelabel
09) exit
10) reboot
```

## Fork Bomb Fix

```bash
ulimit -u / ulimit -a
ulimit -S -u 5000
```

## Samba Install and Configuration

```bash
1) Install Samba packages
dnf install samba, samba-client, samba-common

2) Enable Samba service through firewall
firewall-cmd --add-service=samba
firewall-cmd --reload

3) Create Samba share directory and assign permissions
mkdir -p [folder_name]
chmod a+rwx / 777 [folder_name]
chown -R nobody:nobody [folder_name]

4) Disable SELinux

sestatus - check if SELINUX is enabled
nano /etc/selinux/config
SELINUX=enforcing -> SELINUX=disabled
reboot

5) Modify Samba config file

cp /etc/samba/smb.conf /etc/samba/smb.conf.bk
Delete everything from the file
Add the following parameters:

[global]
	workgroup = WORKGROUP
	netbios name = redhat
	security = user
	map to guest = bad user
	dns proxy = no

[Anonymous]
	path = [folder_path]
	browsable = yes
	writable = yes
	guest ok = yes
	guest only = yes
	read only = no

Verify config file using testparm commmand

6) Enable and Start the services

systemctl enable / start smb
systemctl enable / start nmb

7) Mount on Windows Client

Go to Start
Type [Server_IP]/[shared_folder_path]

8) Mount on Linux Client

Install utilities
dnf install cifs-utils samba-client

Create a mount point directory
mkdir mnt/[mount_dir_name]

Mount the Samba share
mount -t cifs //[Server_IP]/Anonymous /mnt/[mount_dir_name]
```

## NFS Config

### Server

```bash
1) Install NFS Packages
dnf install nfs-utlis libnfsidmap

2) Enable the packages
systemctl enable rpcbind
systemctl enable nfs-server
systemctl start rpcbind
systemctl start nfs-server
systemctl start rpc-statd
systemctl start nfs-idmapd

3) Create NFS share directory and assign permissions
mkdir /[folder_name]
chmod a+rwx / 777 /[folder_name]

4) Modify /etc/exports file to add a new shared filesystem
[foldername] [Client_IP] (rw, sync, no_root_squash) - share filesystem for a single IP
[foldername] * (rw, sync, no_root_squash) - share filesystem for everybody

5) Export the NFS Filesystem
exportfs -rv
```

### Client

```bash
1) Install NFS Packages
dnf install nfs-utils rpcbind

2) Enable and start rpcbind service
systemctl start rpcbind

3) Make sure firewall is stopped
ps -ef | egrep "firewall|iptable"

4) Show mount from the NFS Server
showmount -e [Server_IP]

5) Create a mount point
mkdir /mnt/[client_mount_point]

6) Mount the filesystem
mount [Server_IP]:[Server_shared_folder] /mnt/[client_mount_point]

7) Verify the mount point
df -h

8) To unmount
umount /mnt/[client_mount_point]
```

## NIC Bonding Procedure

```bash
1) modprobe bonding
2) modinfo bonding
3) Create /etc/sysconfig/network-scripts/ifcfg-bond0

DEVICE=bond0
TYPE=Bond
NAME=bond0
BONDING_MASTER=yes
BOOTPROTO=none
ONBOOT=yes
IPADDR=[ip_addr]
NETMASK=[netmask]
GATEWAY=[gateway]
BONDING_OPTS=”mode=5 miimon=100”

4) Edit /etc/sysconfig/network-scripts/ethernet1

TYPE=Ethernet
BOOTPROTO=none
DEVICE=[interface_name]
ONBOOT=yes
HWADDR=[MAC_addr]
MASTER=bond0
SLAVE=yes


5) Edit /etc/sysconfig/network-scripts/ethernet2

TYPE=Ethernet
BOOTPROTO=none
DEVICE=[interface_name]
ONBOOT=yes
HWADDR=[MAC_addr]
MASTER=bond0
SLAVE=yes

6) Restart network - systemctl restart network
```

=====Using nmcli to configure static IP=====

nmcli device - get the listing of network interfaces
nmcli connection modify [conn_name] ipv4.addresses [IP]/24
nmcli connection modify [conn_name] ipv4.gateway [default_gateway]
nmcli connection modify	[conn_name] ipv4.method manual
nmcli connection modify [conn_name] ipv4.dns [8.8.8.8]
nmcli connection down [conn_name] && nmcli connection up [conn_name]
ip address show [conn_name]

=====Using nmcli to configure a second static IP=====

nmcli device status
nmcli connection show --active
ifconfig
nmcli connection modify [conn_name] +ipv4.addresses [IP]/24
nmcli connection reload
systemctl reboot
ip address show

=====Configure FTP on the remote server=====

1) rpm -qa | grep vsftpd
2) nano /etc/vsftpd/vsftpd.conf
3) Disable anonymous_login=NO
4) Enable ascii_upload_enable=YES; ascii_download_enable=YES
5) Enable ftpd_banner
6) Add at the end of the file use_localtime=YES
7) systemctl start vsftpd
8) systemctl enable vsfpd
9) systemctl stop firewalld or enable port 21 
10) useradd [ftp_user]

=====Transfer file to the FTP server=====

1) ftp [IP]
2) Enter username and pass
3) bi
4) hash
5) put [filename]
6) bye

=====Fix Backspace Terminal=====

1) stty -a - check how erase is defined
2) Ctrl + V 
3) Backspace
4) Copy code for Backspace
5) stty erase ^H
6) For persistance add stty erase ^H to .bashrc

=====Create Local Repo=====

1) Create a new folder
2) Copy all content of Packages folder to the new folder created
3) Go to /etc/yum.repos.d
4) Create local.repo
	[OS]
	name=[OS]
	baseurl=file:///[new folder path]
	enabled=1
	gpgcheck=0
5) yum install createrepo
6) createrepo /[new folder path]
7) yum clean all - clean cache
8) yum repolist all - shows all repositories
