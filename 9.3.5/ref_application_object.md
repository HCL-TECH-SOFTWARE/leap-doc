# Application objects {#ref_application_object .concept}

|Object|Description|Example|
|------|-----------|-------|
|app.getAppPage\(appPageId\)|Returns the user interface app page object for the provided *appPageId*.

|```
var myAppPage = app.getAppPage(“AP_Welcome”);
```

|
|app.getAppPageURL\(appPageId, appUid\)|Returns the URL for navigating directly to the app page for the provided app page id and application uid.

**Note:** The appUid parameter is optional. If you do not supply a parameter, it will be set to the object in the current scope.

| |
|app.getAppURL\(\)|Returns the URL for navigating directly to the application.

**Note:** The application will load the form or app page defined in the “Home Page” field on the Settings tab.

| |
|app.getChartsURL\(formId, appUid\)|Returns the URL for navigating directly to the charts page of the form for the provided form uid and application uid.

**Note:** All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.

|```
var url = app.getChartsURL(form.getId(), app.getUID());
```

|
|app.getCurrentUser\(\)|Returns the identifying name of the currently logged in user. The identifying name is the property as defined by the ibm.was.MemberManager.userProps.id property that is located in the Leap\_config.properties file. For example, **uid**, **cn**, **mail**, **displayName**. If the Initiator Role is set to **Anonymous User**, then the function returns the string “Anonymous Guest User”.|To populate the current user's login name into a field in the form, place the following statement in the **onLoad** event of the form:**Note:** The following code must be entered as a single line.

```
//change F_SingleLine to the ID of the desired field 
BO.F_SingleLine.setValue(app.getCurrentUser());
```

|
|app.getCurrentUserId\(\)|Returns the user's "identifier" - the identifying name of the currently logged in user. The identifying name is the property as defined by the ibm.was.MemberManager.userProps.id property that is located in the Leap\_config.properties file. For example, **uid**, **cn**, **mail**, **displayName**. If the Initiator Role is set to **Anonymous User**, then the function returns the string “Anonymous Guest User”.

| |
|app.getCurrentUserEmail\(\)|Returns the user's email.| |
|app.getCurrentUserDisplayName\(\)|Returns the user's full display name.

|Ex. "Eduardo Ramírez López".|
|app.getCurrentUserInfo\(\)|Returns the object containing the attributes of the current user.

|For example:```
{id: "pflorez123", email: "Pedro.Flores@example.com", displayName: "Pedro Flores", userType: "owner"}
```

**Note:** Not all attributes are available in all deployments. In that case, some of these values will be null.

**userType** – possible values:

-   "owner" – if current user is the app owner
-   "guest" – if the current user is anonymous
-   "" \(empty string\) – in all other cases

|
|app.getCurrentUserRoles|Returns a comma-separated list of all the roles for which the current user is a member.|For example:```
item.setValue(app.getCurrentUserRoles());
```

|
|app.getFileBaseURL\(\)|Returns the relative URL to the current browser page where all files that are uploaded into the application at design time are stored. This does not include images and CSS files. All files are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/files/| |
|app.getForm\(formID\)|Returns the user interface form object for the provided formID. If used to return a form that is not shown or loaded, then the object that is returned is not fully operational and should be used for hooking up dynamic event handlers only.|Register an event listener to a service in order to do something when it returns:```
var form = app.getForm('F_Form1');
     var service = form.getServiceConfiguration('SC_ServiceConfig0');

     service.connectEvent('onCallFinished', function(pSuccess)
     {
     alert('call finished');
     });
```

|
|app.getFormLaunchURL\(formId, appUid\)|Returns the URL for navigating directly to the form for the provided application uid and form uid.

**Note:** All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.

|```
var url = app.getFormLaunchURL();
var url = app.getFormLaunchURL(form.getId());
var url = app.getFormLaunchURL(form.getId(), app.getUID());

```

|
|app.getImageBaseURL\(\)|Returns the relative URL to the current browser page where all images that are uploaded into the application at design time are stored. All images are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/image/| |
|app.getLocale\(\)|Returns the current locale of the application, according to the application's settings or the current user's preferences. The returned value is a locale code, in accordance with [Tags for the Identification of Languages \(RFC 3066\)](https://www.ietf.org/rfc/rfc3066.txt).| |
|app.getLocation\(callbackFunction, highAccuracy\)

|Allows the form designer to get the current user's location.

 callbackFunction - the callback that occurs after the location request finishes. The designer must define the function to have one argument which will be assigned a Position object if the location request was successful, or null if the request was unsuccessful. Inside the function the designer can assign location attributes to different fields. Five values can be accessed:

 -   position.coords.latitude
-   position.coords.longitude
-   position.coords.accuracy
-   position.coords.altitude
-   position.coords.altitudeAccuracy

 More information in [https://developer.mozilla.org/en-US/docs/Web/API/Position/](https://developer.mozilla.org/en-US/docs/Web/API/Position/).

 highAccuracy - a boolean value that requests a high accuracy location from the browser if true. See [https://developer.mozilla.org/en-US/docs/Web/API/PositionOptions/enableHighAccuracy](https://developer.mozilla.org/en-US/docs/Web/API/PositionOptions/enableHighAccuracy).

|Set the value of F\_SingleLine1 to the current location:

 ```

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

|
|app.getProductBaseURL\(\)|Returns the host and context of the Leap server.

|```
var url = app.getProductBaseURL();
```

|
|app.getRecordURL\(recordUid, formId, appUid\)|Returns the URL for navigating directly to the record.

**Note:** All parameters are optional. If you do not supply a parameter, it will be set to the object in the current scope.

|```
var url = app.getRecordURL(‘d1f6eb71-9483-479c-8d47-dd30bd7e9de9’);
var url = app.getRecordURL(‘d1f6eb71-9483-479c-8d47-dd30bd7e9de9’, form.getId());
var url = app.getRecordURL(‘d1f6eb71-9483-479c-8d47-dd30bd7e9de9’, form.getId(), app.getUID());

```

|
|app.getSharedData\(\)|Returns a JavaScript™ object that can be easily accessed from all custom JavaScript code on the form, and is the suggested location to share data, or create reusable functions.|Create some data and functions to be used later:```
app.getSharedData().titleToShow = 'Welcome Form';
     app.getSharedData().addTwoValues = function(v1,v2)
     {
     return v1 + v2;
     };
```

Example of referencing the established variable and function:```
BO.F_SingleLine.setValue(app.getSharedData().titleToShow);
BO.F_Number.setValue(app.getSharedData().addTwoValues(5, 5));
```

|
|app.getStyleBaseURL\(\)|Returns the relative URL to the current browser page where all CSS style files that are uploaded into the application at design time are stored. All css files are saved as anonymous resources that can be viewed by anyone. An example url is ../../../../../anon/1/content/8.6.0.363/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/styles/| |
|app.getSuppressWarning\(\)|Gets the current set value for suppressing the warning. See setSuppressWarning for information.|```
var suppressWarning = app.getSuppressWarning();
if(suppressWarning === false)
  app.setSuppressWarning(true);
```

|
|app.getUID\(\)|The UID of the application|Can be used to create a link to another form ```
page.F_StaticWebLink.setLinkValue(BO.F_ServerURL.getValue() + '/apps/secure/1/app/' + app.getUID() + '/launch/index.html?form=F_Form2'));
```

|
|app.getUrlParameter\(parm\)|Looks up a single parameter.|```
var param= app.getUrlParameter('debug')
if(param === 'true')
   alert('Shown only when debug param is present');
```

|
|app.getUrlParameters\(\)|Returns an object with all URL parameters.|```
var params = app.getUrlParameters();
     if(params.CustomWarning)
     alert(params.CustomWarning);
```

|
|app.getViewDataURL\(appUid\)|Returns the URL for navigating directly to the View Data page.

**Note:** The parameter is optional. If you do not supply a parameter, it will be set to the object in the current scope.

|```
var url = app.getViewDataURL();
var url = app.getViewDataURL(app.getUID());

```

|
|app.isCurrentUserInRole\(roleName\)|Returns true if the current user is a member of the provided role, otherwise false.**Note:** The function does not validate the role with the provided roleName, therefore if the role does not exist false is returned.

|For example:```
item.setValue(app.isCurrentUserInRole("Manager"));
```

|
|app.isSingleFormView\(\)|Returns true if the form is shown by itself in the browser and false if it is shown in view data.| |
|app.openApp\(appUid, newTab\)|Opens the home page of an application. The current app is used if you do not supply an app id. If “newTab” is “true”, the app is presented in a new browser tab. The default behavior is for the application to be opened in a new tab.

|```
app.openApp(‘d1f6eb71-9483-479c-8d47-dd30bd7e9de9’);
app.openApp (‘d1f6eb71-9483-479c-8d47-dd30bd7e9de9’, true);
app.openApp (app.getUID(), false);

```

|
|app.openAppPage\(appPageId, appUid, newTab\)|Opens the app page of an application that matches the provided *appPageid*.

**Note:** appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

|```
app.openAppPage(‘AP_Page1’);
app.openAppPage (‘AP_Page1’, true);
app.openAppPage (‘AP_Page1’, false);

```

|
|app.openForm\(formId, appUid, newTab\)|Opens the form of an application that matches the provided *formId*.

**Note:** appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

|```
app.openForm(‘F_Form1’);
app.openForm(‘F_Form1’, true);
app.openForm (‘F_Form1’, false);

```

|
|openRecord\(recordUid, formId, appUid, newTab\)|Opens the record of a form that matches the provided *recordId* and *formId*.

**Note:** formId, appUid and newTab are optional. If you do not supply a parameter, it will be set to the object in the current scope. The default behavior is for the application to be opened in a new tab.

|```
app.openRecord(‘xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx’);
app.openRecord(‘xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx’, ‘yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy’);
app.openRecord(‘xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx’, ‘yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy’, true);
app.openRecord(‘xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx’, ‘yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy’, ‘zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz’, false);

```

|
|app.setSuppressWarning\(pSuppress\)|If a user interacts with a form, or JavaScript, they are prompted with a warning message whenever the current browser page tries to navigate to a different URL. This function allows the suppression of that warning. When set to true the message is suppressed until it is set to false again|Can be used at any scope, for example in the application onStart, form onLoad, onItemChange, etc.```
app.setSuppressWarning(true);
```

|
|app.showMessage\(title, message, type, subtitle\)

|Allow usage of a built-in dialog for end-user messages. title: The title to display in the dialog title bar.

 message: The message text to display.

 type \(optional\): can be one of "info", "success", "warn", or "error" and results in appropriate icon being displayed. If type is absent or not one of these values, then no icon will be displayed.

 subtitle \(optional\): Heading text for the message.

|```
app.showMessage
("Error found in data",
 "The booking date cannot be after the event.",
 "error",
 "Please change the booking or event date, then re-submit.");
```

|

**Parent topic:**[Interface objects](ref_jsapi_user_interface_objects.md)

