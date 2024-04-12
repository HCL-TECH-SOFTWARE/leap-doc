# Page and App Page objects 

<table class="table-wrap">
<thead>
<tr>
<th width="250">Object</th><th>Description</th><th>Example</th>
</tr>
<thead>
<tbody>
<tr>
<td> 
page.&lt;itemId&gt;<br>
appPage.&lt;itemId&gt;</td>
<td>Provides convenient direct access to all items on the page, including those inside Sections and Tab Folders.</td>

<td> Hide a specific button on the page:

```javascript
page.F_NextButton.setVisible(false);
```
</td>
</tr>
<tr>
<td>page.addClasses(classes)</br>
appPage.addClasses(classes)</td>
<td>Adds a list of custom class names to the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.</td>
<td>

```javascript
page.addClasses('emphasized error');
```
</td>
</tr>
<tr>
<td>page.connectEvent(eventName,<br>
callbackFunction)<br>
appPage.connectEvent(eventName,<br>
callbackFunction)</td>
<td>Connects a function to an event on the page. The list of events is the same as for the page in the Design interface. Useful for utility functions defined in JavaScript™ files to hook behavior into the page dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using page.disconnectEvent or appPage.disconnectEvent.</td>
<td> </td>
</tr>
<tr>
<td>page.disconnectEvent(eventHandle)<br>
appPage.disconnectEvent (eventHandle)</td>
<td>Disconnects the event handler specified by the passed-in event handle object that was returned by a page.connectEvent or <b>appPage.connectEvent</b> call. To avoid duplicate event handlers being connected to pages, connect to page events from within the application <b>onStart</b> or form <b>onLoad</b> events. If you connect to a page event outside of these two events you should explicitly disconnect from the page event using the <b>disconnectEvent</b> method.</td>
<td>

```javascript 
var eventHdl = page.connectEvent("<some event>", function(pSuccess, pErrorObj)
 {
  if (pSuccess) {
    //do something when service is done
  }
  page.disconnectEvent(eventHndl);
});
```
</td>
</tr>
<tr>
<td>page.getBO()</td>
<td>Returns the object that contains the Business Object data for the entire form.</td>
<td>

```javascript
var theBO = page.getBO();
theBO.F_SingleLine.setValue('new Value');
```
</td>
</tr>
<td>page.getChildren()</br>
appPage.getChildren()</td>
<td>Returns the list object that provides access to all direct children items for this page. For example, items in a Section on the page are not in the list, however the Section itself is. The list object has the getLength() function and get(index) function for accessing the objects in the list.</td>
<td>Hide all button items on a page:

```javascript
var list = page.getChildren();
for (var i=0; i<list.getLength(); i++) {
   if list.get(i).getType() === 'button') {
      list.get(i).setVisible(false);
   }
}
```
</td>
</tr>

<tr>
<td>
page.getClasses()<br>
appPage.getClasses()
</td>
<td>Returns an Array of custom class names currently applied to the page.</td>
<td><!-- no example --></td>
</tr>

<tr>
<td>page.getForm()</td>
<td>Returns the form object to which this page belongs.</td>
<td><!-- no example --></td>
</tr>

<tr>
<td>page.getId()<br>
appPage.getId()</td>
<td>Returns the unique ID, within the application, of this page. For example, <b>P_Page1</b>.</td>
<td><!-- no example --></td>
</tr>

<tr>
<td>appPage.getServiceConfigurationIds()</td>
<td>Returns an array of all the IDs for services mapped in this app page.</td>
<td>

```javascript
var serviceConfigs = appPage.getServiceConfigurationIds();
```
</td>
</tr>

<tr>
<td>appPage.getServiceConfiguration (serviceId)</td>
<td>Gets the service object for a particular service ID.</td>
<td>Lookup and execute a service from JavaScript™:

```javascript
var service = appPage.getServiceConfiguration('SC_ServiceConfig');
service.callService();
```
</td>
</tr>

<tr>
<td>page.getType()<br>
appPage.getType()</td>
<td>Returns a string identifying the object type. For example, "page".</td>
<td><!-- no example --></td>
</tr>

<tr>
<td>page.getVisibility()</td>
<td>Returns true if the page is being shown, and false if it is hidden.</td>
<td><!-- no example --></td>
</tr>

<tr>
<td>page.removeClasses(classes)<br>
appPage.removeClasses(classes)</td>
<td>Removes a list of custom class names from the page for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.</td>
<td>

```javascript
page.removeClasses('emphasized error');
```
</td>
</tr>
</tbody>
</table>


**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)

