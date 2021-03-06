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
***
```powershell
PS /root/projects/perl_one_liners> Get-Date

Thursday, 02 April 2020 09:44:37

```
## How to calculate the total value of third field in all the records?
```powershell
PS /root/projects/perl_one_liners> Get-Content names.txt | %{ [int]$total+=$_.Split(',')[2]; } ; Write-Host "Total: $total" 
Total: 230831
PS /root/projects/perl_one_liners>
```
## How to get number of fields in each record
```powershell
PS /root/projects/perl_one_liners> Get-Content ./names.txt | %{ $a=$_.Split(','); Write-Host "Num of field" $a[0]"="$a.length; }
Num of field 1 = 8
Num of field 2 = 8
Num of field 3 = 8
Num of field 4 = 8
PS /root/projects/perl_one_liners>
```
## Find and replace command
1) **Using Get-Content to read the file and returned the contents to the console, then use replace command to modify the file content (as shown below).**
```powershell
PS /root/projects/perl_one_liners> cat ./names.txt
1,Tony Passaquale,7920,20090222 21:59:00,800,4.78,3824,Follow-up
2,Nigel Shan Shanford,30316,20090405 16:34:00,400,9.99,3996,New-Opportunity
3,Selma Cooper,97455,20090405 16:31:00,1000,9.99,9990,Pre-Approach
4,Allen James,95140,20090405 16:31:00,1000,9.99,9990,New-Opportunity
PS /root/projects/perl_one_liners> ((Get-Content ./names.txt) -replace 'Selma','Sheldon')
1,Tony Passaquale,7920,20090222 21:59:00,800,4.78,3824,Follow-up
2,Nigel Shan Shanford,30316,20090405 16:34:00,400,9.99,3996,New-Opportunity
3,Sheldon Cooper,97455,20090405 16:31:00,1000,9.99,9990,Pre-Approach
4,Allen James,95140,20090405 16:31:00,1000,9.99,9990,New-Opportunity
```
2) **Now that we have the code to find and replace the string we're after, it's now time to modify the file itself. We can do that by using Set-Content.**
```powershell
PS /root/projects/perl_one_liners> ((Get-Content ./names.txt) -replace 'Sheldon','Selma') | Set-Content ./names.txt
PS /root/projects/perl_one_liners> cat ./names.txt
1,Tony Passaquale,7920,20090222 21:59:00,800,4.78,3824,Follow-up
2,Nigel Shan Shanford,30316,20090405 16:34:00,400,9.99,3996,New-Opportunity
3,Selma Cooper,97455,20090405 16:31:00,1000,9.99,9990,Pre-Approach
4,Allen James,95140,20090405 16:31:00,1000,9.99,9990,New-Opportunity
PS /root/projects/perl_one_liners>
```

***
```powershell
PS /root/projects/perl_one_liners> Get-Date

Saturday, 04 April 2020 10:32:44

PS /root/projects/perl_one_liners> (Get-Date).Day
Day        DayOfWeek  DayOfYear  
PS /root/projects/perl_one_liners> (Get-Date).DayOfWeek
Saturday
PS /root/projects/perl_one_liners> (Get-Date).Day      
4
PS /root/projects/perl_one_liners> Get-ChildItem              


    Directory: /root/projects/perl_one_liners

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-----          04/04/2020    10:28             90 hello-world.ps1
-----          04/02/2020    09:36            277 names.txt
-----          03/31/2020    06:12           1430 test.txt
-----          03/31/2020    06:25           1452 test2.txt

PS /root/projects/perl_one_liners> Get-ChildItem | Format-    
Format-Custom  Format-Hex     Format-List    Format-Table   Format-Wide    
PS /root/projects/perl_one_liners> Get-ChildItem | Format-Table


    Directory: /root/projects/perl_one_liners

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-----          04/04/2020    10:28             90 hello-world.ps1
-----          04/02/2020    09:36            277 names.txt
-----          03/31/2020    06:12           1430 test.txt
-----          03/31/2020    06:25           1452 test2.txt

PS /root/projects/perl_one_liners> Get-ChildItem | Format-Wide 


    Directory: /root/projects/perl_one_liners

hello-world.ps1                                                                   names.txt
test.txt                                                                          test2.txt

PS /root/projects/perl_one_liners> cat ./hello-world.ps1
write-Host "Hello World"
$fn = $args[0]
$ln = $args[1]

Write-Host "Good morning $fn $ln"
PS /root/projects/perl_one_liners> ./hello-world.ps1 Shruti Sharma
Hello World
Good morning Shruti Sharma
PS /root/projects/perl_one_liners>
```