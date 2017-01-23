#Get-STFExplicitCommonOptions
Get the ExplicitCommon protocol options
##Syntax
```
```
##Detailed Description
Get the ExplicitCommon Authentication service protocol options.
##Related Commands
*[Set-STFExplicitCommonOptions](Set-STFExplicitCommonOptions)
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.Authentication.AuthenticationService
Parameter AuthenticationService: A .NET class representing the configuration of a StoreFront Authentication service
##Return Values
###ExplicitBL
The .NET 'Citrix.StoreFront.Model.Authentication.ExplicitBL' reference type
##Examples
###EXAMPLE 1 Get ExplicitCommon protocol options
```
Get-STFExplicitCommonOptions - AuthenticationService $authentication
```
REMARKS
Get the ExplicitCommon options from the specified Authentication service
OUTPUT
```
HideDomainField             : True
AllowUserPasswordChange     : Never
AllowZeroLengthPassword     : False
ShowPasswordExpiryWarning   : Windows
PasswordExpiryWarningPeriod : 10
RequireAccountSIDs          : True
DomainSelection             : {}
```