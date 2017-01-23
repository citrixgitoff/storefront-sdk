#Publish-STFServerGroupConfiguration
Publish the configuration from the server to the group
##Syntax
```
```
##Detailed Description
Publishes the configuration of the server on which the command is executed to the other servers within the group.
##Related Commands
*[Wait-STFPublishServerGroupConfiguration](Wait-STFPublishServerGroupConfiguration)
##Parameters
|Name|Description|Required?|Pipeline Input|
###System.Management.Automation.SwitchParameter
Parameter AsBackgroundJob: The .NET 'System.Management.Automation.SwitchParameter' value type
##Return Values
###SynchronisationState
The .NET 'Citrix.DeliveryServices.ConfigurationReplication.Contract.ServiceStatus.SynchronisationState' reference type
##Examples
###EXAMPLE 1 Publish configuration without progress
```
Write-Host 'Publish is going on in the background'
```
REMAR
```




Publishes the configuration to servers within the group as a background job. A 
message is output without waiting for publish to complete.
```