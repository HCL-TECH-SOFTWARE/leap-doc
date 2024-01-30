# Form Events {#formevents .reference}

This topic describes the Form Events, and their parameters when using JavaScript™ API in HCL Leap.

There are many events available to hook into on a form that are accessed from the forms **Edit Properties** dialog.

|Variable|Full name|Description|Example|Type|
|--------|---------|-----------|-------|----|
|app|Application object|Contains functions for accessing global general information|`app.isSingleFormView()`|GUI|
|form|Form object|For accessing the pages and controlling page navigation|`form.getPage('P_Page1');`|GUI|
|BO|Business Object object|Top level data object for the form.|`BO.F_Username.getValue();`|DATA|

|Event|Description|Example|
|-----|-----------|-------|
|afterSave|Called after the form is submitted or saved to the server. Changes made to the form in this event are lost, as it was already submitted.|Custom alert message:```
alert(“Thank you for submitting” + app.getCurrentUser());
```

|
|beforeSave|Called just before the form is about to be submitted to the server. Any changes to data in the form are saved.|Make a field lowercase before submission:```
BO.F_tag.setValue(BO.F_tag.getValue().toLowerCase()); 
```

|
|onDataReceived|Applicable only when the form is hosted inside IBM® WebSphere® Portal. This event is called when the form receives data from another portlet. The data is provided with the pData parameter, which is a string containing arbitrary data passed in by portal.|Update Info Message: ```
form.getPage('P_Page1').F_Info.setContent(pData);
```

|
|onHide|Called after the form is hidden.| |
|onDestruct|Same as onHide. Legacy event.| |
|onLoad|Called after data Business Object is attached to the Form, and its values loaded into the interface, whether it is a new form or an existing form. If the form is new, this event is called after onNew.|Update the current Datetime into a Timestamp item: ```
BO.F_Date.setValue(new Date()); 
```

|
|onNew|Called when a blank form is created, and after the default values are loaded. Ideal location to pre-populate, or do first time setup of data.|Populate an item with the current user:```
BO.F_User.setValue(app.getCurrentUser());
```

|
|onShow|Called after the form is shown. This can occur after onNew and onLoad.| |
|onShowActionButtons|Called after the stage action buttons are created and shown.| |
|validateButtonPressed|Called after every stage action button is pressed and the ID of the button is passed in as the pActionId parameter. Returning false in this event cancels the action taken by the button press.|Verify the user is cancelling: ```
if(pActionId === 'S_Cancel')
{    
   if(confirm('Are you sure you want to cancel?'))
       return true;
   return false;
} 
```

|

**Parent topic:**[Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

