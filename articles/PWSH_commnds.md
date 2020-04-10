# Learn Powershell scripting 


```powershell
## Today's Date
PS /root/projects/perl_one_liners> Get-Date                 

Wednesday, 08 April 2020 10:28:17

PS /root/projects/perl_one_liners> $PSVersionTable.PSVersion

Major  Minor  Patch  PreReleaseLabel BuildLabel
-----  -----  -----  --------------- ----------
7      0      0                      

PS /root/projects/perl_one_liners>
PS /root> $Host

Name             : ConsoleHost
Version          : 7.0.0
InstanceId       : 160da9c1-7af0-4434-8cc8-eb5cb95e759a
UI               : System.Management.Automation.Internal.Host.InternalHostUserInterface
CurrentCulture   : 
CurrentUICulture : 
PrivateData      : Microsoft.PowerShell.ConsoleHost+ConsoleColorProxy
DebuggerEnabled  : True
IsRunspacePushed : False
Runspace         : System.Management.Automation.Runspaces.LocalRunspace

```
## $Error is an environment variable, which is an array of errors in a current session.
```Powershell
PS /root> $Error
PS /root>  
PS /root> buinouii
buinouii: The term 'buinouii' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
PS /root> 
PS /root> $var = Shruti
Shruti: The term 'Shruti' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
PS /root> $Error       

Shruti: The term 'Shruti' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

buinouii: The term 'buinouii' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
PS /root> 
```

## Trying to write a script to calculate numbers using variables.

```powershell
PS /root/projects/perl_one_liners> cat ./my_script.ps1

2000, 5000, 10000 | ForEach-Object -Process {"Divison $_ by 20 is"; ($_/20), "Multipliction $_ by 20 is"; ($_*20) }

Write-Host "Variable one is " $var1 = 5 -ForegroundColor blue

Write-Host "Variable second is" $var2 = 40 -ForegroundColor DarkMagenta

$a = $var1+$var2

Write-Host " Total = $a"


PS /root/projects/perl_one_liners> ./my_script.ps1
Divison 2000 by 20 is
100
Multipliction 2000 by 20 is
40000
Divison 5000 by 20 is
250
Multipliction 5000 by 20 is
100000
Divison 10000 by 20 is
500
Multipliction 10000 by 20 is
200000
Variable one is   = 5
Variable second is  = 40
 Total = 
PS /root/projects/perl_one_liners>
```
# Processing the CSV via command line 
```powershell
## Today's Date
PS /root/projects/perl_one_liners> Get-Date                                                                                                    

Thursday, 09 April 2020 11:02:41

## Read .csv file content
PS /root/projects/perl_one_liners> Get-Content ./data.cvs                                                                                      
Alex,3,M,6897907
Peter,56,M,6079227
Rita,38,F,9689787
Hema,20,F,7859766
John,67,M,6898078

## The Import-Csv cmdlet creates table-like custom objects from the items in CSV files.

PS /root/projects/perl_one_liners> Import-Csv ./data.cvs  -Delimiter "," -Header "Name", "Age", "Gender", "Phone"                              

Name  Age Gender Phone
----  --- ------ -----
Alex  3   M      6897907
Peter 56  M      6079227
Rita  38  F      9689787
Hema  20  F      7859766
John  67  M      6898078

## Select a column 

PS /root/projects/perl_one_liners> Import-Csv ./data.cvs  -Delimiter "," -Header "Name", "Age", "Gender", "Phone" |select NAme                 

Name
----
Alex
Peter
Rita
Hema
John

PS /root/projects/perl_one_liners> Import-Csv ./data.cvs  -Delimiter "," -Header "Name", "Age", "Gender", "Phone" |select Age                  

Age
---
3
56
38
20
67

## Save the output of the command to a file
PS /root/projects/perl_one_liners> Import-Csv ./data.cvs  -Delimiter "," -Header "Name", "Age", "Gender", "Phone" |select NAme > ./New_data.csv


PS /root/projects/perl_one_liners> Get-Content ./New_data.csv

Name
----
Alex
Peter
Rita
Hema
John

PS /root/projects/perl_one_liners>

# Read the csv file

PS /root/projects/perl_one_liners> Get-Content ./demo.csv
ERR036201       M       30/06/1965      1       1997.043836     0
ERR036213       F       30/06/1977      1       1997.112329     1
ERR036217       F       30/06/1948      1       1996.964481     1
ERR036222       M       30/06/1969      1       1997.172603     1
ERR036223       M       30/06/1936      1       1997.169863     1
ERR036230       M       15/02/1963      1       1997.287671     1
ERR036236       F       30/06/1971      1       1997.457534     1
ERR037473       M       30/06/1971      1       1997.961644     1
ERR037476       F       30/06/1964      1       1997.950685     0
ERR037489       F       15/12/1974      1       1998.054795     1
ERR037491       M       30/06/1961      1       1998.471233     1
ERR037496       F       30/06/1931      1       1998.358904     0
ERR037510       M       15/04/1945      1       1998.594521     0
ERR037511       M       15/08/1971      1       1998.473973     0
ERR037519       F       30/06/1946      1       1998.663014     1
ERR037520       F       15/10/1977      1       1998.726027     0
ERR037521       M       15/04/1962      1       1998.59726      1
ERR037523       M       15/06/1970      1       1998.843836     1
PS /root/projects/perl_one_liners>

#Select the column you want

PS /root/projects/perl_one_liners> Get-Content ./demo.csv | %{$_.Split("`t")[0]} | Set-Content ./New_data.csv
PS /root/projects/perl_one_liners> cat ./New_data.csv
ERR036201
ERR036213
ERR036217
ERR036222
ERR036223
ERR036230
ERR036236
ERR037473
ERR037476
ERR037489
ERR037491
ERR037496
ERR037510
ERR037511
ERR037519
ERR037520
ERR037521
ERR037523
```

