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
```

#### Get-ScheduledTask
*View the existing scheduled tasks on the machine.*

```powershell
Get-ScheduledTask -Taskname '<task name>'       > View task with specified name
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

🔰 Measure-Object argument | ℹ️ Function
-- | --
**`-Word`** | Count the number of words
**`-Line`** | Count the number of lines

#### Select-Object
*Pull out the properties from the output of a cmdlet and create a new object.*

```powershell
Verb-Noun | Select-Object -Property
Get-ChildItem | Select-Object -Property Mode, Name      > Get the Mode and name from Get-ChildItem
```

🔰 Select-Object argument | ℹ️ Function
-- | --
**`-First <x>`** | Select the first x from the result
**`-Last <x>`** | Select the last x from the result
**`-Unique`** | Select only unique values
**`-Skip <x>`** | Skip the first x from the result

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
```

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
