#Remove-STFUserFarmMapping
Remove a UserFarmMapping from the Store
##Syntax
```
Remove-STFUserFarmMapping [-Name] <String> [-StoreService] <StoreService> [<CommonParameters>]
```
##Detailed Description
Remove the UserFarmMapping configured for or Store.
##Related Commands
*[Set-STFUserFarmMapping](Set-STFUserFarmMapping)
*[Get-STFUserFarmMapping](Get-STFUserFarmMapping)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
###Citrix.StoreFront.Model.Store.UserFarmMapping
Parameter UserFarmMapping: The .NET 'Citrix.StoreFront.Model.Store.UserFarmMapping' reference type
###System.String
Parameter Name: The .NET 'System.String' reference type
##Return Values
##Examples
###EXAMPLE 1 Remove a UserFarmMapping
```
Remove-STFUserFarmMapping -StoreService $store -Name "EUMapping"
```
REMARKS
Remove the EUMapping from the UserFarmMappings for the Store service
/Citrix/Store.
