# Other objects 

## Table 1. Service Configuration Object
This object represents a mapped service in the form and is retrieved using `form.getServiceConfiguration()`.

<table class="table-wrap">
<tr>
<td width="200"><b>Object</b> </td><td> <b>Description</b> <td><b>Example</b></td>
</tr>
<tr>
<td>service.callService()
<td>Executes the service.
<td>

```javascript
var serviceConfig = form.getServiceConfiguration('SC_ServiceConfig');
serviceConfig.callService();
```
</tr>
<tr>
<td>service.connectEvent (eventName, callbackFunction)
<td>The only supported event is <b>onCallFinished</b>, which is called every time after the service mapping is executed. It is passed two parameters:
<ul>
<li>  <b>pSuccess</b>, which indicates whether the service call succeeded.</li>
<li>  <b>pErrorObj</b>, which is a JSON object (<code>{code: '', message: '', handled: ''}</code>) that contains details about the error (if thrown).</li></ul>

If the error is being handled by javascript, setting <code>pErrorObj.handled = true</code> will suppress the error dialog.<br>
<br>

Resister these events in the Applications <b>onStart</b> event so that they are only registered once.
<td> 

```javascript
var form = app.getForm('F_Form1');
var serviceConfig = form.getServiceConfiguration('SC_ServiceConfig');
serviceConfig.connectEvent('onCallFinished', function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  } else {    
    //do something with the error
    form.getBO().F_Error.setValue(pErrorObj.code + ': ' + pErrorObj.message); 
    pErrorObj.handled = true; //suppress error dialog
  }
});

```
</tr>
<tr>
<td>service.disconnectEvent (eventHandle)
<td>Disconnects the event handler specified by the passed-in event handle object that was returned by a <b>service.connectEvent</b> call. To avoid duplicate event handlers being connected, connect to events from within the application <b>onStart</b> or form <b>onLoad</b> events. If you connect to an event outside of these two events, you should explicitly disconnect from the event using the <b>disconnectEvent</b> method.
<td> 

```javascript 
var form = app.getForm('F_Form1');
var serviceConfig = form.getServiceConfiguration('SC_ServiceConfig');
var serviceHdl = serviceConfig.connectEvent('onCallFinished', function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  }
  serviceConfig.disconnectEvent(serviceHdl);
});
```

</tr>
</table>

## Table 2. Stage Action Button Object
Represents an action button that is retrieved by calling `form.getStageActions()`.


<table class="table-wrap">
<tr>
<td width="200"><b>Object</b> </td><td> <b>Description</b></td>
</tr>
<tr>
<td>action.activate()
<td>Triggers this button, which cancels, submits or saves a draft of the form.<br> <b>Note:</b> If a button is hidden by a Rule, you can try and activate it; however, the server will reject the submission.
<td> 

```javascript
var actionButtons = form.getStageActions();
for (var i=0; i<actionButtons.length; i++) {
   var actionButton = get(actionButtons, i);
   if (actionButton.getId() === 'S_Cancel') {
      actionButton.activate();
   }
}
```

</tr>
<tr>
<td>action.addClasses(classes)
<td>Adds a list of custom class names to an action for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.
<td>

```javascript
action.addClasses('emphasized error');
```

</tr>
<tr>
<td>action.getActionType()
<td>Returns a string that identifies the type of the button. Values are <code>'Cancel'</code>, <code>'Submit'</code>, and <code>'Save'</code>.
<td>
</tr>

<tr>
<td>action.getActive()
<td>Returns true if this button is active, and false if it is disabled.
<td>
</tr>

<tr>
<td>action.getClasses()
<td>Returns an Array of custom class names currently applied to an action.
<td>
</tr>

<tr>
<td>action.getId()
<td>Returns the unique ID (within the application) of this action button 'S_Submit'.
<td>
</tr>

<tr>
<td>action.getTitle()
<td>Returns the user-defined title of this button.
<td>
</tr>
<tr>
<td>action.getVisible()
<td>Returns true if this button is visible, or false if it is hidden by a rule or JavaScript™.
<td>
</tr>

<tr>
<td>action.removeClasses (classes)
<td>Removes a list of custom class names from an action for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.
<td>

```javascript
action.removeClasses('emphasized error');
```

</tr>

<tr>
<td>action.setActive(active)
<td>If active is true, then the button is made active. If false, the button is disabled.
<td>
</tr>
<tr>
<td>action.setFocus()
<td>Causes this button to receive focus, if possible.
<td>
</tr>
<tr>
<td>action.setTitle(title)
<td>Sets the title for the button.
<td>
</tr>
<tr>
<td>action.setVisible(visible)
<td>Sets whether this action is visible. <br>
<b>Note:</b> If this item is made invisible by a rule, then you cannot unhide it by calling this function.
<td>
</tr>
</table>


**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)

