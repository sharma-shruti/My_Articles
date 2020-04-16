# Powershell and XML


## Cmdlets

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
```