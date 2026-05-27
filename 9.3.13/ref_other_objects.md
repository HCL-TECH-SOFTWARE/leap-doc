# Other objects 

## Service Configuration Object

This object represents a mapped service in the form and is retrieved using `form.getServiceConfiguration()`.

### callService

Executes the service.

**Syntax**
```javascript
service.callService()
```

**Example**
```javascript
var serviceConfig = form.getServiceConfiguration('SC_ServiceConfig');
serviceConfig.callService();
```


### connectEvent

The only supported event is  **onCallFinished**, which is called every time after the service mapping is executed. It is passed two parameters:
  - **pSuccess**, which indicates whether the service call succeeded.
  - **pErrorObj**, which is a JSON object (<code>{code: '', message: '', handled: ''}</code>) that contains details about the error (if thrown).

If the error is being handled by javascript, setting <code>pErrorObj.handled = true</code> will suppress the error dialog.

Resister these events in the Applications  **onStart** event so that they are only registered once.

**Syntax**
```javascript
service.connectEvent (eventName, callbackFunction)
``` 

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| eventName     | Only supported event is 'onCallFinished' |
| callbackFunction | A function that is executed based on the service eventName |

**Example**
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


### disconnectEvent

Disconnects the event handler specified by the passed-in event handle object that was returned by a  **service.connectEvent** call. 

To avoid duplicate event handlers being connected, connect to events from within the application  **onStart** or form  **onLoad** events. 

If you connect to an event outside of these two events, you should explicitly disconnect from the event using the  **disconnectEvent** method.

**Syntax**
```javascript
service.disconnectEvent (eventHandle)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| eventHandle   | The object returned from the service.connectEvent call |

**Example**
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

## Stage Action Button Object

Represents an action button that is retrieved by calling `form.getStageActions()`.


### activate

Triggers this button, which cancels, submits or saves a draft of the form.

!!! note
    If a button is hidden by a Rule, you can try and activate it; however, the server will reject the submission.

**Syntax**
```javascript
action.activate()
```

**Example**
```javascript
var actionButtons = form.getStageActions();
for (var i=0; i<actionButtons.length; i++) {
   var actionButton = get(actionButtons, i);
   if (actionButton.getId() === 'S_Cancel') {
      actionButton.activate();
   }
}
```


### addClasses

Adds a list of custom class names to an action for dynamic CSS styling. 

If any of the given class names are invalid CSS class names, then no classes are added and false is returned.

**Syntax**
```javascript
action.addClasses(classes)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| classes    | Single class name, a list of CSS class names separated by spaces or an array of class names |

**Example**
```javascript
action.addClasses('emphasized error');
```


### getActionType

Returns a string that identifies the type of the button. Values are <code>'Cancel'</code>, <code>'Submit'</code>, and <code>'Save'</code>.

**Syntax**
```javascript
action.getActionType()
```


### getActive

Returns true if this button is active, and false if it is disabled.

**Syntax**
```javascript
action.getActive()
```


### getClasses

Returns an Array of custom class names currently applied to an action.

**Syntax**
```javascript
action.getClasses()
```


### getId

Returns the unique ID (within the application) of this action button 'S_Submit'.

**Syntax**
```javascript
action.getId()
```


### getTitle

Returns the user-defined title of this button.

**Syntax**
```javascript
action.getTitle()
```


### getVisible

Returns true if this button is visible, or false if it is hidden by a rule or JavaScript™.

**Syntax**
```javascript
action.getVisible()
```


### removeClasses

Removes a list of custom class names from an action for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.

**Syntax**
```javascript
action.removeClasses (classes)
```

**Example**
```javascript
action.removeClasses('emphasized error');
```


### setActive

If active is true, then the button is made active. If false, the button is disabled.

**Syntax**
```javascript
action.setActive(active)
```


### setFocus

Causes this button to receive focus, if possible.

**Syntax**
```javascript
action.setFocus()
```


### setTitle

Sets the title for the button.

**Syntax**
```javascript
action.setTitle(title)
```


### setVisible

Sets whether this action is visible.

!!! note
    If this item is made invisible by a rule, then you cannot make it visible it by calling this function.

**Syntax**
```javascript
 action.setVisible(visible)
```


**Parent topic:** [Interface objects](ref_jsapi_user_interface_objects.md)

