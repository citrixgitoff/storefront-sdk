#Get-STFExplicitAuthenticator
Get the password validator
##Syntax
```
```
##Detailed Description
Gets the password validator configuration.
##Related Commands
*[Set-STFExplicitAuthenticator](Set-STFExplicitAuthenticator)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Authentication.AuthenticationService
Parameter AuthenticationService: A .NET class representing the configuration of a StoreFront Authentication service
##Return Values
###String
The .NET 'System.String' reference type
##Examples
###EXAMPLE 1 Get Password Validator settings
```
Get-STFExplicitAuthenticator -AuthenticationService $auth
```
REMARKS
Get the password validator settings for the Authentication service.
