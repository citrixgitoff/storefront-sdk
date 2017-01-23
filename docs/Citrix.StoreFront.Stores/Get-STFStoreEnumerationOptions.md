#Get-STFStoreEnumerationOptions
Get Store enumeration options
##Syntax
```
```
##Detailed Description
Get the Store options used when enumerating the XenApp and XenDesktop xml services.
##Related Commands
*[Set-STFStoreEnumerationOptions](Set-STFStoreEnumerationOptions)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
##Return Values
###Enumeration
A .NET class representing the configuration of Enumeration settings in a StoreFront Store service
##Examples
###EXAMPLE 1 Get Store enumeration settings
```
Get-STFStoreEnumerationOptions -StoreService $storeservice
```
REMARKS
Get the enumeration setting from the Store
OUTPUT
```
MaximumConcurrentEnumerations                : 0
MinimumFarmsRequiredForConcurrentEnumeration : 3
RequestFullIconData                          : FullAndMulti
RequestedHighColorIcons                      : {[small, 16], [medium, 32], 
[large, 48]}
FilterByTypesInclude                         :
FilterByKeywordsInclude                      :
FilterByKeywordsExclude                      :
```