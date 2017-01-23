#Get-STFUserFarmMapping
Get the UserFarmMappings for a Store
##Syntax
```
```
##Detailed Description
Get the UserFarmMappings configured for a Store or a specific UserFarmMapping matching the supplied name.
##Related Commands
*[Set-STFUserFarmMapping](Set-STFUserFarmMapping)
*[Clear-STFUserFarmMappings](Clear-STFUserFarmMappings)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
###System.String
Parameter Name: The .NET 'System.String' reference type
##Return Values
###UserFarmMapping
The .NET 'Citrix.StoreFront.Model.Store.UserFarmMapping' reference type
##Examples
###EXAMPLE 1 Get all UserFarmMappings
```
```
REMARKS
Gets all existing UserFarmMappings on the Store service $store.

```
```
REMARKS
Gets the EUUsers UserFarmMapping from the Store $store.
