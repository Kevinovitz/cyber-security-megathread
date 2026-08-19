# Powershell Command Syntax

<p align="center"><img alt="Powershell Logo" src="https://itblog.ldlnet.net/wp-content/uploads/2019/01/powershell-2.png" width=500 /></p>

PowerShell is a task automation and configuration management program from Microsoft, consisting of a command-line shell and the associated scripting language.

</br>

## Table of Contents

- [Main commands to use Powershell](#main-commands-to-use-powershell)
- [Other usefull commands](#other-usefull-commands)

> [!NOTE]
> Some of these commands can only be used after a (meterpreter) shell has been made to another machine. These will be marked with a 💲. Others must be used outside of these shells.

<br>

## Basic Powershell Syntax

Powershell uses a `verb-noun` structure in its commands

**Common verbs:**

```
> Get
> Start
> Stop
> Read
> Write
> New
> Out
```

The Pipeline `|` is used to pass output from one cmdlet to another.

View details/members of the output of a certain cmdlet you can use `Get-Member`.

Pull out the properties from the output of a cmdlet and create a new object using `Select-Object`.

<br>

## Usefull Commands/Cmdlets

#### Get-Acl
*Get security (permissions, owner) descriptors of a file or folder.*

```powershell
Get-Acl -Path "C:\"     > View the owner of the specified path
```

#### Get-ChildItem
*List the contents of the current directory.*

```powershell
Get-ChildItem -File -Hidden -ErrorAction SilentlyContinue

> Use this command to search for files in a specified directory

Get-ChildItem -Path C:\ -File -Recurse -Include *<term>* -ErrorAction SilentlyContinue

> Remove '-File' to also look for directories

gci C:\ *.pub -file -ea silent -recurse

> Same idea using aliases (gci = Get-ChildItem, ea = ErrorAction) — search the whole C: drive for files with a specific extension
```

#### Get-Command
*List all available commands.*

```powershell
Get-Command
Get-Command Verb-*      > List command with the specified verb
Get-Command *-Noun      > List command with the specified noun
```

#### Get-Content
*Read the contents of a file.*

```powershell
Get-Content -Path file.txt
(Get-Content -Path file.txt)[index]                     > Get string on provided index
Get-Content -Path file.txt | Measure-Object -Word       > Get the number of words in the file
gc C:\Windows\System32\LogFiles\Firewall\pfirewall.log | more    > Read the Windows Firewall log (gc is an alias for Get-Content)
```

#### Get-Disk
*View the disks attached to the machine, including their partition style.*

```powershell
Get-Disk       > Shows the partition style (MBR/GPT) of each disk
```

#### Get-FileHash
*Get the hash of a specific file.*

```powershell
Get-FileHash -Algorithm MD5 file.txt
```

#### Get-Help
*Get help for a specific cmdlet.*

```powershell
Get-Help <Command-name>
Get-Help Get-Contents                   > Get help for the Get-Contents cmdlet
Get-Help <Command-name> -Examples       > How to use the command examples
```

#### Get-Hotfix
*View all applied patches to the machine.*

```powershell
Get-Hotfix -ID <KB nr.>                                         > Two different ways of looking up a specific patch
Get-Hotfix | Where-Object -Property HotFixID -eq <KB nr.>       > Two different ways of looking up a specific patch
```

#### Get-LocalUser
*View the users on the current machine.*
```powershell
Verb-Noun | ft colum names
> Format the output with specified columns (use Get-Member to find valid entries)
```

#### Get-LocalGroup
*View the groups on the current machine.*

```powershell
Verb-Noun | ft colum names
> Format the output with specified columns (use Get-Member to find valid entries)
```

#### Get-Member
*View details/members of the output of a certain cmdlet.*

```powershell
Verb-Noun | Get-Member
Get-Command | Get-Member -MemberType Method     > View the members of Get-Command
```

#### Get-NetTCPConnection
*View all connection to the machine.*

```powershell
Get-NetTCPConnection -State Listen      > List all listening connections

Get-NetTCPConnection | select LocalAddress,localport,remoteaddress,remoteport,state,@{name="process";Expression={(get-process -id $_.OwningProcess).ProcessName}}, @{Name="cmdline";Expression={(Get-WmiObject Win32_Process -filter "ProcessId = $($_.OwningProcess)").commandline}} | sort Remoteaddress -Descending | ft -wrap -autosize
> Show TCP connections and the process/command line associated with each

(Get-NetTCPConnection).remoteaddress | Sort-Object -Unique      > Sort and get unique remote IPs

Get-NetTCPConnection -remoteaddress <ip>  | select state, creationtime, localport,remoteport | ft -autosize      > Investigate connections to/from a specific IP address
```

#### Get-NetUDPEndpoint
*View all UDP connections to the machine.*

```powershell
Get-NetUDPEndpoint | select local*,creationtime, remote* | ft -autosize
```

#### Get-DnsClientCache
*View the local DNS resolver cache.*

```powershell
Get-DnsClientCache | ? Entry -NotMatch "workst|servst|memes|kerb|ws|ocsp" | out-string -width 1000
```

#### Get-SmbConnection / Get-SmbShare
*View active SMB connections or configured SMB shares.*

```powershell
Get-SmbConnection
Get-SmbShare
```

#### Get-ScheduledTask
*View the existing scheduled tasks on the machine.*

```powershell
Get-ScheduledTask -Taskname '<task name>'       > View task with specified name

Get-ScheduledTask | Where-Object {$_.State -ne "Disabled"}       > List all enabled scheduled tasks

Get-ScheduledTask | Where-Object {$_.Date -ne $null -and $_.State -ne "Disabled"} | Sort-Object Date | select Date,TaskName,Author,State,TaskPath | ft
> List all enabled scheduled tasks with a creation date, sorted by date
```

#### Get-Service
*View services and their status/start type on the machine.*

```powershell
Get-Service | Where-Object {$_.Status -eq "Running" -and $_.StartType -eq "Automatic"}       > List all running services set to start automatically
```

#### Get-WinEvent
*Query Windows Event Logs.*

```powershell
Get-WinEvent -FilterHashTable @{LogName='System';ID='7045'} | fl       > Retrieve events matching a specific log and Event ID
```

#### Launch the hidden executable hiding within ADS

```powershell
wmic process call create $(Resolve-Path file.exe:streamname)
```

#### Measure-Object
*Measure various metrics of an output.*

```powershell
Verb-Noun | Measure-Object				-> View all metrics
```

Measure-Object argument | Function
-- | --
**`-Word`** | Count the number of words
**`-Line`** | Count the number of lines

#### Select-Object
*Pull out the properties from the output of a cmdlet and create a new object.*

```powershell
Verb-Noun | Select-Object -Property
Get-ChildItem | Select-Object -Property Mode, Name      > Get the Mode and name from Get-ChildItem
```

Select-Object argument | Function
-- | --
**`-First <x>`** | Select the first x from the result
**`-Last <x>`** | Select the last x from the result
**`-Unique`** | Select only unique values
**`-Skip <x>`** | Skip the first x from the result

```powershell
somecommand | Select-Object *
```
List all properties of an item, including ones not shown by default. Useful for discovering what fields are available before filtering with `-Property`.

#### Set-Location
*Navigate to a specific directory.*

```powershell
Set-Location .\Documents\
Set-Location -Path c:\users\administrator\Documents
```

#### Select-String
*Search a file for a pattern.*

```powershell
Select-String -Path 'C:\users\administrator\desktop' -Pattern '\.pdf'
Get-ChildItem -Recurse | Select-String -Pattern '<string>'      > Recursively search file contents for a string
```

#### findstr
*Search a file for a pattern (native Windows command, not a PowerShell cmdlet).*

```powershell
findstr /s /i "<string>" C:\Users\Administrator\Desktop\*.*      > Recursively (/s) and case-insensitively (/i) search files for a string
```

#### Searching for a String — Which Tool to Use

Tool | Pros | Cons
-- | -- | --
**`Select-String`** | Native PowerShell cmdlet; supports regex; returns rich objects (filename, line number, matched text) that can be piped further | Slower than `findstr` on very large file sets; regex syntax differs slightly from `findstr`
**`Where-Object`** | Best for filtering structured object properties (e.g. process names, service states) rather than raw text | Not intended for searching inside file contents; requires the data to already be an object collection
**`findstr`** | Very fast, available on any Windows box without PowerShell; simple substring/regex search | Limited regex support; returns plain text lines, not objects — harder to process further

<br>

#### Sort-Object
*Sort the output of a cmdlet.*
```powershell
Verb-Noun | Sort-Object
```

#### View Alternate Data Streams (ADS)

```powershell
Get-Item -Path file.exe -Stream *
```

#### Where-Object
*Filter objects.*

```powershell
Verb-Noun | Where-Object -Property <Propertyname> -<operator> <Value>       > Filter object
Verb-Noun | Where-Object {$_.<Propertyname> -<operator> <Value>             > Iterate through every object

-<operator>     > Contains, eq, gt
```

https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-6





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
