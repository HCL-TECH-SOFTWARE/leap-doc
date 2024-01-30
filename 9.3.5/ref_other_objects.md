# Other objects {#ref_other_objects .concept}

|Object|Description|Example|
|------|-----------|-------|
|service.callService\(\)|Executes the service.| |
|service.connectEvent\(eventName, callbackFunction\)|The only supported event is **onCallFinished**, which is called every time after the service mapping is executed. It is passed two parameters:-   pSuccess, which indicates whether the service call succeeded.
-   pErrorObj, which is a JSON object \(\{code: '', message: '', handled: ''\}\) that contains details about the error \(if thrown\).

If the error is being handled by javascript, setting `pErrorObj.handled = true` will suppress the error dialog.

Resister these events in the Applications onStart event so that they are only registered once.

|```
var form = app.getForm('F_Form1');
var serviceConfig = form.getServiceConfiguration("SC_ServiceConfig");
serviceConfig.connectEvent("onCallFinished", function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  } else {    
    //do something with the error
    form.getBO().F_Error.setValue(pErrorObj.code + “: ” + pErrorObj.message); 
    pErrorObj.handled = true; //suppress error dialog
  }
});

```

|
|service.disconnectEvent\(eventHandle\)|Disconnects the event handler specified by the passed-in event handle object that was returned by a service.connectEvent call.To avoid duplicate event handlers being connected, connect to events from within the application **onStart** or form **onLoad** events. If you connect to an event outside of these two events, you should explicitly disconnect from the event using the **disconnectEvent** method.

|``` {#codeblock_i2t_5r5_vvb}
var form = app.getForm('F_Form1');
var serviceConfig = form.getServiceConfiguration("SC_ServiceConfig");
var serviceHdl = serviceConfig.connectEvent("onCallFinished", function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  }
  serviceConfig.disconnectEvent(serviceHdl);
});
```

|

|Object|Description| |
|------|-----------|--|
|action.activate\(\)|Triggers this button, which cancels, submit or save the form. **Note:** If a button is hidden by a Rule, you can try and fire it. However, the server rejects the submission.

|```
var actionButtons = form.getStageActions();
for(var i=0; i<actionButtons.length; i++){
  if(get(actionButtons, i).getId() === 'S_Cancel')
     get(actionButtons, i).activate();
}
```

|
|action.addClasses\(classes\)|Adds a list of custom class names to an action for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.|```
action.addClasses(“emphasized error”);
```

|
|action.getActionType\(\)|Returns a string that identifies the type of the button. Values are **Cancel**, **Submit**, and **Save**.| |
|action.getActive\(\)|Returns true if this button is active, and false if it is disabled.| |
|action.getClasses\(\)|Returns an Array of custom class names currently applied to an action.| |
|action.getId\(\)|Returns the unique ID \(within the application\) of this action button “S\_Submit”.| |
|action.getTitle\(\)|Returns the user-defined title of this button.| |
|action.getVisible\(\)|Returns true if this button is visible, or false if it is hidden by a rule or JavaScript™.| |
|action.removeClasses\(classes\)|Removes a list of custom class names from an action for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.|```
action.removeClasses(“emphasized”);
```

|
|action.setActive\(active\)|If active is true, then the button is made active. If false, the button is disabled.| |
|action.setFocus\(\)|Causes this button to receive focus, if possible.| |
|action.setTitle\(title\)|Sets the title for the button.| |
|action.setVisible\(visible\)|Sets whether this action is visible. **Note:** If this item is made invisible by a rule, then you cannot unhide it by calling this function.

| |

**Parent topic:**[Interface objects](ref_jsapi_user_interface_objects.md)

