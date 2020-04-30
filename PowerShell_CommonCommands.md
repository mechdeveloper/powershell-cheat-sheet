# powershell-cheat-sheet
Basic PowerShell commands for windows administration

## Create PowerShell session (PSSession) on local or remote computer
```
$Server01 = New-PSSession -ComputerName Server01
$s1, $s2, $s3 = New-PSSession -ComputerName Server01,Server02,Server03
```

```
$Server01 = NEW-PSSESSION -COMPUTERNAME Server01
ENTER-PSSESSION -SESSION $Server01

hostname

Exit-PSSession
```

https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/new-pssession?view=powershell-7

## logoff a user from a session 
```
logoff
logoff <sessionid>
logoff <nameofsession> /server:<nameofserver>
```

## list Environment variables
```
Get-ChildItem Env:
# or
ls Env:
```

## Send emails from PowerShell
```
$hostname = hostname
Send-MailMessage -From 'test@domain.com' -To 'user@domain.com' -Subject ($hostname + 'Test mail') -SmtpServer "smtpserver.domain.com"
```




