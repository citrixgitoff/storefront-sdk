# Requests
The following topics describe the requests available using the API. Each request is described, together with possible response codes and examples.

!!! tip "Note"
	In some examples, line breaks and white space have been added for readability.

## Client Configuration
Use this request to obtain the client configuration settings for the site. These settings define the behavior of the client and provide Web Proxy URLs for other services such as authentication and resource enumeration.

### Request

| URL                 | Method | Description                                                             |
|---------------------|--------|-------------------------------------------------------------------------|
| /Home/Configuration | GET    | Requests the client configuration, which is returned as an XML document |

| Response Code | Description                                     |
|---------------|-------------------------------------------------|
| 200           | Success                                         |
| 403           | Forbidden, due to one of the following reasons: |
|               |- Invalid CSRF token                             |             
|               |- Invalid X-Citrix-IsUsingHTTPS header           |

### Success Response Content
If a successful response (HTTP status code 200 OK) is returned, the response body contains an XML document describing the Citrix Receiver for Web configuration settings for the client, with root node `clientSettings`. For more information about the various configuration elements and attributes, see Using configuration elements on page 81.

####Response

```curl
Content-Length: 1592
```
##Session Keep Alive


|---|---|----|


|---|----|



HEAD http://webserver/Citrix/StoreWeb/Home/KeepAlive HTTP/1.1
PasswordChangeAllowed=
```
####Response
```curl
HTTP/1.1 200 OK
```
##Authentication Methods

|URL (indicative only)|Method|Description|
|---|----|---|

	* The client must first make a POST request to /Resources/List. Since the user is not yet 	authenticated, this returns a challenge in the form of a CitrixWebReceiver- Authenticate 	header with the GetAuthMethods URL in the location field.
For example:
```curl
CitrixWebReceiver-Authenticate:
```
!!! tip "Note"


|----|----|

|---|----|


|----|----|----|

###Example: Get Auth Methods
```curl
POST http://webserver/Citrix/StoreWeb/Authentication/
```
####Response
```curl
HTTP/1.1 200 OK
```
##Domain Pass-Through and Smart Card Authentication
|/DomainPassthroughAuth/ Login|POST|Authenticates the user using the credentials with which he or she logged on to the computer.|

	* Domain pass-through authentication requires the client browser to be running on 	Microsoft Windows. The caller must check the client platform OS prior to initiating pass-	through authentication.

###Response

|Response Code|Description|
|200|Success or failure.|
| |* The user attempts smart card authentication and cancels one of the browser prompts to insert a card, select a certificate, or enter a PIN.|
|403|Forbidden, due to one of the following reasons:|

|Response Format|Request Accept/Response Content-Type Header|
|---|----|

###Success Response Content

|Result|Yes|Value "success" or "failure".|





```curl
POST http://webserver/Citrix/StoreWeb/DomainPassthroughAuth/
20100101 Firefox/26.0
```
####Response
```curl
HTTP/1.1 401 Unauthorized
 <h2>401 - Unauthorized: Access is denied due to invalid
```
##Explicit Forms Authentication
Use this request to authenticate a user using explicit forms authentication. Explicit authentication, where the user enters credentials manually, is performed using the Citrix Common Forms Protocol. See the Citrix StoreFront API documentation for more information about Common Forms authentication.




|URL (indicative only)|Method|Accepts POST data|Description|
|-----|-----|----|----|

	* If the client omits to post any of the required data, the Authentication service rejects 	the form, resulting in a failed logon.

|Response Code|Description|
|---|----|

|XML|application/xml|


|-----|----|-----|
|TimeRemaining|No|The time remaining (in minutes) until the user's password expires. Only sent when authentication succeeds, password expiry notification is enabled and the user's password is due to expire within the configured time.|

`AuthenticateResponse` is an XML description of a form that is displayed to the user to collect additional information required for the authentication operation (typically, logon on change password). See the Common Forms Authentication documentation for information about the various form elements.

###Example: Explicit Authentication—Logon Form Returned 
####Request
Cookie: CtxsAuthMethod=ExplicitForms;
```
####Response
```curl
HTTP/1.1 200 OK
```
The client transforms the XML form description into an HTML representation, which is then dynamically added to the web page DOM. The above XML results in an HTML form consisting of a **User name** label and text input field, a **Password** label and password input field, and a **Log On** button.

The user types his or her credentials in the input fields and submits the form by clicking the **Log On** button.

The client intercepts the form submission and follows the Common Forms Authentication rules to build the form data to send back to the Web Proxy (to be forwarded to the Authentication service). The form is submitted to the PostBack URL; in this case Authentication/LoginAttempt. However, the user mistypes their password which results in the Authentication service returning another logon form XML document, this time highlighting the error with an additional Requirements node.
###Example: Explicit Authentication—Incorrect Credentials Submitted 
####Request
On&StateContext=
```
####Response
```curl
HTTP/1.1 200 OK
```

###Example: Explicit Authentication—Password Expired

On&StateContext=
```
####Response
```curl
HTTP/1.1 200 OK
  <Type>username</Type>
<Type>newpassword</Type>
```
When the user enters the requested information and submits the form, a further form is returned by the Authentication service for the user to confirm that their password has been successfully changed. Note that the request specifies the button id changePasswordBtn specified in the form above; failing to specify the correct button id results in the form being rejected. The confirmation form comprises simply of a text label and OK button.
```curl
POST http://webserver/Citrix/StoreWeb/ExplicitAuth/SendForm
CsrfToken=94FEF17799905C51ADD4599AC0056209;
```
####Response
```curl
HTTP/1.1 200 OK
	nticationRequirements>
```
After the user clicks the OK button, the confirmation form is submitted and a successful authentication response is obtained.
```
####Response
```curl
HTTP/1.1 200 OK
```

###Example: Explicit Authentication—Elective Change Password
On&StateContext=

  TimeRemaining>89</TimeRemaining>
The client may then provide an interface for the user to initiate an elective change password request at any time using the changeCredentials URL obtained from the Citrix Receiver for Web configuration at XPath /clientSettings/authManager. Requesting this URL initiates a Common Forms protocol conversation, in a similar way to /ExplicitAuth/ Login. If the user submits the form after entering invalid data (or omitting required data), further forms may be generated. The client must be prepared to receive multiple forms in succession and process these until either a success or failure response is received. If the password change is successful, a password confirmation form is returned; when the confirmation form is submitted a successful AuthenticationStatus response is returned. In other words, the change password conversation proceeds exactly as described in the example for the case where the user's password has expired at logon time.
```curl
POST http://webserver/Citrix/StoreWeb/Authentication/
```
####Response
<AuthenticateResponse xmlns="http://citrix.com/authentication/
<Text>
```
With elective change password the user has already authenticated to Citrix Receiver for Web. Since the change password request is not essential to access the site, the client UI should provide a Cancel button on the form. If the user chooses to cancel, the Web Proxy cancel post-back URL in the above form must be used to relay to the Authentication service that the request has been cancelled.
```curl
POST http://webserver/Citrix/StoreWeb/ExplicitAuth/CancelForm
```
####Response
response/1">
```
##Post Credentials Authentication
|-----------------------------|--------|----------------------------------------------------------------------------------------------------------------------------------|
| /PostCredentialsAuth/ Login | POST   | Authenticates the user using the credentials supplied in the POST body. The URL is returned by / Authentication/ GetAuthMethods. |

| POST parameter | Description                                                                                                                           |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------|
| username       | The username, including a domain specification if required, in either SAM or UPN format. For example, domain\fred or fred@some.domain |
| password       | The password.                                                                                                                         |

!!! tip "Note"
	* The Http Basic authentication method must be enabled for the Authentication service 	because the Web Proxy internally uses HttpBasic to authenticate the user to StoreFront.

|---------------|-------------------------------------------------|
| 200           | Success or failure                              |
| 400           | The username or password was not supplied.      |
| 403           | Forbidden, due to one of the following reasons: |
|               | * Invalid CSRF token                            |
|               | * Invalid X-Citrix-IsUsingHTTPS header          |

| Response Format | Request Accept/Response Content-Type Header |
|-----------------|---------------------------------------------|
| XML             | application/xml                             |

###Success Response Content

| Element name | Required | Description |
|--------------|----------|------------ |
| Result       | Yes      |Value "success" or "failure".|
| AuthType	   | No | The authentication type, as indicated by one of the authentication method strings: "ExplicitForms", "IntegratedWindows", "Certificate", "CitrixAGBasic", "PostCredentials". Only sent when authentication succeeds.|
| LogMessage | No | An error id indicating the reason for the authentication failure. Typically the generic value "fatalerror" is returned, but "sessiontimeout" is returned if the Citrix Receiver for Web session has timed out. When the credentials are rejected by the Authentication service, "loginfailed" is returned. Only sent when authentication fails. |

###Example: Successful Post Credentials Authentication 
####Request
```curl
POST http://webserver/Citrix/StoreWeb/PostCredentialsAuth/
```
####Response
##NetScaler Gateway Single Sign-On

|--------------------|--------|----------------------------------------------------------------|
| /GatewayAuth/Login | POST   | Authenticates the user using NetScaler Gateway single sign-on. |

!!! tip "Notes"
 	* When Citrix Receiver for Web is accessed through NetScaler Gateway, changing an expired 	password during logon is dealt with by the Gateway.


|---------------|-------------------------------------------------|
| 200           | Success or failure                              |
| 403           | Forbidden, due to one of the following reasons: |
|               | * Invalid CSRF token                            |
|               | * Invalid X-Citrix-IsUsingHTTPS header          |

| Response Format | Request Accept/Response Content-Type Header |
|-----------------|---------------------------------------------|
| XML             | application/xml                             |

###Success Response Content


POST https://gateway.acme.com/Citrix/StoreWeb/GatewayAuth/
Accept: application/xml, text/xml, */*; q=0.01
```
####Response
```curl
Response
```
##Get User Name

|------------------------------|--------|----------------------------------------------------------------------------------------------------------------------------|
| /Authentication/ GetUserName | POST   | Returns the user name. Obtain the URL from the Citrix Receiver for Web configuration using the getUsernameURL attribute at XPath /clientSettings/ authManager|

!!! tip "Notes"
	* This request requires an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId. When using an unauthenticated Store, no user has 	actually logged on and an HTTP 403 response is returned.

|---------------|---------------------------------------------------------------------------------------|
| 200           | Success or authentication challenge                                                   |
| 403           | Forbidden, due to one of the following reasons:                                       |
|               | * Invalid CSRF token                                                                  |
|               | * Invalid X-Citrix-IsUsingHTTPS header w Invalid CtxsAuthId cookie                    |
|               | * Missing authentication token in server session, when the user has not yet logged on |

###Success Response Content




```
##Log Off

|------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------|
| /Authentication/Logoff | POST   | Terminates the user's web session. Obtain the URL from the Citrix Receiver for Web configuration using the logoffURL attribute at: XPath /clientSettings/ authManager.                                                                                                |

!!! tip "Notes"
	* This request requires an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId.


|---------------|--------------------------------------------------------------------|
| 200           | Success                                                            |
| 403           | Forbidden, due to one of the following reasons:                    |
|               | * Invalid CSRF token                                               |
|               | * Invalid X-Citrix-IsUsingHTTPS header w Invalid CtxsAuthId cookie |

###Success Response Content

####Request
```curl
POST http://webserver/Citrix/StoreWeb/Authentication/Logoff
```
####Response
```
##Resource Enumeration


|-----------------------|--------|-----------------------------------------------------------------------|
| /Resources/List       | POST   | Returns a list of all resources available for the user in JSON format |

| POST parameters | Description                                                        |
|---------------|--------------------------------------------------------------------|
| resourcesDetails           | The resource details to include in the response. Use one of the following supported values: |

	* Typically, this request requires an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId. However, when the Web Proxy is configured to use an 	unauthenticated Store, an authenticated session is not required.


|---------------|----------------------------------------------------------------------|
| 200           | Success or authentication challenge                                  |
| 403           | Forbidden, due to one of the following reasons: w Invalid CSRF token |
|               | * Invalid X-Citrix-IsUsingHTTPS header w Invalid CtxsAuthId cookie   |
|               | * Invalid CtxsAuthId cookie                                          |

| Response Format | Request Accept/Response Content-Type Header |
|-----------------|---------------------------------------------|
| JSON             | application/json                            |

###Success Response Content

|-------------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| resources               | Object Array    | Details of each published resource available to the user. Each object in the array corresponds to a single resource and contains a set of fields, as described below. |
| isSubscriptionEna bled  | Boolean         | Whether subscription operations are enabled for the Store or not.                                                                                                     |
| isUnauthenticated Store | Boolean         | Whether or not the Store is accessible only without first authenticating.                                                                                             |

The resources field in the table above is an array of resource objects. Each resource object always contains the following set of fields:

| Field | JavaScript Type | Description                          |
|-------|-----------------|--------------------------------------|
| clienttypes| String Array | An array of string values identifying the clients supported for launches. Known values include **ica30**, **rade**, **rdp** (XenApp/XenDesktop), **application/ios**, **application/android** (AppController), **g2m**, **g2t** etc. (Citrix Online Integration using Generic applications). |
|iconurl | String | The URL to request the resource's icon image data. |
| id | String | Unique resource identifier, created by the Web Proxy. |
| launchstatusurl | String | The URL to determine whether a resource is ready to launch or not (see ICA Launch). |
| launchurl | String | The URL to make a launch request (see ICA Launch). |
| name | String | The user-friendly name of the resource. |
| path | String | The path defined in the XenApp/XenDesktop site (farm) for the resource. |
| shortcutvalidation url | String | The app shortcut validation URL, to confirm that an app may be launched using a shortcut. | 
| subscriptionstatus | String | The subscription status (see Resource Subscription).|

In addition, each resource object may contain the following optional fields:

| Field | JavaScript Type | Description |
|-------|-----------------|-------------|
|assigndesktopurl| String |Call this URL to assign a desktop to the user. Supplied only for XenDesktop assign-on-first-use desktops.|
|content | Boolean | Supplied with value *true* if the resource represents a document as opposed to a published application/desktop, otherwise omitted.|
| description | String | A longer text description of the resource.|
| desktopassignmenttype| String | The desktop assignment type: one of the values *shared*, *assign-on-first-use* or *assigned*. Supplied only for XenDesktop resources.|
|desktophostname| String| The desktop host name, if known. Supplied only for XenDesktop assigned desktops.|
| disabled | Boolean | Supplied with value *true* if the resource is not enabled, otherwise omitted.|
| isdesktop| Boolean | Supplied with value *true* if the resource is a desktop, otherwise omitted.|
| keywords| String Array | An array of string values identifying keywords associated with the resource.|
| mandatory| Boolean | Supplied with value true if the resource is tagged by the back-end resource provider as mandatory, otherwise omitted.|
|position|String|A string representing the relative position of a subscribed resource in the Citrix Receiver for Web UI. Only generated for resources for which a position has already been defined.|
|poweroffurl|String|The URL to make a machine power-off request. Only supplied if the resource can be powered- off, as reported by the StoreFront Resources service.|
|prelaunchurl |String|The URL to call to contact the AppController pre-launch service to obtain an updated content URL for single sign-on.|
|recommended|Boolean|Supplied with value true if the resource is tagged by the back-end resource provider as **featured** or **recommended**, otherwise omitted.|
|requiresvpn|Boolean| Supplied with value true if the resource is marked (using the Resources Service VPN keyword,) as launchable remotely (with NetScaler Gatway) only when using a VPN, otherwise omitted.|
|requiresworkflow|Boolean| Supplied with value true if workflow is enabled for the resource (typically due to the presence of the **WFS** keyword).|
|subscriptionurl|String|The URL to make a subscription request (see Resource Subscription).|

When the `resourceDetails` request parameter specifies that a "Full" enumeration should be performed, the following additional, and optional fields may be returned:

| Field | JavaScript Type | Description |
|-------|-----------------|-------------|
| images | Object Array | An array of objects identifying the image sizes and color depths of the resource icon held by the StoreFront Services server (may be used to determine which image sizes are likely to give good results when requested by the client). Each object in the array contains a pair of integer fields named **size** and **depth**.|
| playsfiletypes | Object Array | An array of objects describing the file extensions supported by the resource [Application only]. Each object in the array may contain the following fields:|
| | | *name* (String): file type association name |
| | | *description* (String): file type association description |
| | | *isdefault* (Boolean): whether this is the default file type association or not |
| | | *fileextensions* (String Array): array of file extensions that can be opened by this resource |
| | | *mimetypes* (String Array): array of mime types supported by the resource |
| | | *parameters* (String Array): array of parameters used for launching the resource |
| properties | Object Array | Resource properties—an array of name value pairs associated with the resource and ultimately supplied by the resource provider. Each object in the array contains a string field name describing the property *name* and a string array field *values* describing a list of property values.|
| publishername | String| The name of the publisher (the farm name for XenApp).|
| shortcuturl | String | The app shortcut URL, to use when embedding a link to the resource in a portal page.|
| subscriptionproperties | Object Array | Subscription properties — an array of name value pairs associated with the resource subscription and stored in the subscription database. Each object in the array contains a string field name for the property *name* and an optional string array field *values* for the list of property values. For more information, see Resource Subscription. |
| type | String |The resource type, typically one of the following values:|
| | | * Citrix.MPS.Application| 
| | | * Citrix.MPS.Desktop|
| | | * Citrix.MPS.Document|

!!! tip "Notes"
	* The iconurl value encodes a particular icon size, as configured in the Web.config site 	configuration file (resourcesService section, within serverSettings). The StoreFront Store 	service returns the icon that best matches the requested size.

```curl
POST http://webserver/Citrix/StoreWeb/Resources/List HTTP/1.1
```
####Response
Content-Type: application/json; charset=utf-8
```
###Example: Request all resources (full enumeration) 
####Request
```curl
POST http://webserver/Citrix/StoreWeb/Resources/List HTTP/1.1
Csrf-Token: 1062D9DA90BA01931DB472C09D61A6EB
```
####Response
{
```
##ICA Launch

|-----------------------|--------|-------------|

|-----------|-------------|
|displayNameDesktopTitle | The desktop display name. This is inserted in the generated ICA file as the value for the Title setting. This name is then displayed in the title bar of the Desktop Viewer. Note: this is a POST parameter for GetLaunchStatus and a query string parameter for LaunchIca.|

!!! tip "Notes"
	* Typically, these requests require an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId. However, when the Web Proxy is configured to use an 	unauthenticated Store, an authenticated session is not required.


|--------------|-------------|




|---|----|----|----|


```
####Response
```curl
```
###Example: Failed ICA launch 
####Request
```curl
Accept-Encoding: gzip, deflate
```
####Response
```curl
```


POST http://webserver/Citrix/StoreWeb/Resources/
```
####Response
```
##Icons


|---|----|-----|

|------|-----|
|{size}|The pixel size of the icon image to return. Only the values 16, 24, 32, 48, 64, 96, 128, 256 and 512 are supported. This value is included in the iconurl returned from an earlier enumeration request, based on the image size configured in the Citrix Receiver for Web site configuration file (defaults to 48).|

!!! tip "Notes"
	* This request requires an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId.
	* The URLs above are for illustrative purposes only; the actual URLs used by a client must 	be taken from the result of an earlier enumeration request, which provides a separate icon 	URL for each resource.

|-----------------------|-----|

|Response Format | Request Accept /Response Content-Type Header|
|---------|--------------|


GET http://webserver/Citrix/StoreWeb/Resources/Icon/
20100101 Firefox/23.0
```
####Response
```
##Machine Power Off
|URL (indicative only)|Method|Description|
|--------|-------|------|

|------|-----|



|Response Code | Description |
|----|-----|
| |* Invalid CSRF token|
| |* Invalid CtxsAuthId cookie|

|---|---|


|---|----|
|operation-in-progress|The server is busy with a control operation on the specified machine and cannot handle another request at this time.|


```
####Response
{"status":"success"}
```
##Resource Subscription
|---|----|----|
| | | * **subscribe**—attempt to subscribe to the resource. This may create a new subscription (if one does not already exist) and, by default, sets the subscription to the subscribed state.|

|----|----|
|Id|Unique identifier for a particular resource. Note: this parameter is a component of the URL.|
|operation|The subscription operation to perform: either **subscribe**, **unsubscribe**, or **update**.|

	* This request requires an authenticated session, indicated by the cookies `ASP . NET _ 	SessionId` and `CtxsAuthId`.

|----|-----|
| | * Invalid CSRF token|
|503 (Service Unavailable)|Subscription operations are unavailable for the specified resource, due to one of the following reasons:|



|---|---|-----|

|---|-----|

####Request
```curl
POST http://webserver/Citrix/StoreWeb/Resources/Subscription/
```
####Response
```
###Example: Unsuccessful unsubscription 
####Request
POST http://webserver/Citrix/StoreWeb/Resources/Subscription/
20100101 Firefox/23.0
```
####Response
HTTP/1.1 200 OK
```
###Example: Successful update of subscription properties

POST http://webserver/Citrix/StoreWeb/Resources/Subscription/
Cookie: CsrfToken=48C7A008D81F87116B4BDE418FB63B3C;
```
####Response
```
##Session Enumeration
|----|-----|-----|

|---|----|

	* This request requires an authenticated session, indicated by the cookies 	ASP.NET_SessionId and CtxsAuthId. When the Web Proxy is configured to use an 	unauthenticated Store, an empty session list is returned.

|------|------|
|----|------|------|

|----|-----|


```curl
```
####Response
 {
```
##Session Launch
|---|----|----|

|----|-----|

	* These requests require an authenticated session, indicated by the cookies `ASP . NET _ 	SessionId` and `CtxsAuthId`.


|----|----|

|----|-----|
|ICA File|application/octet-stream|

###Success Response Content

|----|----|----|
|pollTimeout|No|Only supplied when status is **retry**, the number of seconds to wait before retrying the launch request.|

When a successful response for LaunchIca is returned, the response body can be either a JSON string as described above for `GetLaunchStatus` or, if the resource is ready to launch, an ICA file.

POST http://webserver/Citrix/StoreWeb/Sessions/GetLaunchStatus/
Connection: keep-alive
```
####Response


```
####Response
[WFClient]
```
##Session Disconnect and Logoff

|----|-----|-----|

	* These requests require an authenticated session, indicated by the cookies `ASP .NET_ 	SessionId` and `CtxsAuthId`.

|----|----|----|
|200|Success/failure, or authentication challenge.|
| | * Invalid CtxsAuthId cookie|

|Response Format|Request Accept/Response Content-Type Header|
|---|----|



POST http://webserver/Citrix/StoreWeb/Sessions/Disconnect HTTP/
```
####Response
```curl
```
###Example: Session Logoff

####Request
```curl
POST http://webserver/Citrix/StoreWeb/Sessions/Logoff HTTP/1.1
```
####Response
```