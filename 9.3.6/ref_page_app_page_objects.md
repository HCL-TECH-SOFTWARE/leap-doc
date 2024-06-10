# Page and App Page objects 

## itemId

Provides convenient direct access to all items on the page, including those inside Sections and Tab Folders.

### Syntax
```javascript
page.<itemId>;
appPage.<itemId>;
```

### Example

Hide a specific button on the page:

```javascript
page.F_NextButton.setVisible(false);
```


## addClasses

Adds a list of custom class names to the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.

### Syntax

```javascript
page.addClasses(classes)
appPage.addClasses(classes)
```

### Example 

```javascript
page.addClasses('emphasized error');
```

## connectEvent

Connects a function to an event on the page. The list of events is the same as for the page in the Design interface. Useful for utility functions defined in JavaScript™ files to hook behavior into the page dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using page.disconnectEvent or appPage.disconnectEvent.

### Syntax
```javascript
page.connectEvent(eventName,callbackFunction)
appPage.connectEvent(eventName,callbackFunction)
```


## disconnectEvent

Disconnects the event handler specified by the passed-in event handle object that was returned by a page.connectEvent or <b>appPage.connectEvent</b> call. To avoid duplicate event handlers being connected to pages, connect to page events from within the application <b>onStart</b> or form <b>onLoad</b> events. If you connect to a page event outside of these two events you should explicitly disconnect from the page event using the <b>disconnectEvent</b> method.

### Syntax
```javascript
page.disconnectEvent(eventHandle)
appPage.disconnectEvent (eventHandle)
```

### Example

```javascript 
var eventHdl = page.connectEvent("<some event>", function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  }
  page.disconnectEvent(eventHndl);
});
```


## getBO

Returns the object that contains the Business Object data for the entire form.

### Syntax
```javascript
page.getBO()
```

### Example
```javascript
var theBO = page.getBO();
theBO.F_SingleLine.setValue('new Value');
```

## getChildren

Returns the list object that provides access to all direct children items for this page. For example, items in a Section on the page are not in the list, however the Section itself is. The list object has the getLength() function and get(index) function for accessing the objects in the list.

### Syntax
```javascript
page.getChildren()
appPage.getChildren()
```

### Example

Hide all button items on a page:
```javascript
var list = page.getChildren();
for (var i=0; i<list.getLength(); i++) {
   if list.get(i).getType() === 'button') {
      list.get(i).setVisible(false);
   }
}
```

## getClasses

Returns an Array of custom class names currently applied to the page.

### Syntax
```javascript
page.getClasses()
appPage.getClasses()
```


## getForm

Returns the form object to which this page belongs.

### Syntax
```javascript
page.getForm()
```


## getId

Returns the unique ID, within the application, of this page. For example, <b>P_Page1</b>.

### Syntax
```javascript
page.getId()
appPage.getId()
```


## getServiceConfigurationIds

Returns an array of all the IDs for services mapped in this app page.

### Syntax
```javascript
appPage.getServiceConfigurationIds()
```

### Example

```javascript
var serviceConfigs = appPage.getServiceConfigurationIds();
```


## getServiceConfiguration

Gets the service object for a particular service ID.

### Syntax
```javascript
appPage.getServiceConfiguration (serviceId)
```

### Example

Lookup and execute a service from JavaScript™:
```javascript
var service = appPage.getServiceConfiguration('SC_ServiceConfig');
service.callService();
```

## getType

Returns a string identifying the object type. For example, "page".

### Syntax
```javascript
page.getType()
appPage.getType()
```


## getVisibility

Returns true if the page is being shown, and false if it is hidden.

### Syntax
```javascript
page.getVisibility()
```


## removeClasses

Removes a list of custom class names from the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.

### Syntax
```javascript
page.removeClasses(classes)
appPage.removeClasses(classes)
```

## Example

```javascript
page.removeClasses('emphasized error');
```

**Parent topic:** [Interface objects](ref_jsapi_user_interface_objects.md)

