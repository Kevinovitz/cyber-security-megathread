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

- [Aircrack-ng](#aircrack-ng)
- [Smbclient](#smbclient)

<br>

## Separate command sheets

Some tools are so vast, they have many commands. Too many to include in this document whilst keeping it nice and organized. That is why I created a separate document specifically for such programs. 

🔰 Name |
-- | 
**⭐[Metasploit Framework](commands/metasploit.md)**
**⭐[Powershell](commands/powershell.md)**
****

## Aircrack-ng

Aircrack- ng is a complete suite of tools to assess WiFi network security. More info [here](https://www.aircrack-ng.org/)

**_Crack wifi passwords from a network capture file (must include EAPOL handshake)._**

```console
aircrack-ng -w <wordlist> <capture_file>
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture.pcap
```

## Smbclient

Smbclient is a client that can 'talk' to an SMB/CIFS server and is part of the Samba suite.

**_'Exploit' misconfiguration of the anonymous login ability._**

```console
smbclient <ip> -U:Anonymous -p:<port>
```

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
