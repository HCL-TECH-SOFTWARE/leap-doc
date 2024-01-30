# Page and App Page objects {#ref_page_app_page_objects .concept}

|Object|Description|Example|
|------|-----------|-------|
|page.<itemId\>appPage.<itemId\>

|Provides convenient direct access to all items on the page, including those inside Sections and Tab Folders.|Hide a specific button on the page:```
page.F_NextButton.setVisible(false);
```

|
|page.addClasses\(classes\)appPage.addClasses\(classes\)

|Adds a list of custom class names to the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.|```
page.addClasses(“emphasized error”);
```

|
|page.connectEvent\(eventName, callbackFunction\)appPage.connectEvent\(eventName, callbackFunction\)

|Connects a function to an event on the page. The list of events is the same as for the page in the Design interface. Useful for utility functions defined in JavaScript™ files to hook behavior into the page dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using page.disconnectEvent or appPage.disconnectEvent.| |
|page.disconnectEvent\(eventHandle\)appPage.disconnectEvent\(eventHandle\)

|Disconnects the event handler specified by the passed-in event handle object that was returned by a page.connectEvent or **appPage.connectEvent** call. To avoid duplicate event handlers being connected to pages, connect to page events from within the application **onStart** or form **onLoad** events. If you connect to a page event outside of these two events you should explicitly disconnect from the page event using the **disconnectEvent** method.|``` {#codeblock_wlb_xr5_vvb}
var eventHdl = page.connectEvent("<some event>", function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  }
  page.disconnectEvent(eventHndl);
});
```

|
|page.getBO\(\)|Returns the object that contains the Business Object data for the entire form.|```
var theBO = page.getBO();
theBO.F_SingleLine.setValue('new Value');
```

|
|page.getChildren\(\)appPage.getChildren\(\)

|Returns the list object that provides access to all direct children items for this page. For example, items in a Section on the page are not in the list, however the Section itself is. The list object has the getLength\(\) function and get\(index\) function for accessing the objects in the list.|Hide all button items on a page:```
var list = page.getChildren();
     for(var i=0; i<list.getLength(); i++)
     {
     if(list.get(i).getType() === 'button')
     list.get(i).setVisible(false);
     }
```

|
|page.getClasses\(\)appPage.getClasses\(\)

|Returns an Array of custom class names currently applied to the page.| |
|page.getForm\(\)|Returns the form object to which this page belongs.| |
|page.getId\(\)appPage.getId\(\)

|Returns the unique ID, within the application, of this page. For example, P\_Page1.| |
|appPage.getServiceConfigurationIds\(\)|Returns an array of all the IDs for services mapped in this app page.|```
var serviceConfigs = appPage.getServiceConfigurationIds();
```

|
|appPage.getServiceConfiguration\(serviceId\)|Gets the service object for a particular service ID.|Lookup and execute a service from JavaScript™:```
var service = appPage.getServiceConfiguration('SC_ServiceConfig');
     service.callService();
```

|
|page.getType\(\)appPage.getType\(\)

|Returns a string identifying the object type. For example,“page”.| |
|page.getVisibility\(\)|Returns true if the page is being shown, and false if it is hidden.| |
|page.removeClasses\(classes\)appPage.removeClasses\(classes\)

|Removes a list of custom class names from the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.|```
page.removeClasses(“emphasized”);
```

|

**Parent topic:**[Interface objects](ref_jsapi_user_interface_objects.md)

