#Set-STFRoamingBeacon
Set the internal and external beacons
##Syntax
```
Set-STFRoamingBeacon [-Internal <Uri>] [-External <Uri[]>] [-Internal] <Uri> [<CommonParameters>]
Set-STFRoamingBeacon [-External] <Uri[]> [-Internal] <Uri> [<CommonParameters>]
Set-STFRoamingBeacon [-RefreshServiceRecordOnly] <SwitchParameter> [-Internal] <Uri> [<CommonParameters>]
```
##Detailed Description
Configure the internal and external roaming beacons.
##Related Commands
##Parameters
|Name|Description|Required?|Pipeline Input|
###System.Uri
Parameter Internal: The .NET 'System.Uri' reference type
###System.Uri[]
Parameter External: The .NET 'System.Uri' reference type
###System.Management.Automation.SwitchParameter
Parameter RefreshServiceRecordOnly: The .NET 'System.Management.Automation.SwitchParameter' value type
##Return Values
##Examples
###EXAMPLE 1 Set the internal beacon
```
```
REMARKS
Set the internal beacon to http://myinternalbeacon.com.

```
```
REMARKS
Set the external beacons to http://external1.com and http://external2.com.
