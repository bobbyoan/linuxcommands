# Comprehensive List of PowerShell Commands

## General Commands
```powershell
# Display PowerShell version
$PSVersionTable

# Get help for a cmdlet
Get-Help <cmdlet>

# Update help files
Update-Help

# List available modules
Get-Module -ListAvailable

# Import a module
Import-Module <module_name>

# List all aliases
Get-Alias

# Set an alias
Set-Alias <alias> <cmdlet>
```

## System Information
```powershell
# Get system information
Get-ComputerInfo

# Get operating system information
Get-CimInstance Win32_OperatingSystem

# Get CPU information
Get-CimInstance Win32_Processor

# Get memory information
Get-CimInstance Win32_PhysicalMemory

# List installed hotfixes
Get-HotFix

# Get disk information
Get-Disk

# Get network adapter information
Get-NetAdapter
```

## File and Directory Management
```powershell
# List files and directories
Get-ChildItem <path>

# Create a new file
New-Item -Path <path> -ItemType File

# Create a new directory
New-Item -Path <path> -ItemType Directory

# Delete a file
Remove-Item <file_path>

# Copy a file or directory
Copy-Item -Path <source> -Destination <destination>

# Move a file or directory
Move-Item -Path <source> -Destination <destination>

# Get file content
Get-Content <file_path>

# Set file content
Set-Content <file_path> -Value <content>

# Append content to a file
Add-Content <file_path> -Value <content>
```

## User and Group Management
```powershell
# List all users
Get-LocalUser

# Create a new user
New-LocalUser -Name <username> -Password (Read-Host -AsSecureString "Enter Password") -FullName "<fullname>"

# Delete a user
Remove-LocalUser -Name <username>

# List all groups
Get-LocalGroup

# Add a user to a group
Add-LocalGroupMember -Group <group_name> -Member <username>

# Remove a user from a group
Remove-LocalGroupMember -Group <group_name> -Member <username>
```

## Process and Service Management
```powershell
# List running processes
Get-Process

# Start a process
Start-Process <process_name>

# Stop a process
Stop-Process -Name <process_name>

# List services
Get-Service

# Start a service
Start-Service <service_name>

# Stop a service
Stop-Service <service_name>

# Restart a service
Restart-Service <service_name>

# Get detailed service information
Get-Service <service_name> | Format-List *
```

## Networking
```powershell
# Get network configuration
Get-NetIPAddress

# Test network connectivity
Test-Connection <hostname>

# Get network adapter information
Get-NetAdapter

# Enable a network adapter
Enable-NetAdapter -Name <adapter_name>

# Disable a network adapter
Disable-NetAdapter -Name <adapter_name>

# List open ports
Get-NetTCPConnection | Where-Object { $_.State -eq "Listen" }

# Set a static IP address
New-NetIPAddress -InterfaceAlias <adapter_name> -IPAddress <ip> -PrefixLength <prefix> -DefaultGateway <gateway>
```

## System Administration
```powershell
# Restart the computer
Restart-Computer

# Shutdown the computer
Stop-Computer

# Log off the current user
Logoff

# Create a scheduled task
New-ScheduledTaskTrigger -Daily -At 6am | Register-ScheduledTask -Action (New-ScheduledTaskAction -Execute "notepad.exe") -TaskName "DailyNotepad"

# Get event logs
Get-EventLog -LogName <log_name>

# Clear event logs
Clear-EventLog -LogName <log_name>
```

## Security
```powershell
# Get Windows Defender status
Get-MpComputerStatus

# Start a Windows Defender scan
Start-MpScan -ScanType FullScan

# Get firewall rules
Get-NetFirewallRule

# Enable a firewall rule
Enable-NetFirewallRule -Name <rule_name>

# Disable a firewall rule
Disable-NetFirewallRule -Name <rule_name>
```

## Scripting and Automation
```powershell
# Run a script
& "<script_path>"

# Create a function
function <function_name> {
    <commands>
}

# Loop through a collection
foreach ($item in <collection>) {
    <commands>
}

# Conditional statements
if (<condition>) {
    <commands>
} elseif (<condition>) {
    <commands>
} else {
    <commands>
}

# Schedule a PowerShell script
Register-ScheduledTask -Action (New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-File <script_path>") -Trigger (New-ScheduledTaskTrigger -Daily -At 6am) -TaskName "DailyScript"
```

## Active Directory (If RSAT Installed)
```powershell
# List all Active Directory users
Get-ADUser -Filter *

# Get detailed user information
Get-ADUser -Identity <username> -Properties *

# Create a new Active Directory user
New-ADUser -Name <name> -SamAccountName <username> -UserPrincipalName <username>@domain.com -AccountPassword (Read-Host -AsSecureString "Enter Password") -Enabled $true

# Delete an Active Directory user
Remove-ADUser -Identity <username>

# List all Active Directory groups
Get-ADGroup -Filter *

# Add a user to an Active Directory group
Add-ADGroupMember -Identity <group_name> -Members <username>

# Remove a user from an Active Directory group
Remove-ADGroupMember -Identity <group_name> -Members <username>
```
