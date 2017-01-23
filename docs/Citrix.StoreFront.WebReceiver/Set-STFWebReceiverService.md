#Set-STFWebReceiverService
Configure Receiver for Web
##Syntax
```
```
##Detailed Description
Configure Receiver for Web service options.
##Related Commands
##Parameters
|Name|Description|Required?|Pipeline Input|
###Citrix.StoreFront.Model.ReceiverForWeb.WebReceiverService
Parameter WebReceiverService: A .NET class representing the configuration of a StoreFront Web Receiver service
###System.Boolean
Parameter ClassicReceiverExperience: The .NET 'System.Boolean' value type
###System.Management.Automation.SwitchParameter
Parameter DefaultIISSite: The .NET 'System.Management.Automation.SwitchParameter' value type
###System.Management.Automation.SwitchParameter
Parameter PassThru: The .NET 'System.Management.Automation.SwitchParameter' value type
##Return Values
##Examples
###EXAMPLE 1 Set Receiver for Web options
```
Set-STFWebReceiverService $rfw -CommunicationAttempts 2 -ShowDesktopViewer $false
```
REMARKS
Configure the number of communication attempts to two and disable the desktop
viewer on the only configured Receiver for Web service.
