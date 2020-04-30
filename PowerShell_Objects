# Working with objects
## Viewing Object Structire (Get-Member)
```
Get-Process | Get-Member
Get-Process | Get-Member -MemberType Properties
```

## Selecting Parts of Objects (Select-Object)
```
Get-CimInstance -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace
```
create calculated properties
```
Get-CimInstance -Class Win32_LogicalDisk |
  Select-Object -Property Name, @{
    label='FreeSpace'
    expression={($_.FreeSpace/1GB).ToString('F2')}
  }
```

## Filtering Objects in the pipeline

### Performing Simple Tests with Where-Object

#### Comparision Operators
```
-eq
1 -eq 1

-ne
1 -ne 2

-lt
1 -lt 2

-le
1 -le 2

-gt
2 -gt 1

-ge
2 -ge 1

-like
"file.doc" -like "f*.do?"

-notlike
"file.doc" -notlike "p*.doc"

-contains
1,2,3 -contains 1

-notcontains
1,2,3 -notcontains 4

```

#### Logical Operators
```
-and
(1 -eq 1) -and (2 -eq 2)

-or
(1 -eq 1) -or (1 -eq 2)

-not
-not (1 -eq 2)

!
!(1 -eq 2)
```

#### Where-Object script blocks use the special variable $_
```
1,2,3,4 | Where-Object {$_ -lt 3}
```

#### Filtering based on Object Propertis
```
Get-CimInstance -Class Win32_SystemDriver |
  Where-Object {$_.State -eq 'Running'}
```
```
Get-CimInstance -Class Win32_SystemDriver |
  Where-Object {$_.State -eq "Running"} |
    Where-Object {$_.StartMode -eq "Auto"}
```
```
Get-CimInstance -Class Win32_SystemDriver |
  Where-Object {$_.State -eq "Running"} |
    Where-Object {$_.StartMode -eq "Manual"} |
      Format-Table -Property Name,DisplayName
```
```
Get-CimInstance -Class Win32_SystemDriver |
  Where-Object {($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual')} |
    Format-Table -Property Name,DisplayName
```

### Sorting Objects
#### Basic Sorting

Ascending
```
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name |
  Format-Table -Property LastWriteTime, Name
```

Descending
```
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name -Descending |
  Format-Table -Property LastWriteTime, Name
```

Using hash tables

You can sort different properties in different orders by using hash tables in an array. Each hash table uses an Expression key to specify the property name as string and an Ascending or Descending key to specify the sort order by $true or $false. The Expression key is mandatory. The Ascending or Descending key is optional.
```
Get-ChildItem |
  Sort-Object -Property @{ Expression = 'LastWriteTime'; Descending = $true }, @{ Expression = 'Name'; Ascending = $true } |
  Format-Table -Property LastWriteTime, Name
```

set a scriptblock to the Expression key. When running the Sort-Object cmdlet, the scriptblock is executed and the result is used for sorting.
The following example sorts objects in descending order by the time span between CreationTime and LastWriteTime.
```
Get-ChildItem |
  Sort-Object -Property @{ Expression = { $_.LastWriteTime - $_.CreationTime }; Descending = $true } |
  Format-Table -Property LastWriteTime, CreationTime
```

### Using Static Classes and Methods
```
# Getting Environment Data with System.Environment
[System.Environment]
[System.Environment] | Get-Member
[System.Environment] | Get-Member -Static

# Displaying Static Properties of System.Environment
[System.Environment]::Commandline

# Doing Math with System.Math
[System.Math] | Get-Member -Static -MemberType Methods
```

### Getting WMI Objects (Get-CimInstance)

Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner. Because of how much WMI makes possible, the PowerShell cmdlet for accessing WMI objects, Get-CimInstance, is one of the most useful for doing real work.

```
# Listing WMI Classes
# trying to find out what can be done with WMI.

Get-CimClass -Namespace root/CIMV2 |
  Where-Object CimClassName -like Win32* |
    Select-Object CimClassName

# retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:

Get-CimClass -Namespace root/CIMV2 -ComputerName 192.168.1.29


# Displaying WMI Class Details

Get-CimInstance -Class Win32_OperatingSystem
Get-CimInstance -Class Win32_OperatingSystem | Get-Member -MemberType Property

# Displaying Non-Default Properties with Format Cmdlets

Get-CimInstance -Class Win32_OperatingSystem |
  Format-Table -Property TotalVirtualMemorySize, TotalVisibleMemorySize,
    FreePhysicalMemory, FreeVirtualMemory, FreeSpaceInPagingFiles

# The memory data might be more readable if you format it as a list by typing:
Get-CimInstance -Class Win32_OperatingSystem | Format-List Total*Memory*, Free*

```

# Creating .NET and COM Objects (New-Object)
## Using Internet Explorer from Windows Powershell
```
$ie = New-Object -ComObject InternetExplorer.Application
$ie.Visible = $true
$ie.Navigate("https://devblogs.microsoft.com/scripting/")
$ie.Document.Body.InnerText
$ie.Quit()
Remove-Variable ie
```
To improve readability, you can place the hash tables into a separate variable:
```
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```

