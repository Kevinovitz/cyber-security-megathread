> [!Note]
> Heavy work in progress

<p align="center"><img alt="" src="" width="300" /></p>

*<p align="center">A curated list of usefull tools, programs, websites, and other resources.</p>*

Not all tools have to be downloaded or installed on your computer. I found some invaluable resources/websites the can help you in your endeavours. But, as with the commands, at a certain point it just becomes too much to remember.

<p align="center"><img alt="Need a better meme here.." src="https://github.com/Kevinovitz/cyber-security-megathread/blob/main/images/Cyber_Meme_03.png" width="300" /></p>

So I created this collection of websites that I find to be very interesting and might help others out in the process. I mean, I learned most of my stuff looking at what other people are doing/using.

----

### Subjects

- [Command Injection](3command-injection)
- [Domain Enumeration](#domain-enumeration)
- [XSS - Cross Site Scripting](#xss---cross-site-scripting)

<br>

## Knowledge Bases

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐HackTricks** | Online and freely available book of knowledge about a multitude of topics within Cyber Security | https://book.hacktricks.xyz/
**** |  | 

<br>

## Cheatsheets

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Enumerating AD cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/ad-enumeration-cheatsheet-55a95535f3ee
**Get-Acl cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/get-acl-cheatsheet-f7871edf247f
**Hash cracking cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/hash-cracking-cheatsheet-**Windows reverse shells cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/windows-reverse-shells-cheatsheet-5eeb09b28c8e
**Mimikatz cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/mimikatz-cheatsheet-ad2b88059b4
**MS Graph PowerShell cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/microsoft-graph-powershell-cheatsheet-d8a841bafa09
7c10f2b31143
**Set-Acl cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/set-acl-cheatsheet-6c79e0c2f32b
**The Credential Theft Shuffle** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/the-credential-theft-shuffle-54ec6cd32ea5
**** |  | 

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

----

<br>

## Active Directory

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Active Directory Methodology** | All things AD. From a basic overview to complex command. | https://book.hacktricks.xyz/windows-hardening/active-directory-methodology
**DCSync** | DCSync is an attack that allows an adversary to simulate the behavior of a domain controller (DC) and retrieve password data via domain replication. | https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/dcsync

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Command Injection
 
### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Certificate Search** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://crt.sh/
**Command Injection Payload List** | This Github repository contains several payloads for use in command injection attacks on Unix or Windows systems. | https://github.com/payloadbox/command-injection-payload-list
**Entrust CTSearch** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://ui.ctsearch.entrust.com/ui/ctsearchui

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Domain Enumeration

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Certificate Search** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://crt.sh/
**Entrust CTSearch** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://ui.ctsearch.entrust.com/ui/ctsearchui

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

### Usefull documentation

## Hashes

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**CQhashdump** | A small password hash dumping utility by CQure Academy. | https://cqureacademy.wpenginepowered.com/wp-content/uploads/2016/09/cqhashdumpv2.zip

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Lateral Movement - Pass the Hash

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Alternative ways to Pass the Hash (PtH)** | Alternative ways to pass the hash by using tools as: (evil) WINRM, RDP, smbclient, LDAP, Secretsdump, Pass the Ticket, Mount, SSH, and Resource Based Constrained Delegation (RBCD). | https://www.n00py.io/2020/12/alternative-ways-to-pass-the-hash-pth/
**Introduction to Pass the Hash Attack** | This website goes into how pash the hash attacks work and which tools can be used. | https://medium.com/@upadhyay.varun/pass-the-hash-attack-b0f214b2884a
**Offensive Lateral Movement** | Using various methods to move laterally through a network (psexec, impacket, metasploit, rmi, etc.). | https://eaneatfruit.github.io/2019/08/18/Offensive-Lateral-Movement/
**⭐Pass the Hash Techniques** |  | https://cesidt.medium.com/pass-the-hash-techniques-92e46f28af89
**PSExec Pass the Hash** | Using Metasploit with Psexes to dump the NTLM hashes and access other systems without cracking the passwords | https://www.offsec.com/metasploit-unleashed/psexec-pass-hash/
**⭐Windows Lateral Movement with smb, psexec and alternatives** | Using various methods to move laterally through a network (psexec, impacket, metasploit, rmi, etc.). | https://nv2lt.github.io/windows/smb-psexec-smbexec-winexe-how-to/

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**CrackMapExec** | A swiss army knife for pentesting networks  | https://github.com/Porchetta-Industries/CrackMapExec
**CQhashdump** | A small password hash dumping utility by CQure Academy. | http://4f2bcn3u2m2u2z7ghc17a5jm.wpengine.netdna-cdn.com/wp-content/uploads/2016/09/cqhashdumpv2.zip
**Evil-WinRM** | The ultimate WinRM shell for hacking/pentesting. | https://github.com/Hackplayers/evil-winrm
**Impacket-psexec** | Impacket - Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/tree/master/examples/psexec.py
**Impacket-smbexec** | Impacket - Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/blob/master/examples/smbexec.py
**Impacket-wmiexec** | Impacket - Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/tree/master/examples/wmiexec.py
**Invoke-TheHash** | PowerShell Pass The Hash Utils. | https://github.com/Kevin-Robertson/Invoke-TheHash
**Metasploit PSExec** | The Psexec module in Metasploit allows us to use a dumped has to connect to a different system | https://www.metasploit.com/download
**Mimikatz** | An open source tool that has become an extremely effective attack tool against Windows clients, allowing bad actors to retrieve cleartext passwords, as well as password hashes from memory. | http://blog.gentilkiwi.com/mimikatz
**Psexec** | PsExec is a light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software. | https://download.sysinternals.com/files/SysinternalsSuite.zip
**xFreeRDP** | RDP client for linux | https://linux.die.net/man/1/xfreerdp

<br>

## Windows Defender Anti-Virus

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐Manage MS Defender with PowerShell on Windows 10** | You can manage settings and control virtually any aspect of the Microsoft Defender Antivirus using PowerShell commands. | https://www.windowscentral.com/how-manage-microsoft-defender-antivirus-powershell-windows-10

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## XSS - Cross Site Scripting

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**XSS Hunter (deprecated)** | A popular open source web-based tool for identifying cross-site scripting (XSS) bugs in websites. Now depreciated, use the offline [version](tools.md#xss---cross-site-scripting) now. | https://xsshunter.com/



<!--- 

## TITLE

### Usefull documentation

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 


Name | ℹ️ Description | 🔗 Link
-- | -- | --

--->
