# Form objects

Table 1. Form Object (form) The form object provides access to a number of functions that affect the entire form.

<table class="table-wrap">
<tr>
<td> <b>Object</b> </td><td> <b>Description</b> </td><td> <b>Example</b> </td>
</tr>
<tr>
<td>form.addClasses(classes)</td>
<td>Adds a list of custom class names to the form for dynamic CSS styling. The <b>classes</b> parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and <b>false</b> is returned.</td>
<td>

```javascript
form.addClasses('emphasized error');
```

</td>
</tr>
<tr>
<td>form.backwardPage()</td>
<td>Return the form to the previous page in navigation order. If the first page is reached, then nothing happens.</td>
<td>The following could be used to turn a regular button into a navigation button. In the <b>onClick</b> event of a button:

```javascript
form.backwardPage();
```

</td>
</tr>
<tr>
<td>form.connectEvent(eventName, callbackFunction)</td>
<td>Connects a function to an event on the form. This is useful for utility functions defined in external JavaScript™ files to hook behavior into the form dynamically. Returns a handle object that represents the connection of the function to that event name. The handle can be used to disconnect this same event using <b>form.disconnectEvent</b>.</td>
<td>If there is a F_CurrentUser field, then populate the currentUser:

```javascript
var hndl = form.connectEvent('onLoad', function()
{
   var currentUserField = form.getBO().F_CurrentUser;
   if (currentUserField) {
      currentUserField.setValue(app.getCurrentUser());
   }
});
```

</td>
</tr>
<tr>
<td>form.disconnectEvent(eventHandle)</td>
<td>Disconnects the event handler specified by the passed-in event handle object that was returned by a form.connectEvent call.  To avoid duplicate event handlers being connected, connect to events from within the application <b>onStart</b> or form <b>onLoad</b> events. If you connect to an event outside of these two events, you should explicitly disconnect from the event using the <b>disconnectEvent</b> method.</td>
<td>

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

</td>
</tr>
<tr>
<td>form.forwardPage()</td>
<td>Advance the form to the next page in navigation order. If the last page is reached, then nothing happens.</td>
<td>The following could be used to turn a regular button into a navigation button. In the <b>onClick</b> event of a button:

```javascript
form.forwardPage();
```

</td>
</tr>
<tr>
<td>form.getApp()</td>
<td>Returns the application object: app. Not a commonly used function, because within the form scope the <b>app</b> variable is also available.</td>
<td><!-- no example --></td>
</tr>
<tr>
<td>form.getBO()</td>
Returns the object that contains the Business Object data for the entire form.</td>
<td>This is commonly used in the application <b>onStart</b>, since at this scope the <b>form</b> variable is not defined.  

<td>

```javascript
var myForm = app.getForm('F_Form1');
var formBO = myForm.getBO();
formBO.F_SingleLine.setValue('setting the value using code!');
```

</td>
</tr>

<tr>
<td>
form.getClasses()
<td>
Returns an Array of custom class names currently applied to the form.
<td>
<!-- no example -->
</td>
</tr>

<tr>
<td>
form.getCurrentPage()
<td>
Gets the currently shown page. If there is no page shown, then <code>null</code> is returned. It is possible, though rarely desirable, to have all pages hidden.
<td>

```javascript
var pageShown = form.getCurrentPage();
if (pageShown === 'F_Page1')
   pageShown.F_Text.setContent('Changing the text of this text item when this page is shown.');
```

</td>
</tr>

<tr>
<td>
form.getId()
<td>
Returns the unique ID within the application of this form. For example, <code>'F_Form1'</code>.
</td>
<td>
<!-- no example -->
</td>
</tr>

<tr>
<td>
form.getPageIds()
<td>
Returns an array of the page IDs for the pages in this form.<br>
<td><!-- no example --></td>
</tr>

<tr>
<td>
form.getPage(pageId)
<td>
Returns the page object, page, for the page specified. Returns <code>null</code> if the <b>pageId</b> is invalid.
</td>
<td>
Get the specified page:<br>

```javascript
var thePage = form.getPage('F_Page1');
```

If the page exists then, navigate to that page:<br>

```javascript
if(thePage !== null) 
  form.selectPage('thePage')
```
</td>
</tr>

<tr>
<td>
form.getServiceConfigurationIds()
<td>
Returns an array of all the IDs for services mapped in this form.
<td>

```javascript
var serviceConfigs = form.getServiceConfigurationIds();
```
</td>
</tr>

<tr>
<td>
form.getServiceConfiguration(serviceId)
<td>
Gets the service object for a particular service ID.
</td>
<td>
Lookup and execute a service from JavaScript:

```javascript
var service = form.getServiceConfiguration('SC_ServiceConfig');
service.callService();
```
</td>
</tr>

<td>
form.getStageActions()
<td>
Returns an array of all the action buttons for the current stage. This includes any hidden action buttons as well.
</td>
<td>
Trigger a specific action using JavaScript:

```javascript
var actions = form.getStageActions():
for (var i=0; i<actions.length; i++) {
  if(get(actions,i).getId() === 'S_Submit')
  {
    get(actions,i).activate();
    break;
  }
}
```

<tr>
<td>
form.getType()
</td>
<td>
Returns a string identifying the object type. For example, <code>'form'</code>.
<td>
  <!-- no example -->
</td>

<tr>
<td>
form.removeClasses(classes)
<td>
Removes a list of custom class names from the form for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.
<td>

```javascript
form.removeClasses('emphasized error');
```
</td>

<tr>
<td>form.removePageFromNavigation(pageId)
<td>Removes the specified page from the navigation list for the form. The page navigation item no longer visits that page when <b>next</b>, or <b>previous</b> is selected, nor can you switch to that page programmatically.
<td>
If the check is selected, remove page 2 from the navigation:
 
```javascript
if(BO.F_Check.getValue())
  form.removePageFromNavigation('P_Page2');
```
</td>

<tr>
<td>
form.restorePageNavigation(pageId)
<td>Restores a previously removed page back into the navigation list for the form.
<td>
If the check is not selected, restore page 2 into the navigation:<br>

```javascript
if(!BO.F_Check.getValue())
  form.restorePageNavigation('P_Page2');
```

<tr>
<td>
form.selectPage(pageId)
<td>
Switches to the specified page. If the page is removed from navigation by Stages, Rules, or JavaScript, then you cannot select it.
<td>Get the specified page:<br>

```javascript
var thePage = form.getPage('F_Page1');
```

If the page exists then navigate to that page:<br>

```javascript
if (thePage !== null) 
  form.selectPage('F_Page1');
```

</td>
</tr>
</table>

**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)

