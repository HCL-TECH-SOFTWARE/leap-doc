# Form Events 

This topic describes the Form Events, and their parameters when using JavaScript™ API in HCL Leap.

There are many events available to hook into on a form that are accessed from the forms **Edit Properties** dialog.

Table 1. JavaScript™ objects available in form events

|Variable|Full name|Description|Example|Type|
|--------|---------|-----------|-------|----|
|app|Application object|Contains functions for accessing global general information|`app.isSingleFormView()`|GUI|
|form|Form object|For accessing the pages and controlling page navigation|`form.getPage('P_Page1');`|GUI|
|BO|Business Object object|Top level data object for the form.|`BO.F_Username.getValue();`|DATA|

Table 2. Form Events

<table>
<tr>
<td> <b>Event</b> </td><td> <b>Description</b> <td><b>Example</b></td>
</tr>
<tr>
<td> afterSave </td>
<td>Called after the form is submitted or saved to the server. Changes made to the form in this event are lost, as it was already submitted.<td>Custom alert message:<br>

```javascript
alert('Thank you for submitting ' + app.getCurrentUser());
```
</tr>
<tr>
<td> beforeSave  
<td> Called just before the form is about to be submitted to the server. Any changes to data in the form are saved.
<td>Make a field lowercase before submission:

```javascript
BO.F_tag.setValue(BO.F_tag.getValue().toLowerCase()); 
```

</tr>
<tr>
<td>onDataReceived
<td>Applicable only when the form is hosted inside IBM® WebSphere® Portal. This event is called when the form receives data from another portlet. The data is provided with the pData parameter, which is a string containing arbitrary data passed in by portal.
<td>Update Info Message:

```javascript
form.getPage('P_Page1').F_Info.setContent(pData);
```

</tr>
<tr>
<td>onHide
<td>Called after the form is hidden.
<td>
</tr>
<tr>
<td>onDestruct
<td>Same as onHide. Legacy event.
<td>
</tr>
<tr>
<td>onLoad
<td>Called after data Business Object is attached to the Form, and its values loaded into the interface, whether it is a new form or an existing form. If the form is new, this event is called after onNew.
<td>Update the current Datetime into a Timestamp item:

```javascript
BO.F_Date.setValue(new Date()); 
```
</tr>
<tr>
<td>onNew
<td>Called when a blank form is created, and after the default values are loaded. Ideal location to pre-populate, or do first time setup of data.
<td>Populate an item with the current user:

```javascript
BO.F_User.setValue(app.getCurrentUser());
```

</tr>
<tr>
<td>onShow
<td>Called after the form is shown. This can occur after onNew and onLoad.
<td>
</tr>
<td>onShowActionButtons
<td>Called after the stage action buttons are created and shown.
<td>
</tr>
<tr>
<td>validateButtonPressed
<td>Called after every stage action button is pressed and the ID of the button is passed in as the pActionId parameter. Returning false in this event cancels the action taken by the button press.
<td>Verify the user is cancelling:

```javascript
if(pActionId === 'S_Cancel')
{    
   if(confirm('Are you sure you want to cancel?'))
       return true;
   return false;
} 
```

</tr>
</table>

**Parent topic: **[Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

