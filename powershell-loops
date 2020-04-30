## ForEach-Object Loop
```
# ForEach-Object has two aliases, ForEach and %

Get-WMIObject Win32_LogicalDisk | ForEach-Object {$_.FreeSpace}
# or
Get-WMIObject Win32_LogicalDisk | ForEach {$_.FreeSpace}
# or
Get-WMIObject Win32_LogicalDisk | % FreeSpace
```

## PowerShell For Loop
```
$colors = @("Red","Orange","Yellow","Green","Blue","Indigo","Violet")
For ($i=0; $i -lt $colors.Length; $i++) {
    $colors[$i]
}
```

## While, Do-While and Do-Until Loops
While and Do-While loops are both used to perform an action while the condition evaluates to $true, and differ only in their syntax.
Do-Until loops have similar syntax to Do-While, but stop processing once the condition statement is met.

```
# While
$i=1
While ($i -le 10) {
  $i
  $i++
}
    
# Do-While
$i=1
Do {
  $i
  $i++
} While ($i -le 10)

# Do-Until
$i=1
Do {
  $i
  $i++
} Until ($i -gt 10)
```

To exit a loop early use Break
```
# Break
While ($true) {
  $i
  $i++
  if ($i -gt 10) {
    Break
  }
}
```

