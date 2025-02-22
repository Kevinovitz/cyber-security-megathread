> [!Note]
> Heavy work in progress

<p align="center"><img alt="" src="" width="300" /></p>

*<p align="center">A curated list of usefull tools, programs, websites, and other resources.</p>*

Not all tools have to be downloaded or installed on your computer. I found some invaluable resources/websites the can help you in your endeavours. But, as with the commands, at a certain point it just becomes too much to remember.

<p align="center"><img alt="Need a better meme here.." src="https://github.com/Kevinovitz/cyber-security-megathread/raw/main/images/Cyber_Meme_03.png" width="300" /></p>

So I created this collection of websites that I find to be very interesting and might help others out in the process. I mean, I learned most of my stuff looking at what other people are doing/using.

----

### Subjects

- [Knowledge Bases](#knowledge-bases)
- [Cheatsheets](#cheatsheets)
- [Tools Top Tips](#tools-top-tips)
- [Active Directory](#active-directory)
- [Command Injection](#command-injection)
- [Cryptography](#cryptography)
- [Digital Forensics](#digital-forensics)
- [Encryption](#encryption)
- [Enumeration (Domain)](#enumeration-domain)
- [Enumeration (Host)](#enumeration-host)
- [Hashes](#hashes)
- [File Analysis](#file-analysis)
- [Lateral Movement | Pass the Hash](#lateral-movement--pass-the-hash)
- [Misc](#misc)
- [Network Analysis](#network-analysis)
- [Obfuscation](#obfuscation)
- [Phishing](#phishing)
- [Red Teaming](#red-teaming)
- [Reverse Engineering](#reverse-engineering)
- [Risk Management](#risk-management)
- [Shells (reverse / web / ...)](#shells-reverse--web)
- [SQL Injection](#sql-injection)
- [Static & Dynamic Analysis](#static--dynamic-analysis)
- [Threat Modelling](#threat-modelling)
- [Tunneling / Pivoting](#tunneling--pivoting)
- [Windows Defender Anti-Virus](#windows-defender-anti-virus)
- [XSS** | Cross Site Scripting](#xss---cross-site-scripting)

<br>

## Knowledge Bases

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐HackTricks** | Online and freely available book of knowledge about a multitude of topics within Cyber Security | https://book.hacktricks.xyz/
**⭐Internall All The Things** | Active Directory and Internal Pentest Cheatsheets  | https://swisskyrepo.github.io/InternalAllTheThings/
**⭐Payloads All The Things** | A list of useful payloads and bypasses for Web Application Security. | https://swisskyrepo.github.io/PayloadsAllTheThings/
**⭐Red Teaming Toolkit** | This repository contains cutting-edge open-source security tools (OST) for a red teamer and threat hunter. | https://github.com/infosecn1nja/Red-Teaming-Toolkit
**⭐SecLists** | SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. | https://github.com/danielmiessler/SecLists
**Sticky notes for pentesting** | Search hacking techniques and tools for penetration testings, bug bounty, CTFs.  | https://exploit-notes.hdks.org/
**Netero1010 Security Lab** | A collection of thoughts and research related to offensive security. | https://www.netero1010-securitylab.com
**netbiosX Checklists** | Red Teaming & Pentesting checklists for various engagements  | https://github.com/netbiosX/Checklists
**Total OSCP Guide** | Notepad about stuff related to IT-security, and specifically penetration testing. | https://sushant747.gitbooks.io/total-oscp-guide/content/
**** |  | 

<br>

## Cheatsheets

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐Active Directory Mindmaps** | AD mindmaps made by Orange Cyberdefense about steps related to pentesting an Active Directory environment. | https://github.com/Orange-Cyberdefense/ocd-mindmaps/tree/main
**Enumerating AD cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/ad-enumeration-cheatsheet-55a95535f3ee
**Get-Acl cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/get-acl-cheatsheet-f7871edf247f
**Hash cracking cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/hash-cracking-cheatsheet-
**Windows reverse shells cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/windows-reverse-shells-cheatsheet-5eeb09b28c8e
**Mimikatz cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/mimikatz-cheatsheet-ad2b88059b4
**MS Graph PowerShell cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/microsoft-graph-powershell-cheatsheet-d8a841bafa09
**⭐MSFVenom Cheat Sheet** | Easy way to create Metasploit Payloads | https://web.archive.org/web/20220607215637/https://thedarksource.com/msfvenom-cheat-sheet-create-metasploit-payloads/
**Password Storage Cheat Sheet** | This cheat sheet advises you on the proper methods for storing passwords for authentication. | https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
**Set-Acl cheatsheet** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/set-acl-cheatsheet-6c79e0c2f32b
**SQL injection cheat sheet** | This SQL injection cheat sheet contains examples of useful syntax that you can use to perform a variety of tasks that often arise when performing SQL injection attacks. | https://portswigger.net/web-security/sql-injection/cheat-sheet
**The Credential Theft Shuffle** | Cheatsheet with just commands and links to background information. | https://happycamper84.medium.com/the-credential-theft-shuffle-54ec6cd32ea5
**** |  | 

<br>

## Tools Top Tips

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐Arsenal** | Arsenal is just a quick inventory and launcher for hacking programs. You can search for a command, select one and it's prefilled directly in your terminal. | https://github.com/Orange-Cyberdefense/arsenal
**⭐[Metasploit Framework](commands/metasploit.md)** | The Metasploit framework is a product made by Rapid7 and is part of the Metasploit Project. It is a very powerfull tool that can be used to create and use exploit code on target machines. | https://www.metasploit.com/
**OWASP Juice Shop** | OWASP Juice Shop is probably the most modern and sophisticated insecure web application! It can be used in security trainings, awareness demos, CTFs and as a guinea pig for security tools! Juice Shop encompasses vulnerabilities from the entire OWASP Top Ten along with many other security flaws found in real-world applications! | https://owasp.org/www-project-juice-shop/
**** |  | 

<br>

----

<br>

## Active Directory

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Active Directory Methodology** | All things AD. From a basic overview to complex command. | https://book.hacktricks.xyz/windows-hardening/active-directory-methodology
**DCSync** | DCSync is an attack that allows an adversary to simulate the behavior of a domain controller (DC) and retrieve password data via domain replication. | https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/dcsync
**DCSync Detection** | Blog post about ways to detect DCSync attacks. | https://www.netero1010-securitylab.com/detection/dcsync-detection
**SharpHound CE Flags, Explained** | SharpHound has several optional flags that let you control scan scope, performance, output, and other behaviors. | https://support.bloodhoundenterprise.io/hc/en-us/articles/17481375424795-All-SharpHound-Community-Edition-Flags-Explained
**SharpHound Flags, Explained (Legacy)** | SharpHound Community Edition has several optional flags that let you control scan scope, performance, output, and other behaviors. | https://bloodhound.readthedocs.io/en/latest/data-collection/sharphound-all-flags.html
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**BloodHound** | BloodHound uses graph theory to reveal the hidden and often unintended relationships within an Active Directory or Azure environment. Attackers can use BloodHound to quickly identify highly complex attack paths that would otherwise be impossible to find. | https://github.com/SpecterOps/BloodHound
**SharpHound** | C# Data Collector for BloodHound | https://github.com/SpecterOps/SharpHound
**** |  | 

<br>

## Command Injection
 
### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Certificate Search** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://crt.sh/
**Command Injection Payload List** | This Github repository contains several payloads for use in command injection attacks on Unix or Windows systems. | https://github.com/payloadbox/command-injection-payload-list
**Entrust CTSearch** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://ui.ctsearch.entrust.com/ui/ctsearchui

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Cryptography

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**quipqiup** | Uipqiup is a fast and automated cryptogram solver. | https://www.quipqiup.com/
**** |  | 

<br>

## Digital Forensics

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Arsenal’s Digital Forensics Tools** | Tools by Arsenal Recon used in digital forensics. | https://arsenalrecon.com/downloads/
**FTK Imager** - Disc image acquisition and analysis tools for forensic use. | https://www.exterro.com/digital-forensics-software/ftk-imager
**Rekall** - Framework for memory forensics in incident response. | https://github.com/google/rekall
**Volatility** | Developed as an open source memory forensics tool written in Python. Volatility commands are executed to identify and extract specific artefacts from memory images, and the resulting output can be saved to text files for further examination. | https://github.com/volatilityfoundation/volatility3
**** |  | 

<br>

## Encryption

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**RSA Encryption** | Blog explaining the theory, maths, and examples behind RSA encryption. | https://muirlandoracle.co.uk/2020/01/29/rsa-encryption/
**Setting up your own HTTPS server** | How to create a self-signed SSL certificate for Apache to set up your own HTTPS server. Can also be used to exfiltrate date over HTTPS. | https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-18-04
**Decrypt WPA2-PSK using Wireshark** | In this post we will see how to decrypt WPA2-PSK traffic using wireshark. | https://mrncciew.com/2014/08/16/decrypt-wpa2-psk-using-wireshark/
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**RsaCtfTool** | RSA attack tool (mainly for ctf)** | retrieve private key from weak public key and/or uncipher data | https://github.com/RsaCtfTool/RsaCtfTool
**Rsatool** | Rsatool can be used to calculate RSA and RSA-CRT parameters | https://github.com/ius/rsatool
**** |  | 

<br>

## Enumeration (Domain)

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Certificate Search** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://crt.sh/
**Entrust CTSearch** | Offers a searchable database of certificates that shows current and historical results for a given domain name. | https://ui.ctsearch.entrust.com/ui/ctsearchui

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Enumeration (Host)

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Enum4Linux** | enum4Linux is a Linux alternative to enum.exe for enumerating data from Windows and Samba hosts. | https://github.com/CiscoCXSecurity/enum4linux
**Seatbelt** | Seatbelt is a C# project that performs a number of security oriented host-survey "safety checks" relevant from both offensive and defensive security perspectives. | https://github.com/GhostPack/Seatbelt
**Threader3000** | Multi-threaded Python Port Scanner with Nmap Integration. | https://github.com/dievus/threader3000/tree/master
**** |  | 

<br>

## File Analysis

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**FileInsight** | A program for looking through and editing binary files. | https://github.com/nmantani/FileInsight-plugins
**Hex Fiend** | Hex editor that is light and quick. | https://hexfiend.com/
**HxD** | Binary file viewing and editing with a hex editor. | https://mh-nexus.de/en/hxd/
**** |  | 

<br>

## Hashes

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**CQhashdump** | A small password hash dumping utility by CQure Academy. | https://cqureacademy.wpenginepowered.com/wp-content/uploads/2016/09/cqhashdumpv2.zip
**Hashes.com** | Hashes.com is a hash lookup service. This allows you to input a hash and search for its corresponding plaintext in our database of already-cracked hashes. | https://hashes.com/en/decrypt/hash
**** |  | 

<br>

## Lateral Movement | Pass the Hash

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Alternative ways to Pass the Hash (PtH)** | Alternative ways to pass the hash by using tools as: (evil) WINRM, RDP, smbclient, LDAP, Secretsdump, Pass the Ticket, Mount, SSH, and Resource Based Constrained Delegation (RBCD). | https://www.n00py.io/2020/12/alternative-ways-to-pass-the-hash-pth/
**Introduction to Pass the Hash Attack** | This website goes into how pash the hash attacks work and which tools can be used. | https://medium.com/@upadhyay.varun/pass-the-hash-attack-b0f214b2884a
**Offensive Lateral Movement** | Using various methods to move laterally through a network (psexec, impacket, metasploit, rmi, etc.). | https://eaneatfruit.github.io/2019/08/18/Offensive-Lateral-Movement/
**⭐Pass-the-Hash Attacks** | This page looks at a lot of tools and techniques which can be used to perform a pass the hash attack. | https://juggernaut-sec.com/pass-the-hash-attacks/
**⭐Pass the Hash Techniques** | On this page they look at a lot of tools and techniques which can be used to perform a pass the hash attack. | https://cesidt.medium.com/pass-the-hash-techniques-92e46f28af89
**PSExec Pass the Hash** | Using Metasploit with Psexes to dump the NTLM hashes and access other systems without cracking the passwords | https://www.offsec.com/metasploit-unleashed/psexec-pass-hash/
**⭐Windows Lateral Movement with smb, psexec and alternatives** | Using various methods to move laterally through a network (psexec, impacket, metasploit, rmi, etc.). | https://nv2lt.github.io/windows/smb-psexec-smbexec-winexe-how-to/
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**CrackMapExec** | A swiss army knife for pentesting networks  | https://github.com/Porchetta-Industries/CrackMapExec
**CQhashdump** | A small password hash dumping utility by CQure Academy. | http://4f2bcn3u2m2u2z7ghc17a5jm.wpengine.netdna-cdn.com/wp-content/uploads/2016/09/cqhashdumpv2.zip
**Evil-WinRM** | The ultimate WinRM shell for hacking/pentesting. | https://github.com/Hackplayers/evil-winrm
**Impacket-psexec** | Impacket** | Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/tree/master/examples/psexec.py
**Impacket-smbexec** | Impacket** | Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/blob/master/examples/smbexec.py
**Impacket-wmiexec** | Impacket** | Collection of Python classes for working with network protocols. | https://github.com/fortra/impacket/tree/master/examples/wmiexec.py
**Invoke-PowerDump** | This script utilizes the same technique found in the Metasploit framework’s meterpreter hashdump command. Part of the PowerShell Empire post-exploitation framework. | https://github.com/EmpireProject/Empire/blob/master/data/module_source/credentials/Invoke-PowerDump.ps1
**Invoke-TheHash** | PowerShell Pass The Hash Utils. | https://github.com/Kevin-Robertson/Invoke-TheHash
**lsassy** | Can be used to dump the LSASS process remotely | https://github.com/Hackndo/lsassy
**Metasploit PSExec** | The Psexec module in Metasploit allows us to use a dumped has to connect to a different system | https://www.metasploit.com/download
**Mimikatz** | An open source tool that has become an extremely effective attack tool against Windows clients, allowing bad actors to retrieve cleartext passwords, as well as password hashes from memory. | http://blog.gentilkiwi.com/mimikatz
**Psexec** | PsExec is a light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software. | https://download.sysinternals.com/files/SysinternalsSuite.zip
**xFreeRDP** | RDP client for linux | https://linux.die.net/man/1/xfreerdp
**** |  | 

<br>

## Misc

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Exploiting simple network services in CTF’s** | For those of you that enjoy CTF’s here are a few tips on how you can go about testing non HTTP network services. | https://gregit.medium.com/exploiting-simple-network-services-in-ctfs-ec8735be5eef
**List of file signatures** | This is a list of file signatures, data used to identify or verify the content of a file. | https://en.wikipedia.org/wiki/List_of_file_signatures
**Penetration Test Report** | Penetration Test Report by Offensive Security. | https://www.offsec.com/reports/penetration-testing-sample-report-2013.pdf
**PowerLessShell** | PowerLessShell rely on MSBuild.exe to remotely execute PowerShell scripts and commands without spawning powershell.exe. | https://github.com/Mr-Un1k0d3r/PowerLessShell
**** |  | 

<br>

## Network Analysis

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Wireshark** | Network protocol analyzer for traffic recording and examination. | https://www.wireshark.org/
**Nmap** | A vulnerability detection and network mapping tool. | https://nmap.org/
**Netcat** | Read and write data across network connections with this helpful tool. | https://nmap.org/ncat/
**** |  | 

<br>

## Obfuscation

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**JavaScript Obfuscator** | Javascript Obfuscator is a free tool that can be used for obfuscating JavaScript code. | https://codebeautify.org/javascript-obfuscator
**JavaScript Obfuscator Tool** | A free and efficient obfuscator for JavaScript to make your code harder to copy and prevent people from stealing your work. | https://obfuscator.io/
**Obfuscator.io Deobfuscator** | A tool to undo obfuscation performed by obfuscator.io | https://obf-io.deobfuscate.io/
**** |  | 

<br>

## Phishing

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**GoPhish** | GoPhish is a web-based framework to set up phishing campaigns. It stores your SMTP server settings, has a web-based tool for creating email templates, can also schedule when emails are sent, and has an analytics dashboard that shows how many emails have been sent, opened or clicked. | https://getgophish.com/
**Social Engineering Toolkit (SET)** | The Social Engineering Toolkit contains a multitude of tools, but some of the important ones for phishing are the ability to create spear-phishing attacks and deploy fake versions of common websites to trick victims into entering their credentials. | https://www.trustedsec.com/tools/the-social-engineer-toolkit-set/

<br>

## Red Teaming

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**LOLBAS Repository** | Living Off The Land Binaries, Scripts and Libraries | https://lolbas-project.github.io
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Reverse Engineering

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**PE Format Explained** | Learn more about PE. | https://learn.microsoft.com/en-us/windows/win32/debug/pe-format
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Binary Ninja** | A tool for disassembling and decompiling binaries. | https://binary.ninja/
**Capa** | Capa is the FLARE team's free and open-source tool to identify capabilities in executable files. | https://mandiant.github.io/capa/
**Capa Explorer Web** | Capa Explorer Web is a web-based tool to explore the capabilities identified by capa. | https://mandiant.github.io/capa/explorer/
**CFF Explorer** | A PE editor designed to analyze and edit Portable Executable (PE) files. | https://ntcore.com/explorer-suite/
**FlareVM** | A collection of software installations scripts for Windows systems that allows you to easily setup and maintain a reverse engineering environment on a VM. | https://github.com/mandiant/flare-vm/tree/main
**Ghidra** | NSA-developed open-source reverse engineering suite. | https://ghidra-sre.org/
**Hopper Disassembler** | A Debugger, disassembler, and decompiler. | https://www.hopperapp.com/
**ILSpy** | .NET Decompiler with support for PDB generation, ReadyToRun, Metadata (&more)** | cross-platform! | https://github.com/icsharpcode/ILSpy
**OllyDbg** | Debugger for reverse engineering at the assembly level. | https://www.ollydbg.de/
**PEiD** | Packer, cryptor, and compiler detection tool. | https://github.com/wolfram77web/app-peid
**Radare2** | A sophisticated open-source platform for reverse engineering. | https://rada.re/n/radare2.html
**RetDec** | Open-source decompiler for machine code. | https://github.com/avast/retdec
**x64dbg** | Open-source debugger for binaries in x64 and x32 formats. | https://x64dbg.com/
**** |  | 

<br>

## Risk Management

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**NIST SP 800-30** | A risk assessment methodology developed by the National Institute of Standards and Technology (NIST). It involves identifying and evaluating risks, determining the likelihood and impact of each risk, and developing a risk response plan. | https://csrc.nist.gov/pubs/sp/800/30/r1/final
**Facilitated Risk Analysis Process (FRAP)** | A risk assessment methodology that involves a group of stakeholders working together to identify and evaluate risks. It is designed to be a more collaborative and inclusive approach to risk analysis. | https://pivotpointconsulting.com/insights/blog/using-frap-for-risk-assessment/
**Operationally Critical Threat, Asset, and Vulnerability Evaluation (OCTAVE)** | A risk assessment methodology that focuses on identifying and prioritising assets based on their criticality to the organisation’s mission and assessing the threats and vulnerabilities that could impact those assets. | https://www.iriusrisk.com/resources-blog/octave-threat-modeling-methodologies
**Failure Modes and Effect Analysis (FMEA)** | A risk assessment methodology commonly used in engineering and manufacturing. It involves identifying potential failure modes for a system or process and then analysing the possible effects of those failures and the likelihood of their occurrence. | https://asq.org/quality-resources/fmea
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Shells (reverse / web / ...)

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**b374k webshell** | This PHP Shell is a useful tool for system or web administrator to do remote management without using cpanel, connecting using ssh, ftp etc. All actions take place within a web browser | https://github.com/b374k/b374k
**p0wny-shell** | p0wny@shell:~# is a very basic, single-file, PHP shell. It can be used to quickly execute commands on a server when pentesting a PHP application. | https://github.com/flozz/p0wny-shell
**** |  | 

<br>

## SQL Injection

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**SQL injection cheat sheet** | This SQL injection cheat sheet contains examples of useful syntax that you can use to perform a variety of tasks that often arise when performing SQL injection attacks. | https://portswigger.net/web-security/sql-injection/cheat-sheet
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## Static & Dynamic Analysis

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Dependency Walker** | A tool for displaying an executable’s DLL dependencies. | https://www.dependencywalker.com/
**DIE (Detect It Easy)** | A packer, compiler, and cryptor detection tool. | https://github.com/horsicq/Detect-It-Easy
**InetSIM** | INetSim is a software suite for simulating common internet services in a lab environment, e.g. for analyzing the network behaviour of unknown malware samples.  | https://www.inetsim.org/
**Oledump.py** | oledump.py is a program to analyze OLE files. These files contain streams of data. oledump allows you to analyze these streams. The best known is MS Office files. | https://blog.didierstevens.com/programs/oledump-py/
**PEStudio** | A software designed to investigate potentially malicious files and extract information from them without execution. This will help us focus on the static analysis side of the investigation | https://www.winitor.com/download
**PEview** | A portable executable (PE) file viewer for analysis. | http://wjradburn.com/software/
**Process Hacker** | Sophisticated memory editor and process watcher. | https://processhacker.sourceforge.io/downloads.php
**** |  | 

<br>

## Threat Modelling

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**MITRE ATT&CK framework** | A comprehensive, globally accessible knowledge base of cyber adversary behaviour and tactics, developed by the MITRE Corporation | https://attack.mitre.org/
**DREAD Framework** | A risk assessment model developed by Microsoft to evaluate and prioritise security threats and vulnerabilities. | https://learn.microsoft.com/en-us/windows-hardware/drivers/driversecurity/threat-modeling-for-drivers#the-dread-approach-to-threat-assessment
**STRIDE Framework** | A threat modelling methodology developed by Microsoft, which helps identify and categorise potential security threats in software development and system design. | https://www.softwaresecured.com/stride-threat-modeling/
**PASTA Framework** | A structured, risk-centric threat modelling framework designed to help organisations identify and evaluate security threats and vulnerabilities within their systems, applications, or infrastructure. | https://versprite.com/blog/what-is-pasta-threat-modeling/
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**ATT&CK Navigator** | An open-source, web-based tool that helps visualise and navigate the complex landscape of the MITRE ATT&CK Framework. | https://mitre-attack.github.io/attack-navigator/
**** |  | 

<br>

## Tunneling / Pivoting

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Neo-reGeorg** | Encapsulates other protocols and sends them back and forth via the HTTP protocol. Create an HTTP tunnel communication channel to pivot into the internal network and communicate with local network devices through HTTP protocol. | https://github.com/L-codes/Neo-reGeorg
**** |  | 

<br>

## Windows Defender Anti-Virus

### Usefull documentation

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**⭐Manage MS Defender with PowerShell on Windows 10** | You can manage settings and control virtually any aspect of the Microsoft Defender Antivirus using PowerShell commands. | https://www.windowscentral.com/how-manage-microsoft-defender-antivirus-powershell-windows-10

### Related tools

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**** |  | 

<br>

## XSS** | Cross Site Scripting

🔰 Name | ℹ️ Description | 🔗 Link
-- | -- | --
**Ultimate XSS Polyglot** | An XSS polyglot can be generally defined as any XSS vector that is executable within various injection contexts in its raw form. | https://github.com/0xsobky/HackVault/wiki/Unleashing-an-Ultimate-XSS-Polyglot
**XSS Hunter (deprecated)** | A popular open source web-based tool for identifying cross-site scripting (XSS) bugs in websites. Now depreciated, use the offline [version](tools.md#xss---cross-site-scripting) now. | https://xsshunter.com/
**** |  | 



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
