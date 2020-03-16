Get-Date //This command is used to display date

Get-TimeZone //This command is used to display timezone

Start-Transcript // Used to maintain history of all the changes made at that instance/session

Get-Command //all the functions available for us in powershell.

All the commands in powershell are written in the form of verb-noun or action-object
For example: When we run the following command we will get a list of all the commands having noun as "string"
PS /Users/ashwarybhatt/Documents/GIT/My_Articles> Get-Command -noun string


CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Join-String                                        7.0.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-String                                         7.0.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-String                                      7.0.0.0    Microsoft.PowerShell.Utility

PS /Users/ashwarybhatt/Documents/GIT/My_Articles>



Get-Help Get-Date //get-help is like a manual that provides details of every command 
PS /Users/ashwarybhatt/Documents/GIT/My_Articles> Get-Help Get-Date

NAME
    Get-Date
    
SYNTAX
    Get-Date [[-Date] <datetime>] [-Year <int>] [-Month <int>] [-Day <int>] [-Hour <int>] [-Minute <int>] [-Second <int>] [-Millisecond <int>] [-DisplayHint {Date 
    | Time | DateTime}] [-Format <string>] [<CommonParameters>]
    
    Get-Date [[-Date] <datetime>] [-Year <int>] [-Month <int>] [-Day <int>] [-Hour <int>] [-Minute <int>] [-Second <int>] [-Millisecond <int>] [-DisplayHint {Date 
    | Time | DateTime}] [-UFormat <string>] [<CommonParameters>]


    
        
Powershell does allow you to use alias but it is a good practice to use the correct format i.e verb-noun when working with powershell.
Example: Instead of using cls, we should use clear-host 
PS /Users/ashwarybhatt/Documents/GIT/My_Articles> Get-Alias cls       


CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           cls -> Clear-Host                                             

PS /Users/ashwarybhatt/Documents/GIT/My_Articles>