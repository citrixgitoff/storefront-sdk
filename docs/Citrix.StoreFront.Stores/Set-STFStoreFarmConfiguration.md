#Set-STFStoreFarmConfiguration
Configure common Store farm options
##Syntax
```
```
##Detailed Description
Configure Store wide settings common to all configured farms.
##Related Commands
*[Set-STFStoreLaunchOptions](Set-STFStoreLaunchOptions)
*[Get-STFStoreLaunchOptions](Get-STFStoreLaunchOptions)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
###System.Boolean
Parameter EnableFileTypeAssociation: The .NET 'System.Boolean' value type
###System.TimeSpan
Parameter CommunicationTimeout: The .NET 'System.TimeSpan' value type
###System.TimeSpan
Parameter ConnectionTimeout: The .NET 'System.TimeSpan' value type
###System.TimeSpan
Parameter LeasingStatusExpiryFailed: The .NET 'System.TimeSpan' value type
###System.TimeSpan
Parameter LeasingStatusExpiryLeasing: The .NET 'System.TimeSpan' value type
###System.TimeSpan
Parameter LeasingStatusExpiryPending: The .NET 'System.TimeSpan' value type
###System.Boolean
Parameter PooledSockets: The .NET 'System.Boolean' value type
###System.Int32
Parameter ServerCommunicationAttempts: The .NET 'System.Int32' value type
###System.TimeSpan
Parameter BackgroundHealthCheckPollingPeriod: The .NET 'System.TimeSpan' value type
###System.Boolean
Parameter AdvancedHealthCheck: The .NET 'System.Boolean' value type
##Return Values
##Examples
###EXAMPLE 1 Enable pooled sockets
```
Set-STFStoreFarmConfiguration $storeService -PooledSockets $true
```
REMARKS
Enable pooled sockets on the only configured store service

```
Set-STFStoreFarmConfiguration $storeService -EnableFileTypeAssociation $false
```
REMARKS
Disables FTA, file type association for the only configured Store service.
