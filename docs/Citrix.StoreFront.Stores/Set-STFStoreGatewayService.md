#Set-STFStoreGatewayService
Set the gateway service settings for a Store
##Syntax
```
```
##Detailed Description
Set the gateway service settings for a Store.
##Related Commands
*[Get-STFStoreGatewayService](Get-STFStoreGatewayService)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
###System.Boolean
Parameter Enabled: The .NET 'System.Boolean' value type
###System.String
Parameter CustomerId: The .NET 'System.String' reference type
###System.String
Parameter GetGatewayServiceUrl: The .NET 'System.String' reference type
###System.String
Parameter PrivateKey: The .NET 'System.String' reference type
###System.String
Parameter ServiceName: The .NET 'System.String' reference type
###System.String
Parameter InstanceId: The .NET 'System.String' reference type
###System.String
Parameter SecureTicketAuthorityUrl: The .NET 'System.String' reference type
###System.TimeSpan
Parameter SecureTicketLifetime: The .NET 'System.TimeSpan' value type
###System.Boolean
Parameter SessionReliability: The .NET 'System.Boolean' value type
###System.Management.Automation.SwitchParameter
Parameter PassThru: The .NET 'System.Management.Automation.SwitchParameter' value type
##Return Values
###StoreGateway
The .NET 'Citrix.StoreFront.Model.Store.StoreGateway' reference type
##Examples
###EXAMPLE 1 Set gateway service settings for a Store
```
```
