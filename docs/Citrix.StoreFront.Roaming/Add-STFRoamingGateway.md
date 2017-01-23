#Add-STFRoamingGateway
Add a new Gateway that can be used for remote access and authentication.
##Syntax
```
Add-STFRoamingGateway [-Name] <String> [-LogonType] <UsedForHDXOnly | Domain | RSA | DomainAndRSA | SMS | GatewayKnows | SmartCard | None> [[-SmartCardFallbackLogonType] <UsedForHDXOnly | Domain | RSA | DomainAndRSA | SMS | GatewayKnows | SmartCard | None>] [[-Version] <Version10_0_69_4 | Version9x>] [-GatewayUrl] <Uri> [[-CallbackUrl] <Uri>] [[-SessionReliability] <SwitchParameter>] [[-RequestTicketTwoSTAs] <SwitchParameter>] [[-SubnetIPAddress] <String>] [[-SecureTicketAuthorityUrls] <Uri[]>] [[-StasUseLoadBalancing] <SwitchParameter>] [[-StasBypassDuration] <TimeSpan>] [[-PassThru] <SwitchParameter>] [<CommonParameters>]
```
##Detailed Description
Add a new Gateway to the global gateway list. Gateways for remote access and authentication are added to Stores from the globally managed list.
##Related Commands
*[Get-STFRoamingGateway](Get-STFRoamingGateway)
*[Remove-STFRoamingGateway](Remove-STFRoamingGateway)
*[Set-STFRoamingGateway](Set-STFRoamingGateway)
*[New-STFRoamingGateway](New-STFRoamingGateway)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Roaming.RoamingGateway
Parameter RoamingGateway: The .NET 'Citrix.StoreFront.Model.Roaming.RoamingGateway' reference type
###System.String
Parameter Name: The .NET 'System.String' reference type
###Citrix.StoreFront.Model.Roaming.GatewayLogonType
Parameter LogonType: The .NET 'Citrix.StoreFront.Model.Roaming.GatewayLogonType' value type
###Citrix.StoreFront.Model.Roaming.GatewayLogonType
Parameter SmartCardFallbackLogonType: The .NET 'Citrix.StoreFront.Model.Roaming.GatewayLogonType' value type
###Citrix.StoreFront.Model.Roaming.GatewayVersion
Parameter Version: The .NET 'Citrix.StoreFront.Model.Roaming.GatewayVersion' value type
###System.Uri
Parameter GatewayUrl: The .NET 'System.Uri' reference type
###System.Uri
Parameter CallbackUrl: The .NET 'System.Uri' reference type
###System.Management.Automation.SwitchParameter
Parameter SessionReliability: The .NET 'System.Management.Automation.SwitchParameter' value type
###System.Management.Automation.SwitchParameter
Parameter RequestTicketTwoSTAs: The .NET 'System.Management.Automation.SwitchParameter' value type
###System.String
Parameter SubnetIPAddress: The .NET 'System.String' reference type
###System.Uri[]
Parameter SecureTicketAuthorityUrls: The .NET 'System.Uri' reference type
###System.Management.Automation.SwitchParameter
Parameter StasUseLoadBalancing: The .NET 'System.Management.Automation.SwitchParameter' value type
###System.TimeSpan
Parameter StasBypassDuration: The .NET 'System.TimeSpan' value type
###System.Management.Automation.SwitchParameter
Parameter PassThru: The .NET 'System.Management.Automation.SwitchParameter' value type
##Return Values
##Examples
###EXAMPLE 1 Add Version 10x Gateway
```
```
REMARKS
Add a version 10 or greater Gateway.

```
```
REMARKS
Add a version 9 Gateway.
