# Form Events 

This topic describes the Form Events, and their parameters when using JavaScript™ API in HCL Leap.

There are many events available to hook into on a form that are accessed from the forms **Edit Properties** dialog.

## JavaScript™ objects

|Variable|Full name|Description|Example|Type|
|--------|---------|-----------|-------|----|
|app|Application object|Contains functions for accessing global general information|`app.isSingleFormView()`|GUI|
|form|Form object|For accessing the pages and controlling page navigation|`form.getPage('P_Page1');`|GUI|
|BO|Business Object object|Top level data object for the form.|`BO.F_Username.getValue();`|DATA|


## afterSave

Called after the form is submitted or saved to the server. Changes made to the form in this event are lost, as it was already submitted.

**Example**

Custom alert message:
```javascript
alert('Thank you for submitting ' + app.getCurrentUser());
```


## beforeSave  

Called just before the form is about to be submitted to the server. Any changes to data in the form are saved.

**Example**

Make a field lowercase before submission:
```javascript
BO.F_tag.setValue(BO.F_tag.getValue().toLowerCase()); 
```

## onDataReceived
Applicable only when the form is hosted inside IBM® WebSphere® Portal. This event is called when the form receives data from another portlet. The data is provided with the pData parameter, which is a string containing arbitrary data passed in by portal.

**Example**

Update Info Message:
```javascript
form.getPage('P_Page1').F_Info.setContent(pData);
```

## onHide

Called after the form is hidden.


## onDestruct

Same as onHide. Legacy event.

## onLoad

Called after data Business Object is attached to the Form, and its values loaded into the interface, whether it is a new form or an existing form. If the form is new, this event is called after onNew.

**Example**

Update the current Datetime into a Timestamp item:
```javascript
BO.F_Date.setValue(new Date()); 
```


## onNew

Called when a blank form is created, and after the default values are loaded. Ideal location to pre-populate, or do first time setup of data.

**Example**

Populate an item with the current user:
```javascript
BO.F_User.setValue(app.getCurrentUser());
```


## onShow

Called after the form is shown. This can occur after onNew and onLoad.


## onShowActionButtons

Called after the stage action buttons are created and shown.


## validateButtonPressed
Called after every stage action button is pressed and the ID of the button is passed in as the pActionId parameter. Returning false in this event cancels the action taken by the button press.

**Examples**

Verify the user is cancelling:
```javascript
if(pActionId === 'S_Cancel')
{    
   return confirm('Are you sure you want to cancel?');
} 
```

Have the user confirm their submit action:
```javascript
if(pActionId === 'S_Submit') {
  var msg = "BY CLICKING ON THE 'OK' BUTTON, YOU AGREE TO THE TERMS OF THIS  AGREEMENT. IF YOU ARE ACCEPTING THESE TERMS ON BEHALF OF A COMPANY OR OTHER LEGAL ENTITY, YOU REPRESENT AND WARRANT THAT YOU HAVE FULL AUTHORITY TO BIND SUCH COMPANY OR OTHER LEGAL ENTITY TO THESE TERMS IN WHICH CASE THE TERMS WILL REFER TO SUCH ENTITY. THE AGREEMENT IS EFFECTIVE AS OF THE DATE YOU ACCEPT THESE TERMS ('Effective Date').\n\nIF YOU DO NOT HAVE SUCH AUTHORITY, OR IF YOU DO NOT AGREE TO THESE TERMS, DO NOT CLICK THE 'OK' BUTTON";

  return confirm(msg);
}
```

Do not allow submission if a table item does not contain the minimum number of rows:
```javascript
if(pActionId === "S_Submit") {
 
  if(BO.F_Table.getLength() < 5) {
    alert("A minimum of 5 rows must be provided in the table before submitting the form. You currently have " + BO.F_Table.getLength() + ".");
    return false;
  }
}
```

**Parent topic:** [Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

