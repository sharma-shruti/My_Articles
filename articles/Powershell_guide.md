# Learning  Powershell

## PowerShell is a command-line shell and scripting language that aims to help administrators and power-users rapidly automate tasks.
With the help of these three cmdlets, you can find, explore, and leverage the others to perform a wide variety of tasks.
1. **Get-Command** – this cmdlet can be used to display available commands.
``` powershell
S /root> Get-Command *process*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Debug-Process                                      7.0.0.0    Microsoft.PowerShell.Management
Cmdlet          Enter-PSHostProcess                                7.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Exit-PSHostProcess                                 7.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-Process                                        7.0.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-PSHostProcessInfo                              7.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Start-Process                                      7.0.0.0    Microsoft.PowerShell.Management
Cmdlet          Stop-Process                                       7.0.0.0    Microsoft.PowerShell.Management
Cmdlet          Wait-Process                                       7.0.0.0    Microsoft.PowerShell.Management

PS /root>
```
2. **Get-Help** - It provides information about what a cmdlet does, and how it can be used.
```powershell
PS /root> Get-Help Start-Process

NAME
    Start-Process
    
SYNTAX
    Start-Process [-FilePath] <string> [[-ArgumentList] <string[]>] [-Credential <pscredential>] [-WorkingDirectory <string>] [-LoadUserProfile] [-NoNewWindow] [-P
    assThru] [-RedirectStandardError <string>] [-RedirectStandardInput <string>] [-RedirectStandardOutput <string>] [-WindowStyle {Normal | Hidden | Minimized | Ma
    ximized}] [-Wait] [-UseNewEnvironment] [-WhatIf] [-Confirm] [<CommonParameters>]
    
    Start-Process [-FilePath] <string> [[-ArgumentList] <string[]>] [-WorkingDirectory <string>] [-PassThru] [-Verb <string>] [-WindowStyle {Normal | Hidden | Mini
    mized | Maximized}] [-Wait] [-WhatIf] [-Confirm] [<CommonParameters>]
    

ALIASES
    saps
    

REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help Start-Process -Online" or
           go to https://go.microsoft.com/fwlink/?LinkID=2097141.


PS /root>
```
3. **Get-Member** - PowerShell deals with objects. Get-Member serves to help you identify what type of objects you are dealing with when using PowerShell and also what properties and methods are available to that object.
```powershell
PS /root> Get-Date | Get-Member


   TypeName: System.DateTime

Name                 MemberType     Definition
----                 ----------     ----------
Add                  Method         datetime Add(timespan value)
AddDays              Method         datetime AddDays(double value)
AddHours             Method         datetime AddHours(double value)
AddMilliseconds      Method         datetime AddMilliseconds(double value)
AddMinutes           Method         datetime AddMinutes(double value)
AddMonths            Method         datetime AddMonths(int months)
AddSeconds           Method         datetime AddSeconds(double value)
AddTicks             Method         datetime AddTicks(long value)
```
*This indicates that Get-Date returns a System.DateTime object, which contains many properties, such as Date, Day, Hour, Second, etc.*

## Practicing powershell one-liner commands 
```powershell
PS /root/projects/perl_one_liners> Get-Date

Wednesday, 01 April 2020 10:52:31

PS /root/projects/perl_one_liners> cat ./names.txt                               
1,Tony Passaquale,7920,20090222 21:59:00,800,4.78,3824,Follow-up
2,Nigel Shan Shanford,30316,20090405 16:34:00,400,9.99,3996,New-Opportunity
3,Selma Cooper,97455,20090405 16:31:00,1000,9.99,9990,Pre-Approach
4,Allen James,95140,20090405 16:31:00,1000,9.99,9990,New-Opportunity
PS /root/projects/perl_one_liners> Get-Content ./names.txt | %{$_.Split(',')[0];}
1
2
3
4
PS /root/projects/perl_one_liners> Get-Content ./names.txt | %{$_.Split(',')[1];}
Tony Passaquale
Nigel Shan Shanford
Selma Cooper
Allen James
PS /root/projects/perl_one_liners>
```
## How to print multiple columns side by side.
```powershell
PS /root/projects/perl_one_liners> Get-Content ./names.txt | %{$_.Split(',')[0,1];}
1
Tony Passaquale
2
Nigel Shan Shanford
3
Selma Cooper
4
Allen James
PS /root/projects/perl_one_liners> Get-Content ./names.txt | foreach { Write-Host $_.Split(',')[0,1];}
1 Tony Passaquale
2 Nigel Shan Shanford
3 Selma Cooper
4 Allen James
PS /root/projects/perl_one_liners> Get-Content ./names.txt | foreach { Write-Host $_.Split(',')[0,1,7];} 
1 Tony Passaquale Follow-up
2 Nigel Shan Shanford New-Opportunity
3 Selma Cooper Pre-Approach
4 Allen James New-Opportunity
PS /root/projects/perl_one_liners>
```
