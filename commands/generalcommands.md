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
- [Neo-ReGeorg](#neo-regeorg)
- [RsaCTFtool](#rsactftool)
- [Rsatool](#rsatool)
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

## Enum4Linux

enum4Linux is a Linux alternative to enum.exe for enumerating data from Windows and Samba hosts.

More info [here](https://github.com/CiscoCXSecurity/enum4linux).

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

**_Firefox_**

Configure a manual proxy in the network setting and use the ip and port as listed in the Neo-reGeorge CLI output for the SOCKS host.

## Smbclient

Smbclient is a client that can 'talk' to an SMB/CIFS server and is part of the Samba suite.

**_'Exploit' misconfiguration of the anonymous login ability._**

```console
smbclient <ip> -U:Anonymous -p:<port>
```

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
