# Form objects

The form object (form) provides access to a number of functions that affect the entire form.

## addClasses {.section}

Adds a list of custom class names to the form for dynamic CSS styling. The **classes** parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and **false** is returned.

**Syntax**

```javascript
form.addClasses(classes)
```

**Example**

```javascript
form.addClasses('emphasized error');
```

## backwardPage {.section}

Return the form to the previous page in navigation order. If the first page is reached, then nothing happens.

**Syntax**

```javascript
form.backwardPage()
```

**Example**

The following could be used to turn a regular button into a navigation button. In the **onClick** event of a button:

```javascript
form.backwardPage();
```

## connectEvent { #connectevent-section .section }

Connects a function to an event on the form. This is useful for utility functions defined in external JavaScript™ files to hook behavior into the form dynamically. Returns a handle object that represents the connection of the function to that event name. The handle can be used to disconnect this same event using [form.disconnectEvent](#disconnectevent-section).

**Syntax**

```javascript
form.connectEvent(eventName, callbackFunction)
```

**Example**

If there is a F_CurrentUser field, then populate the currentUser:

```javascript
var hndl = form.connectEvent('onLoad', function()
{
   var currentUserField = form.getBO().F_CurrentUser;
   if (currentUserField) {
      currentUserField.setValue(app.getCurrentUser());
   }
});
```

## disconnectEvent { #disconnectevent-section .section }

Disconnects the event handler specified by the passed-in event handle object that was returned by a [form.connectEvent](#connectevent-section) call.  To avoid duplicate event handlers being connected, connect to events from within the application **onStart** or form **onLoad** events. If you connect to an event outside of these two events, you should explicitly disconnect from the event using this method.

**Syntax**

```javascript
form.disconnectEvent(eventHandle)
```

**Example**

```javascript
var hndl = form.connectEvent('onLoad', function()
{
   var currentUserField = form.getBO().F_CurrentUser;
   if (currentUserField) {
       currentUserField.setValue(app.getCurrentUser());
   }
   form.disconnectEvent(hndl);
});
```

## forwardPage {.section}

Advance the form to the next page in navigation order. If the last page is reached, then nothing happens.

**Syntax**

```javascript
form.forwardPage()
```

**Example**

The following could be used to turn a regular button into a navigation button. In the **onClick** event of a button:

```javascript
form.forwardPage();
```

## getApp {.section}

Returns the application object: app. Not a commonly used function, because within the form scope the **app** variable is also available.

**Syntax**

```javascript
form.getApp()
```

## getBO {.section}

Returns the object that contains the Business Object data for the entire form.

**Syntax**

```javascript
form.getBO()
```

**Example**

This is commonly used in the application **onStart**, since at this scope the **form** variable is not defined.  

```javascript
var myForm = app.getForm('F_Form1');
var formBO = myForm.getBO();
formBO.F_SingleLine.setValue('setting the value using code!');
```

## getClasses {.section}

Returns an Array of custom class names currently applied to the form.

**Syntax**

```javascript
form.getClasses()
```

## getCurrentPage {.section}

Gets the currently shown page. If there is no page shown, then **null** is returned. It is possible, though rarely desirable, to have all pages hidden.

**Syntax**

```javascript
form.getCurrentPage()
```

**Example**

```javascript
var pageShown = form.getCurrentPage();
if (pageShown === 'F_Page1')
   pageShown.F_Text.setContent('Changing the text of this text item when this page is shown.');
```

## getId {.section}

Returns the unique ID within the application of this form. For example, **'F_Form1'**.

**Syntax**

```javascript
form.getId()
```

## getPage {.section}

Returns the page object, page, for the page specified. Returns **null** if the **pageId** is invalid.

**Syntax**

```javascript
form.getPage(pageId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pageId     | The id of the page. |

**Example**

```javascript
// Get the specified page
var thePage = form.getPage('F_Page1');

// If the page exists then, navigate to that page
if(thePage !== null) 
  form.selectPage('thePage')
```

## getServiceConfigurationIds {.section}

Returns an array of all the IDs for services mapped in this form.

**Syntax**

```javascript
form.getServiceConfigurationIds()
```

**Example**

```javascript
var serviceConfigs = form.getServiceConfigurationIds();
```

## getPageIds {.section}

Returns an array of the page IDs for the pages in this form.

**Syntax**

```javascript
form.getPageIds()
```

## getServiceConfiguration {.section}

Gets the service object for a particular service ID.

**Syntax**

```javascript
form.getServiceConfiguration(serviceId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| serviceId     | The id of the service configuration. |

**Example**

```javascript
// Lookup and execute a service from JavaScript
var service = form.getServiceConfiguration('SC_ServiceConfig');
service.callService();
```

## getStageActions {.section}

Returns an array of all the action buttons for the current stage. This includes any hidden action buttons as well.

**Syntax**

```javascript
form.getStageActions()
```

**Example**

```javascript
// Trigger a specific action using JavaScript
var actions = form.getStageActions():
for (var i=0; i<actions.length; i++) {
  if(get(actions,i).getId() === 'S_Submit')
  {
    get(actions,i).activate();
    break;
  }
}
```

```javascript
/*
* Hides all the stage buttons that are specified.
* 
* USAGE:
* app.getSharedData().hideStageButtons(form, ["S_Submit", "S_Submit1"]);
*/
app.getSharedData().hideStageButtons = function(theForm, btnList) {

 var actionButtons = theForm.getStageActions();
 for(var i=0; i<actionButtons.length; i++){
  for(var j=0;j<btnList.length;j++) {
    if(get(btnList, j) === get(actionButtons, i).getId())
       get(actionButtons, i).setVisible(false);
   }      
 }
}
```

## getType {.section}

Returns a string identifying the object type. For example, **'form'**.

**Syntax**

```javascript
form.getType()
```

## removeClasses {.section}

Removes a list of custom class names from the form for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.

**Syntax**

```javascript
form.removeClasses(classes)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| classes       | List of CSS classnames separated by spaces, or an array of class names. |

**Example**

```javascript
form.removeClasses('emphasized error');
```

## removePageFromNavigation {.section}

Removes the specified page from the navigation list for the form. The page navigation item no longer visits that page when **next**, or **previous** is selected, nor can you switch to that page programmatically.

**Syntax**

```javascript
form.removePageFromNavigation(pageId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pageId        | The id of the page. |

**Example**

```javascript
// If the check is selected, remove page 2 from the navigation
if(BO.F_Check.getValue())
  form.removePageFromNavigation('P_Page2');
```

## restorePageNavigation {.section}

Restores a previously removed page back into the navigation list for the form.

**Syntax**

```javascript
form.restorePageNavigation(pageId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pageId        | The id of the page. |

**Example**

```javascript
// If the check is not selected, restore page 2 into the navigation
if(!BO.F_Check.getValue())
  form.restorePageNavigation('P_Page2');
```

## selectPage {.section}

Switches to the specified page. If the page is removed from navigation by Stages, Rules, or JavaScript, then you cannot select it.

**Syntax**

```javascript
form.selectPage(pageId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pageId        | The id of the page. |

**Example**

```javascript
// Get the specified page
var thePage = form.getPage('F_Page1');

// If the page exists then navigate to that page
if (thePage !== null) 
  form.selectPage('F_Page1');
```

**Parent topic:** [Interface objects](ref_jsapi_user_interface_objects.md)
