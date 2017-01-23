#Get-STFCitrixAGBasicOptions
Get the CitrixAGBasic protocol options
##Syntax
```
```
##Detailed Description
Get the CitrixAGBasic Authentication service protocol options.
##Related Commands
*[Set-STFCitrixAGBasicOptions](Set-STFCitrixAGBasicOptions)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Authentication.AuthenticationService
Parameter AuthenticationService: A .NET class representing the configuration of a StoreFront Authentication service
##Return Values
###NetscalerAuthentication
The .NET 'Citrix.StoreFront.Model.Authentication.NetscalerAuthentication' reference type
##Examples
###EXAMPLE 1 Get CitrixAGBasic protocol options
```
Get-STFCitrixAGBasicOptions -AuthenticationService $authentication
```
REMARKS
Get the CitrixAGBasic options from the specified Authentication service
OUTPUT
```
------------------------ -----------------
            Password {}
```