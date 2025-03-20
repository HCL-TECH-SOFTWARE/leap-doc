# Application object 

The {{shortProductName}} application object, referenced by using 'app', provides access to information relevant to the whole application.  The object has several built-in functions.

## Functions


### getAppPage {.section}

Returns the user interface app page object for the provided appPage id.

**Syntax**
```javascript
app.getAppPage(appPageId)
```

**Parameters**

|Parameter|Description|
|---------|-----------|
|appPageId|Optional. The id of the app page to retrieve, if not supplied the current app page id is used.|

**Example**
```javascript
var myAppPage = app.getAppPage("AP_Welcome");
```


### getAppPageURL {.section}

Returns the URL for navigating directly to the app page for the provided app page id and application uid.

**Syntax**
```javascript
getAppPageURL(appPageId, appUid)
```

**Parameters** 

|Parameter|Description|
|------------|----------|
|appPageId|Optional. The id of the app page to retrieve, if not supplied the current app page id is used.|
|appUid|Optional. The uid of the app to retrieve, if not supplied the current app uid is used.|

**Example**
```javascript
var appPageUrl = app.getAppPageUrl('AP_Welcome', 'e09e7739-2214-4e64-88e3-9f54a47c3fdd');
```


### getAppURL {.section}

Returns the URL for navigating directly to the application.

!!! note
    The application will load the form or app page defined in the "Home Page" field on the Settings tab.

**Syntax**
```javascript
app.getAppURL()
```

**Example**
```javascript
var appUrl = app.getAppUrl();
```


### getChartsURL {.section}

Returns the URL for navigating directly to the charts page of the form for the provided form uid and application uid.

**Syntax**
```javascript
app.getChartsURL(formId, appUid)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| formId        | Optional. The id of the form to retrieve, if not supplied the current form id is used. |
| appUid        | Optional. The uid of the app to retrieve, if not supplied the current app uid is used. |

**Example:**
```javascript
var url = app.getChartsURL(form.getId(), app.getUID());
```


### getCurrentUser {.section}

**Deprecated** - Use app.getCurrentUserId()


### getCurrentUserId {.section}

Returns the user's "identifier" - the identifying name of the currently logged in user.

{% if isLeap %}
The identifying name is the property as defined by the ibm.was.MemberManager.userProps.id property that is located in the Leap_config.properties file. For example, *uid*, *cn*, *mail*, *displayName*.
{% endif %}

If the user is not authenticated, then the function returns the string "Anonymous Guest User".

**Syntax**
```javascript
app.getCurrentUserId()
```

**Example:**

To populate the current user's login name into a field in the form, place the following statement in the **onLoad** event of the form:
```javascript
// change F_SingleLine to the ID of the desired field 
BO.F_SingleLine.setValue(app.getCurrentUserId());
```


### getCurrentUserEmail {.section}

Returns the user's email.

**Syntax**
```javascript
app.getCurrentUserEmail()
```

**Example**
```javascript
BO.F_UserEmail.setValue(app.getCurrentUserEmail());
```


### getCurrentUserDisplayName {.section}

Returns the user's full display name. Ex. "Eduardo Ramírez López".

**Syntax**
```javascript
app.getCurrentUserDisplayName()
```

**Example**
```javascript
BO.F_UserName.setValue(app.getCurrentUserDisplayName());
```


### getCurrentUserInfo {.section}

Returns the object containing the attributes of the current user.

**Syntax**
```javascript
app.getCurrentUserInfo()
```

**Example:**
```json
{
  id: "pflorez123", 
  email: "Pedro.Flores@example.com", 
  displayName: "Pedro Flores", 
  userType: "owner"
}
```
!!! note
    Not all attributes are available in all deployments. In that case, some of the values will be null.

*userType* – possible values:

- "owner" – if current user is the app owner
- "guest" – if the current user is anonymous
- "" (empty string) – in all other cases


### getCurrentUserRoles {.section}

Returns a comma-separated list of all the roles for which the current user is a member.

**Syntax**
```javascript
app.getCurrentUserRoles()
```

**Example:**
```javascript
item.setValue(app.getCurrentUserRoles());
```


### getFileBaseURL {.section}

Returns the relative URL to the current browser page where all files that are uploaded into the application at design time are stored. This does not include images and CSS files. All files are saved as anonymous resources that can be viewed by anyone. 

An example url is ../../../../../anon/1/content/9.3.6.33/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/files/

**Syntax**
```javascript
app.getFileBaseURL()
```

**Example**

This example demonstrates how to create a link item in a form that refers to a file included in the {{shortProductName}} application.

1. Attach a file (not image or CSS) to your {{shortProductName}} application. Go to Settings...Files and click the 'Add' button.
2. Add a Link item to the form
3. In the **onShow** event of the Link item add:
```javascript
item.setLinkValue(app.getFileBaseURL() + "sampleAttachedFile");
```


### getForm {.section}

Returns the user interface form object for the provided formID. If used to return a form that is not shown or loaded, then the object that is returned is not fully operational and should be used for hooking up dynamic event handlers only.

**Syntax**
```javascript
app.getForm(formID)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| formId        | The id of the form to retrieve. |

**Example:**
```javascript
// Register an event listener to a service in order to do something when it returns
var form = app.getForm('F_Form1');
var service = form.getServiceConfiguration('SC_ServiceConfig0');
service.connectEvent('onCallFinished', function(pSuccess)
{
  alert('call finished');
});
```

### getFormLaunchURL {.section}

Returns the URL for navigating directly to the form for the provided application uid and form uid.

**Syntax**
```javascript
app.getFormLaunchURL(formId, appUid)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| formId        | Optional. The form id, if not specified the current form id is used. |
| appUid        | Optional. The app uid, if not specified the current app uid is used. |

**Example:**
```javascript
var url = app.getFormLaunchURL();
var url = app.getFormLaunchURL(form.getId());
var url = app.getFormLaunchURL(form.getId(), app.getUID());
```


### getImageBaseURL {.section}

Returns the relative URL to the current browser page where all images that are uploaded into the application at design time are stored. All images are saved as anonymous resources that can be viewed by anyone. 

An example url is ../../../../../anon/1/content/9.3.6.33/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/image/

**Syntax**
```javascript
app.getImageBaseURL()
```

**Example**

This example demonstrates how to create a link item in a form that refers to a file included in the {{shortProductName}} application.

1. Attach an image file to your {{shortProductName}} application. Go to Settings...Files and click the 'Add' button.
2. Add a Link item to the form
3. In the **onShow** event of the Link item add:
```javascript
item.setLinkValue(app.getFileBaseURL() + "sampleAttachedImageFile");
```


### getLocale {.section}

Returns the current locale of the application, according to the application's settings or the current user's preferences. The returned value is a locale code, in accordance with <a href="https://www.ietf.org/rfc/rfc3066.txt" target="_blank">Tags for the Identification of Languages (RFC 3066)</a>.

**Syntax**
```javascript
app.getLocale()
```


### getLocation {.section}

Allows the form designer to get the current user's location.

**Syntax**
```javascript
app.getLocation(callbackFunction, highAccuracy)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| callbackFunction | the callback that occurs after the location request finishes. |
| highAccuracy     | Optional. The form id, if not specified the current form id is used. |

*callbackFunction* -  The designer must define the function to have one argument which will be assigned a Position object if the location request was successful, or null if the request was unsuccessful. Inside the function the designer can assign location attributes to different fields. Five values can be accessed:

- position.coords.latitude
- position.coords.longitude
- position.coords.accuracy
- position.coords.altitude
- position.coords.altitudeAccuracy

More information at <a href="https://developer.mozilla.org/en-US/docs/Web/API/Position/" target="_blank">https://developer.mozilla.org/en-US/docs/Web/API/Position/</a>.

**Example:**
```javascript
// Set the value of F_SingleLine1 to the current location
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


### getProductBaseURL {.section}

Returns the host and context of the {{shortProductName}} server.

**Syntax**
```javascript
app.getProductBaseURL()
```

**Example:**
```javascript
var url = app.getProductBaseURL();
```


### getRecordURL {.section}

Returns the URL for navigating directly to the record.

**Syntax**
```javascript
app.getRecordURL(recordUid, formId, appUid)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| recordUid     | The submitted record uid. |
| formId        | Optional. The form id, if not specified the current form id is used. |
| appUid        | Optional. The app uid, if not specified the current app uid is used. |

**Example:**
```javascript
var url1 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9');
var url2 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', form.getId());
var url3 = app.getRecordURL('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', form.getId(), app.getUID());
```


### getSharedData {.section}

Returns a JavaScript™ object that can be easily accessed from all custom JavaScript code on the form, and is the suggested location to share data, or create reusable 

**Syntax**
```javascript
functions.app.getSharedData()
```

**Example:**
```javascript
// Create a variable
app.getSharedData().titleToShow = 'Welcome Form';

// Create a function
app.getSharedData().addTwoValues = function(v1, v2)
{
  return v1 + v2;
};

// Referencing the variable
BO.F_SingleLine.setValue(app.getSharedData().titleToShow);

// Referencing the function
BO.F_Number.setValue(app.getSharedData().addTwoValues(5, 5));
```


### getStyleBaseURL {.section}

Returns the relative URL to the current browser page where all CSS style files that are uploaded into the application at design time are stored. All css files are saved as anonymous resources that can be viewed by anyone. 

An example url is ../../../../../anon/1/content/9.3.6.33/97eeb588-2fff-49a7-89c1-5000885dafb4/1421171344944-2/desktop/en/en/en/desktop/styles/

**Syntax**
```javascript
app.getStyleBaseURL()
```

**Example**

This example demonstrates how to create a link item in a form that refers to a file included in the {{shortProductName}} application.

1. Attach a CSS file to your {{shortProductName}} application. Go to Settings...Files and click the 'Add' button.
2. Add a Link item to the form
3. In the **onShow** event of the Link item add:
```javascript
item.setLinkValue(app.getFileBaseURL() + "sampleAttachedCSSFile");
```


### getSuppressWarning {.section}

Gets the current set value for suppressing the warning. See setSuppressWarning for information.

**Syntax**
```javascript
app.getSuppressWarning()
```

**Example:**
```javascript
var suppressWarning = app.getSuppressWarning();
if(suppressWarning === false)
  app.setSuppressWarning(true);
```

### getTitle

Gets the title of the application.

**Syntax**
```javascript
app.getTitle()
```

**Example**
```javascript
page.F_Text.setContent(app.getTitle())
```


### getUID {.section}

The UID of the application

**Syntax**
```javascript
app.getUID();
```

**Example:**
```javascript
// Can be stored in a field
BO.F_AppUid.setValue(app.getUID());

// Can be used to create a link to another form.
page.F_StaticWebLink.setLinkValue(BO.F_ServerURL.getValue() + 
  '/apps/secure/1/app/' + app.getUID() + 
  '/launch/index.html?form=F_Form2');
```


### getUrlParameter {.section}

Looks up a single URL query parameter.  If the parameter does not exist then 'undefined' is returned.  If the url parameter is repeated in the URL then all the values will be returned separated by a comma.

```javascript
app.getUrlParameter(parm)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| parm          | The name of parameter to retrieve from the url. |

**Example:**

1. Trigger condition if specific url parameter is passed
```javascript
var param = app.getUrlParameter('debug')
if (param === 'true')
   alert('Shown only when debug param is present');
```

2. Set url parameter values into fields on the form
```javascript
var cityParam = app.getUrlParameter('city')

if (typeof cityParam !== 'undefined')
   BO.F_City.setValue(cityParam);
```

Given the URL 'http://myLeapServer.com/{% if isDominoLeap %}volt-{% endif %}apps/secure/org/app/df102a80-fb5d-450b-8be2-9d3fde5f9b3d/launch/index.html?form=F_Form1&city=Atlantis', 'Atlantis' would be placed into the field.

Given the URL 'http://myLeapServer.com/{% if isDominoLeap %}volt-{% endif %}apps/secure/org/app/df102a80-fb5d-450b-8be2-9d3fde5f9b3d/launch/index.html?form=F_Form1&city=Atlantis&city=Rome', 'Atlantis,Rome' would be placed into the field.


### getUrlParameters {.section}

Returns an object with all URL parameters.

**Syntax**
```javascript
app.getUrlParameters()
```

**Example:**
```javascript
var params = app.getUrlParameters();
if(params.CustomWarning)
     alert(params.CustomWarning);
```


### getViewDataURL {.section}

Returns the URL for navigating directly to the View Data page.

**Syntax**
```javascript
app.getViewDataURL(appUid)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| appUid        | The uid of the app, if not specified the current app will be used. |

**Example:**
```javascript
var url = app.getViewDataURL();
var url = app.getViewDataURL(app.getUID());
```


### isCurrentUserInRole {.section}

Returns true if the current user is a member of the provided role, otherwise false.

!!! note
    The function does not validate the role with the provided roleName, therefore if the role does not exist *false* is returned.

**Syntax**
```javascript
app.isCurrentUserInRole (roleName)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| roleName      | The name of the role to inspect if the current user is a member. |


**Example:**
```javascript
if (!app.isCurrentUserInRole("Manager")) {
  page.F_Instructions.setVisible(false);
}
```


### isSingleFormView {.section}

Returns true if the form is shown by itself in the browser and false if it is shown in view data.

**Syntax**
```javascript
app.isSingleFormView()
```

**Example**
```javascript
if (app.isSingleFormView())
{
  // do something
}
```


### openApp {.section}

Opens the home page of an application. The current app is used if you do not supply an app id. If <code>newTab</code> is <code>true</code>, the app is presented in a new browser tab. The default behavior is for the application to be opened in a new tab.

**Syntax**
```javascript
app.openApp(appUid, newTab)
```

**Parameters** 

| Parameter     | Description |
| :------------ | :---------- |
| appPageId     | The title to display in the dialog title bar. |
| appUid        | The message text to display. |
| newTab        | Optional. Can be one of "info", "success", "warn", or "error" and results in appropriate icon being displayed. If type is absent or not one of these values, then no icon will be displayed. |

**Example:**
```javascript
app.openApp('d1f6eb71-9483-479c-8d47-dd30bd7e9de9');
app.openApp ('d1f6eb71-9483-479c-8d47-dd30bd7e9de9', true);
app.openApp (app.getUID(), false);
```

### openAppPage {.section}

Opens the app page of an application that matches the provided *appPageid*.

**Syntax**
```javascript
app.openAppPage(appPageId, appUid, newTab)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| appPageId     | The id of the app page. |
| appUid        | Optional. The app uid, if not specified the current app uid is used. |
| newTab        | Optional. True or False.  If true, the app page will be opened in a new browser tab. Default is True. |

**Example:**
```javascript
app.openAppPage('AP_Page1');
app.openAppPage ('AP_Page1', true);
app.openAppPage ('AP_Page1', 'd1f6eb71-9483-479c-8d47-dd30bd7e9de9', false);
```

### openForm {.section}

Opens the form of an application that matches the provided *formId*.

**syntax**
```javascript
app.openForm(formId, appUid, newTab)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| formId        | The id of the form. |
| appUid        | Optional. The app uid, if not specified the current app uid is used. |
| newTab        | Optional. True or False.  If true, the form will be opened in a new browser tab. Default is True. |

**Example:**
```javascript
app.openForm('F_Form1');
app.openForm('F_Form1', true);
app.openForm ('F_Form1', false);

```

### openRecord {.section}

Opens the record of a form that matches the provided *recordId* and *formId*.

**Syntax**
```javascript
openRecord(recordUid, formId, appUid, newTab)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| recordUid     | The submitted record uid. |
| formId        | Optional. The form id, if not specified the current form id is used. |
| appUid        | Optional. The app uid, if not specified the current app uid is used. |
| newTab        | Optional. True or False.  If True, the record will be opened in a new browser tab. Default is True.|

**Example:**
```javascript
// open in new tab, only supply the record id
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx');

// open in a new tab, specify record uid and form id
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'F_Form2');

// open form in a new tab, specify the record uid and app uid
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy', true);

// open form in same tab, specify record uid, form id and app uid
app.openRecord('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'F_Form2', 'zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz', false);

```

### setSuppressWarning {.section}

If a user interacts with a form, or JavaScript, they are prompted with a warning message whenever the current browser page tries to navigate to a different URL. This function allows the suppression of that warning. When set to true the message is suppressed until it is set to false again.

**Syntax**
```javascript
app.setSuppressWarning (pSuppress)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pSuppress     | True or False. When true, message is suppressed. |


**Example:**
```javascript
// Can be used at any scope, for example in the application onStart, form onLoad, onItemChange, etc.
app.setSuppressWarning(true);
```

### showConfirmation {.section}

This function presents the user with a {{shortProductName}}-themed dialog that requires their input.  The input can be captured and used to control other form behavior.

You can configure any combination of buttons to appear in the dialog. You can also change the label of each button, this does not affect the return value when the button is pressed.

**Syntax**
```javascript
app.showConfirmation(title, message, type, subtitle, callbackFn, showYes, yesBtnTitle, showNo, noBtnTitle, showCancel, cancelBtnTitle, primaryBtn)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| title         | The title to display in the dialog title bar. |
| message       | The message text to display. |
| type         | Optional. Can be one of "info", "success", "warn", "question", or "error" and results in appropriate icon being displayed. If type is absent or not one of these values, then no icon will be displayed. |
| subtitle      | Optional. Heading text for the message. |
| callbackFn | a function to be called when a button is clicked in the dialog. The valid responses are 'Yes', 'No', 'Cancel'. |
| showYes | Shows the 'OK' button. If pressed the return value is 'Yes'. |
| yesBtnTitle | Set the label of the 'Yes' button. |
| showNo | Shows the 'No' button. If pressed the return value is 'No'. |
| noBtnTitle | Set the label of the 'No' button. |
| showCancel | Shows the 'Cancel' button. If pressed the return value is 'Cancel'. |
| cancelBtnTitle | Set the label of the 'Cancel' button. |
| primaryBtn | Will change the color of the specified button to the primary theme color. valid values are 'yes', 'no', and 'cancel'. |


**Example 1**

```javascript
app.getSharedData().handleConfirm = function (response)
{
  BO.F_SingleLine1.setValue(response);
  if (response === 'yes')
  {
    // take further action
    // . . .
  }
}

app.showConfirmation(
  'Dialog title', 
  'message', 
  'question', 
  'subtitle', 
  app.getSharedData().handleConfirm, 
  true, // show "Yes" button
  null, // use translated default "Yes"
  true, // show "No" button
  null, // use translated default "No"
  false, // show "Cancel" button
  null, // use translated default "Cancel"
  'yes' // the "Yes" button is the primary choice
);
```

**Example 2**

```javascript
app.showConfirmation('Confirm', 'Are you sure you want to delete?', 'warn', null, app.getSharedData().handleConfirm);
```

### showMessage {.section}

Allow usage of a built-in dialog for end-user messages.

**Syntax**
```javascript
app.showMessage(title, message, type, subtitle)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| title         | The title to display in the dialog title bar. |
| message       | The message text to display. |
| type         | Optional. Can be one of "info", "success", "warn", or "error" and results in appropriate icon being displayed. If type is absent or not one of these values, then no icon will be displayed. |
| subtitle      | Optional. Heading text for the message. |


**Example**

```javascript
if (BO.F_BookingDate.getValue() > BO.F_EventDate.getValue())
{
  app.showMessage (
  "Error found in data",
  "The booking date cannot be after the event.",
  "error",
  "Please change the booking or event date, then re-submit."
  );
}
```


**Parent topic:** [Interface objects](ref_jsapi_user_interface_objects.md)