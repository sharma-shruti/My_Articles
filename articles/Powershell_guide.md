## Learning  Powershell

The Help command doesn’t search for cmdlets; it searches for help topics. Because every cmdlet has a help file, we could say that this search retrieves the same results. But you can also directly search for cmdlets by using the Get-Command cmdlet (or its alias, Gcm).

PS /root> Get-Command -Noun service
PS /root> get-service
get-service: The term 'get-service' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
PS /root>

PS /root> Get-Help Get-Service
Get-Help: Get-Help could not find Get-Service in a help file in this session. To download updated help topics type: "Update-Help". To get help online, search for th
e help topic in the TechNet library at https://go.microsoft.com/fwlink/?LinkID=107116.                                                                              
PS /root>