# Powershell and XML


## Cmdlets
```powershell
PS /root/projects/perl_one_liners> Get-Command *xml*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          ConvertTo-Xml                                      7.0.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-Clixml                                      7.0.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Clixml                                      7.0.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-Xml                                         7.0.0.0    Microsoft.PowerShell.Utility
Application     iptables-xml                                       0.0.0.0    /usr/bin/iptables-xml

PS /root/projects/perl_one_liners>
```
* Select-Xml -  Supports XPath queries to search for text in XML strings and documents.

(*Note : XPath (XML Path Language) is a query language for selecting nodes from an XML document.*)
* ConvertTo-Xml - Creates an XML-based representation of an object. To use this cmdlet, pipe one or more objects to the cmdlet, or use the InputObject parameter to specify the object. 

Sample XML file 
```xml
<?xml version="1.0"?>
<catalog>
   <book id="bk101">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <publish_date>2000-10-01</publish_date>
      <description>An in-depth look at creating applications 
      with XML.</description>
   </book>
</catalog>
```
```powershell
$x = [xml](Get-Content ./books.xml)
$x.GetType()
$x
$x.catalog
$x.catalog.book
$x.catalog.book.title
$x.catalog.book |Select-Object title,author,price
$x.SelectNodes("//title")
PS /root/projects/perl_one_liners> $x.SelectSingleNode("//book[6]")

id           : bk106
author       : Randall, Cynthia
title        : Lover Birds
genre        : Romance
price        : 4.95
publish_date : 2000-09-02
description  : When Carla meets Paul at an ornithology 
                     conference, tempers fly as feathers get ruffled.


$x.catalog.book |Format-Table
```
# How to parse a URL from a text file

```
set-Content -path ./New.txt -value "" 
$Text = Get-Content ./node.txt
$URLString = ((Select-String -AllMatches '(http[s]?)(:\/\/)([^\s,]+)(?=")' -Input $Text).Matches.Value)
$URLString | ForEach-Object {
[system.uri]$URL = $_
$Token = ($URL.Query -split 'wvideo=')[1]
$Token = "youtube-dl https://fast.wistia.net/embed/iframe/" + $Token
Add-Content $Token -path ./New.txt
}
Get-Content ./New.txt |Sort-Object -Unique |Set-Content -Path ./New.txt

```