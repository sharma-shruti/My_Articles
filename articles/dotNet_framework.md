# .NET Framework

.NET Framework is a programming infrastructure created by Microsoft for building, deploying, and running applications and services that use .NET technologies, such as desktop applications and Web services. The .NET framework can work with several programming languages such as C#, VB .NET, C++ and F#.

It has several key features, such as support for multiple programming languages, [asynchronous and concurrent programming models](https://docs.microsoft.com/en-us/dotnet/standard/parallel-programming/tpl-and-traditional-async-programming), and [native interoperability](https://docs.microsoft.com/en-us/dotnet/standard/native-interop/), which enable a wide range of scenarios across multiple platforms. 

.NET languages are object-oriented with hierarchies of base and derived classes. 
* A class is basically an object (an instance of a specific type), which can contain various members such as properties, methods and events. 
* A class enables you to create your own custom types by grouping together variables of other types, methods and events. 
* Methods are functions that operate exclusively on objects of a class. 
* A program only calls the methods belonging to a given type. All other calls result in either a compile-time error or a run-time exception.

# How to use dotNET (.NET) classes and methods in PowerShell

A hierarchical namespace organizes classes. This allows you to locate a class in the .NET framework through a fully qualified name. For instance, the fully qualified name of the process class is System.Diagnostics.Process.

Let us take a look at some of the examples.

1. In PowerShell, Get-TimeZone cmdlet gets the current time zone. Its equivalent .NET Framework class provides exactly the same output. 

```powershell
PS /root> Get-TimeZone

Id                         : Etc/UTC
DisplayName                : (UTC+00:00) GMT
StandardName               : GMT
DaylightName               : GMT
BaseUtcOffset              : 00:00:00
SupportsDaylightSavingTime : True
```
In order to find .NET framework object type for checking the TimeZone, we use Get-Member cmdlet in PowerShell. The Get-Member cmdlet gets the members, the properties and methods, of objects (as shown below).
```powershell
PS /root> Get-TimeZone |gm


   TypeName: System.TimeZoneInfo

Name                       MemberType Definition
----                       ---------- ----------
Equals                     Method     bool Equals(System.TimeZoneInfo other), bool Equals(System.Object obj), bool IEquatable[TimeZoneInfo].Equals(System.TimeZoneInfo other)
GetAdjustmentRules         Method     System.TimeZoneInfo+AdjustmentRule[] GetAdjustmentRules()
GetAmbiguousTimeOffsets    Method     timespan[] GetAmbiguousTimeOffsets(System.DateTimeOffset dateTimeOffset), timespan[] GetAmbiguousTimeOffsets(datetime dateTime)
...
...
IsDaylightSavingTime       Method     bool IsDaylightSavingTime(System.DateTimeOffset dateTimeOffset), bool IsDaylightSavingTime(datetime dateTime)
IsInvalidTime              Method     bool IsInvalidTime(datetime dateTime)
BaseUtcOffset              Property   timespan BaseUtcOffset {get;}
DaylightName               Property   string DaylightName {get;}
DisplayName                Property   string DisplayName {get;}
Id                         Property   string Id {get;}
StandardName               Property   string StandardName {get;}
SupportsDaylightSavingTime Property   bool SupportsDaylightSavingTime {get;}

PS /root>
```

Here [System.TimeZoneInfo] is a .NET class which gives the same output.
```powershell
PS /root> [System.TimeZoneInfo]::local

Id                         : Etc/UTC
DisplayName                : (UTC+00:00) GMT
StandardName               : GMT
DaylightName               : GMT
BaseUtcOffset              : 00:00:00
SupportsDaylightSavingTime : True
PS /root>
```
2. Similarly, we can follow the same steps to check the Date and its equivalent .Net class.

```powershell
PS /root> Get-Date              

Saturday, 25 April 2020 13:53:05

PS /root> Get-Date | Get-Member 


   TypeName: System.DateTime

Name                 MemberType     Definition
----                 ----------     ----------
Add                  Method         datetime Add(timespan value)
AddDays              Method         datetime AddDays(double value)
AddHours             Method         datetime AddHours(double value)
AddMilliseconds      Method         datetime AddMilliseconds(double value)
AddMinutes           Method         datetime AddMinutes(double value)
....
....
PS /root> [System.DateTime]::now

Saturday, 25 April 2020 13:53:53

PS /root> 
```
3. It is always a best practice, to use a native Windows PowerShell cmdlet when it exists, unless there is compelling reason for not doing so.

One such example is using a static method within a .NET class. To determine the power of a number we make use of System.Math class and use the method Pow
```powershell
PS /root> [System.Math]::Pow(4,3)
64
PS /root> [system.Math]::
E                 Atan              Ceiling           Exp               Log2              Round             Tanh              
PI                Atan2             Clamp             Floor             Max               ScaleB            Truncate          
Abs               Atanh             CopySign          FusedMultiplyAdd  MaxMagnitude      Sign              
Acos              BigMul            Cos               IEEERemainder     Min               Sin               
Acosh             BitDecrement      Cosh              ILogB             MinMagnitude      Sinh              
Asin              BitIncrement      DivRem            Log               Pow               Sqrt              
Asinh             Cbrt              Equals            Log10             ReferenceEquals   Tan               
PS /root>
```
In this scenario, we are calling .net framework static method of a class to do something that we couldn't do in PowerShell natively. Although, we could write a function in powershell, that uses this approach.
