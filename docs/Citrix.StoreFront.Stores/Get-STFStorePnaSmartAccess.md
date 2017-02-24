#Get-STFStorePnaSmartAccess
Get the SmartAccess settings
##Syntax
```
```
##Detailed Description
Get the servers and certificates that are used to supply and verify SmartAccess conditions in PNA headers. The certificate thumbprint references a certificate in the Delivery Services certificate store. The cerificate is used to verify the signed headers to ensure a trusted source.
##Related Commands
*[Grant-STFStorePnaSmartAccess](Grant-STFStorePnaSmartAccess)
*[Revoke-STFStorePnaSmartAccess](Revoke-STFStorePnaSmartAccess)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Store.StoreService
Parameter StoreService: A .NET class representing the configuration of a StoreFront Store service
##Return Values
###AccessConditionsTrustSettings
The .NET 'Citrix.StoreFront.Model.Store.AccessConditionsTrustSettings' reference type
##Examples
###EXAMPLE 1 Get SmartAccess trust settings
```
Get-STFStorePnaSmartAccess -StoreService $store
```
REMARKS
Gets the trusted server name, certificates and validity period.
OUTPUT
```
AccessConditionsTrusts: {MyXenMobile}
```