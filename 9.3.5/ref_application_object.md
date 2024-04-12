# Application objects 

Table 1. Application Object (app) The Leap application object provides access to information relevant to the whole application.

<table class="table-wrap">
<tr>
<td width="225"> <b>Object</b> </td><td> <b>Description</b> <td><b>Example</b></td>
</tr>
<tr>
<td>app.getAppPage(appPageId)
<td>Returns the user interface app page object for the provided
<td>

```javascript
var myAppPage = app.getAppPage("AP_Welcome");
```

</tr>
<tr>
<td>app.getAppPageURL(appPageId, appUid)
<td>Returns the URL for navigating directly to the app page for the provided app page id and application uid.<br>
<br>

<b>Note:</b> The appUid parameter is optional. If you do not supply a parameter, it will be set to the object in the current scope.
<td>
</tr>
<tr>
<td>app.getAppURL()
<td>Returns the URL for navigating directly to the application.<br>
<br>

<b>Note:</b> The application will load the form or app page defined in the "Home Page" field on the Settings tab.
<td></td>
</tr>
<tr>
<td>app.getChartsURL(formId, appUid)
<td>Returns the URL for navigating directly to the charts page of the form for the provided form uid and application uid.<br>
<br>

<b>Note:</b> All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.
<td>

```javascript
var url = app.getChartsURL(form.getId(), app.getUID());
```

</tr>
<tr>
<td>app.getCurrentUser()
<td>Deprecated - Use app.getCurrentUserId()
<td>
</tr>
<tr>
<td>app.getCurrentUserId()
<td>Returns the user's "identifier" - the identifying name of the currently logged in user.<br>
<br>
The identifying name is the property as defined by the ibm.was.MemberManager.userProps.id property that is located in the Leap_config.properties file. For example, <b>uid</b>, <b>cn</b>, <b>mail</b>, <b>displayName</b>.<br>
<br>
If the user is not authenticated, then the function returns the string "Anonymous Guest User".
<td>
To populate the current user's login name into a field in the form, place the following statement in the <b>onLoad</b> event of the form:<br>
<br>
```javascript
// change F_SingleLine to the ID of the desired field 
BO.F_SingleLine.setValue(app.getCurrentUser());
```

</tr>
<tr>
<td>app.getCurrentUserEmail()
<td>Returns the user's email.
<td>
</tr>
<tr>
<td>app.getCurrentUserDisplayName()
<td>Returns the user's full display name.
<td>Ex. "Eduardo Ramírez López".
</tr>
<tr>
<td>app.getCurrentUserInfo()
<td>Returns the object containing the attributes of the current user.
<td>For example:

```javascript
{
  id: "pflorez123", 
  email: "Pedro.Flores@example.com", 
  displayName: "Pedro Flores", 
  userType: "owner"
}
```

<b>Note:</b> Not all attributes are available in all deployments. In that case, some of these values will be null.<br>
<br>
<b>userType</b> – possible values:
<ul>
<li>  "owner" – if current user is the app owner</li>
<li>  "guest" – if the current user is anonymous</li>
<li>   "" (empty string) – in all other cases</li>
</ul>
</tr>
<tr>
<td>app.getCurrentUserRoles
<td>Returns a comma-separated list of all the roles for which the current user is a member.
<td>For example:

```javascript
item.setValue(app.getCurrentUserRoles());
```

</td>
</tr>
<td>app.getFileBaseURL()
<td>Returns the relative URL to the current browser page where all files that are uploaded into the application at design time are stored. This does not include images and CSS files. All files are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/files/
<td>
</tr>
<tr>
<td>app.getForm(formID)
<td>Returns the user interface form object for the provided formID. If used to return a form that is not shown or loaded, then the object that is returned is not fully operational and should be used for hooking up dynamic event handlers only.
<td>Register an event listener to a service in order to do something when it returns:

```javascript
var form = app.getForm('F_Form1');
var service = form.getServiceConfiguration('SC_ServiceConfig0');
service.connectEvent('onCallFinished', function(pSuccess)
{
  alert('call finished');
});
```

</tr>
<tr>
<td>app.getFormLaunchURL(formId, appUid)
<td>Returns the URL for navigating directly to the form for the provided application uid and form uid.<br>
<br>
<b>Note:</b> All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.

<td>
```javascript
var url = app.getFormLaunchURL();
var url = app.getFormLaunchURL(form.getId());
var url = app.getFormLaunchURL(form.getId(), app.getUID());

```

</tr>
<tr>
<td>app.getImageBaseURL()
<td>Returns the relative URL to the current browser page where all images that are uploaded into the application at design time are stored. All images are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/image/
<td>
</tr>
<tr>
<td> app.getLocale()
<td>Returns the current locale of the application, according to the application's settings or the current user's preferences. The returned value is a locale code, in accordance with <a href="https://www.ietf.org/rfc/rfc3066.txt" target="_blank">Tags for the Identification of Languages (RFC 3066)</a>.
<td>
</tr>
<tr>
<td>app.getLocation(callbackFunction, highAccuracy)
<td>Allows the form designer to get the current user's location.<br>
<br>
 <b>callbackFunction</b> - the callback that occurs after the location request finishes. The designer must define the function to have one argument which will be assigned a Position object if the location request was successful, or null if the request was unsuccessful. Inside the function the designer can assign location attributes to different fields. Five values can be accessed:

<ul>
<li>   position.coords.latitude</li>
<li>   position.coords.longitude</li>
<li>   position.coords.accuracy</li>
<li>   position.coords.altitude</li>
<li>   position.coords.altitudeAccuracy</li>
</ul>
<br>
More information at <a href="https://developer.mozilla.org/en-US/docs/Web/API/Position/" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/Position/</a>.<br>

<td>Set the value of F_SingleLine1 to the current location:

```javascript
var highAccuracy = true;
var myCallbackFunction = function (position) {
  if (position !== null) {
    BO.F_SingleLine1.setValue(position.coords.latitude+", "+position.coords.longitude);
  } else {
    alert("Location request failed");
  }
};
app.getLocation(myCallbackFunction,highAccuracy);

```

</tr>
<tr>
<td>app.getProductBaseURL()
<td>Returns the host and context of the Leap server.
<td>

```javascript
var url = app.getProductBaseURL();
```

</tr>
<td>app.getRecordURL(recordUid, formId, appUid)
<td>Returns the URL for navigating directly to the record.

<b>Note:</b> All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.
<td>

```javascript
var url1 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9');
var url2 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', form.getId());
var url3 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', form.getId(), app.getUID());
```

</tr>
<tr>
<td>
app.getSharedData()
<td>
Returns a JavaScript™ object that can be easily accessed from all custom JavaScript code on the form, and is the suggested location to share data, or create reusable functions.

<td>
Create some data and functions to be used later:
```javascript
app.getSharedData().titleToShow = 'Welcome Form';
app.getSharedData().addTwoValues = function(v1, v2)
{
  return v1 + v2;
};
```

Example of referencing the established variable and function:
```javascript
BO.F_SingleLine.setValue(app.getSharedData().titleToShow);
BO.F_Number.setValue(app.getSharedData().addTwoValues(5, 5));
```

<tr>
<td>app.getStyleBaseURL()
<td>Returns the relative URL to the current browser page where all CSS style files that are uploaded into the application at design time are stored. All css files are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/styles/| 
<td>

<tr>
<td>app.getSuppressWarning()
<td>Gets the current set value for suppressing the warning. See setSuppressWarning for information.
<td>
```javascript
var suppressWarning = app.getSuppressWarning();
if(suppressWarning === false)
  app.setSuppressWarning(true);
```

<tr>
<td>app.getUID()
<td>The UID of the application
<td>Can be used to create a link to another form
```javascript
page.F_StaticWebLink.setLinkValue(BO.F_ServerURL.getValue() + 
  '/apps/secure/1/app/' + 
  app.getUID() + 
  '/launch/index.html?form=F_Form2');
```

<tr>
<td>app.getUrlParameter(parm)
<td>Looks up a single URL query parameter.
<td>
```javascript
var param= app.getUrlParameter('debug')
if(param === 'true')
   alert('Shown only when debug param is present');
```

<tr>
<td>app.getUrlParameters()
<td>Returns an object with all URL parameters.
<td>
```javascript
var params = app.getUrlParameters();
if(params.CustomWarning)
     alert(params.CustomWarning);
```

<tr>
<td>app.getViewDataURL(appUid)
<td>Returns the URL for navigating directly to the View Data page.<br>
<br>
<b>Note:</b> The parameter is optional. If you do not supply a parameter, it will be set to the object in the current scope.
<td>
```javascript
var url = app.getViewDataURL();
var url = app.getViewDataURL(app.getUID());
```

<tr>
<td>app.isCurrentUserInRole (roleName)
<td>Returns true if the current user is a member of the provided role, otherwise false.<br>
<br>
<b>Note:</b> The function does not validate the role with the provided roleName, therefore if the role does not exist <code>false</code> is returned.

<td>For example:
```javascript
if (!app.isCurrentUserInRole("Manager")) {
  page.F_Instructions.setVisible(false);
}
```

<tr>
<td>app.isSingleFormView()
<td>Returns true if the form is shown by itself in the browser and false if it is shown in view data.| 
<td>

<tr>
<td>app.openApp(appUid, newTab)
<td>Opens the home page of an application. The current app is used if you do not supply an app id. If <code>newTab</code> is <code>true</code>, the app is presented in a new browser tab. The default behavior is for the application to be opened in a new tab.
<td>
```javascript
app.openApp('d1f6eb71-9483-479c-8d47-dd30bd7e9de9');
app.openApp ('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', true);
app.openApp (app.getUID(), false);
```

<tr>
<td>app.openAppPage(appPageId, appUid, newTab)
<td>Opens the app page of an application that matches the provided <i>appPageid</i>.<br>
<br>
<b>Note:</b> appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

<td>
```javascript
app.openAppPage('AP_Page1');
app.openAppPage ('AP_Page1', true);
app.openAppPage ('AP_Page1', false);
```

<tr>
<td>app.openForm(formId, appUid, newTab)
<td>Opens the form of an application that matches the provided <i>formId</i>.<br>
<br>
<b>Note:</b> appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

<td>
```javascript
app.openForm('F_Form1');
app.openForm('F_Form1', true);
app.openForm ('F_Form1', false);

```

<tr>
<td>openRecord(recordUid, formId, appUid, newTab)
<td>Opens the record of a form that matches the provided <i>recordId</i> and <i>formId</i>.<br>
<br>
<b>Note:</b> formId, appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

<td>
```javascript
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx');
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy');
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy', true);
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy', 'zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz', false);

```

<tr>
<td>app.setSuppressWarning (pSuppress)
<td>If a user interacts with a form, or JavaScript, they are prompted with a warning message whenever the current browser page tries to navigate to a different URL. This function allows the suppression of that warning. When set to true the message is suppressed until it is set to false again
<td>Can be used at any scope, for example in the application onStart, form onLoad, onItemChange, etc.
```javascript
app.setSuppressWarning(true);
```

<tr>
<td>app.showMessage(title, message, type, subtitle)

<td>Allow usage of a built-in dialog for end-user messages. title: The title to display in the dialog title bar.<br>
<br>
 message: The message text to display.<br>
<br>
 type (optional): can be one of "info", "success", "warn", or "error" and results in appropriate icon being displayed. If type is absent or not one of these values, then no icon will be displayed.<br>
<br>
 subtitle (optional): Heading text for the message.

<td>
```javascript
app.showMessage (
 "Error found in data",
 "The booking date cannot be after the event.",
 "error",
 "Please change the booking or event date, then re-submit."
);
```
</table>
**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)

