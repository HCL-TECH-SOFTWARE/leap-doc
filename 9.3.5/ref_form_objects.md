# Form objects {#ref_form_objects .concept}

|Object|Description|Example|
|------|-----------|-------|
|form.addClasses\(classes\)|Adds a list of custom class names to the form for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.|```
form.addClasses(“emphasized error”);
```

|
|form.backwardPage\(\)|Return the form to the previous page in navigation order. If the first page is reached, then nothing happens.|The following could be used to turn a regular button into a navigation button. In the **onClick** event of a button: ```
form.backwardPage();
```

|
|form.connectEvent\(eventName, callbackFunction\)|Connects a function to an event on the form. This is useful for utility functions defined in external JavaScript™ files to hook behavior into the form dynamically. Returns a handle object that represents the connection of the function to that event name. The handle can be used to disconnect this same event using form.disconnectEvent.|If there is a F\_CurrentUser field, then populate the currentUser:```
var hndl = form.connectEvent('onLoad', function()
     {
     if(form.getBO().F_CurrentUser)
form.getBO().F_CurrentUser.setValue(app.getCurrentUser());
     }
     });
```

|
|form.disconnectEvent\(eventHandle\)|Disconnects the event handler specified by the passed-in event handle object that was returned by a form.connectEvent call.To avoid duplicate event handlers being connected, connect to events from within the application **onStart** or form **onLoad** events. If you connect to an event outside of these two events, you should explicitly disconnect from the event using the **disconnectEvent** method.

|```
var hndl = form.connectEvent('onLoad', function()
{
  if(form.getBO().F_CurrentUser)
     form.getBO().F_CurrentUser.setValue(app.getCurrentUser());
  }
  form.disconnectEvent(hndl);
});
```

|
|form.forwardPage\(\)|Advance the form to the next page in navigation order. If the last page is reached, then nothing happens.|The following could be used to turn a regular button into a navigation button. In the **onClick** event of a button: ```
form.forwardPage();
```

|
|form.getApp\(\)|Returns the application object: app. Not a commonly used function, because within the form scope the “app” variable is also available.| |
|form.getBO\(\)|Returns the object that contains the Business Object data for the entire form.|This is commonly used in the application **onStart**, since at this scope the “form” variable is not defined. ```
var myForm = app.getForm('F_Form1');
var formBO = myForm.getBO();
formBO.F_SingleLine.setValue('setting the value using code!');
```

|
|form.getClasses\(\)|Returns an Array of custom class names currently applied to the form.| |
|form.getCurrentPage\(\)|Gets the currently shown page. If there is no page shown, then null is returned. It is possible, though rarely desirable, to have all pages hidden.|```
var pageShown = form.getCurrentPage();
if(pageShown === 'F_Page1')
  pageShown.F_Text.setContent('Changing the text of this text item when this page is shown.');
```

|
|form.getId\(\)|Returns the unique ID within the application of this form. For example, F\_Form1.| |
|form.getPageIds\(\)|Returns an array of the page IDs for the pages in this form.| |
|form.getPage\(pageId\)|Returns the page object, page, for the page specified. Returns null if the pageId is invalid.|Get the specified page:```
 var thePage = form.getPage('F_Page1');
```

 If the page exists then, navigate to that page:```
if(thePage !== null) 
  form.selectPage('thePage')
```

|
|form.getServiceConfigurationIds\(\)|Returns an array of all the IDs for services mapped in this form.|```
var serviceConfigs = form.getServiceConfigurationIds();
```

|
|form.getServiceConfiguration\(serviceId\)|Gets the service object for a particular service ID.|Lookup and execute a service from JavaScript:```
var service = form.getServiceConfiguration('SC_ServiceConfig');
     service.callService();
```

|
|form.getStageActions\(\)|Returns an array of all the action buttons for the current stage. This includes any hidden action buttons as well.|Trigger a specific action using JavaScript:```
var actions = form.getStageActions():
for(var i=0; i<actions.length; i++)
     {
     if(get(actions,i).getId() === 'S_Submit')
     {
     get(actions,i).activate();
     break;
     }
     }
```

|
|form.getType\(\)|Returns a string identifying the object type. For example, form.| |
|form.removeClasses\(classes\)|Removes a list of custom class names from the form for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.|```
form.removeClasses(“emphasized”);
```

|
|form.removePageFromNavigation\(pageId\)|Removes the specified page from the navigation list for the form. The page navigation item no longer visits that page when **next**, or **previous** is selected, nor can you switch to that page programmatically.|If the check is selected, remove page 2 from the navigation:```
if(BO.F_Check.getValue)
  form.removePageFromNavigation('P_Page2');
```

 |
|form.restorePageNavigation\(pageId\)|Restores a previously removed page back into the navigation list for the form.|If the check is not selected, restore page 2 into the navigation:```
 if(!BO.F_Check.getValue)
  form.restorePageNavigation('P_Page2');
```

|
|form.selectPage\(pageId\)|Switches to the specified page. If the page is removed from navigation by Stages, Rules, or JavaScript, then you cannot select it.|Get the specified page:```
 var thePage = form.getPage('F_Page1');
```

 If the page exists then navigate to that page:```
if(thePage !== null) 
  form.selectPage(thePage);
```

|
|form.sendData\(data\)|For IBM® WebSphere® Portal only. When hosted in a portlet, calling this method sends the string to any subscribers to the portlet. The content of this string depends on the portlet that consumes it.|Send a URL to be processed by the wire connected to the portlet:  ```
form.sendData(BO.F_ServerURL.getValue() + "/apps/secure/org/app/b5806ef1-b784-4c85-8844-653cd4064201/launch/index.html?form=F_FormA"); 
```

|

**Parent topic:**[Interface objects](ref_jsapi_user_interface_objects.md)

