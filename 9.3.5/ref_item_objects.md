# Item objects {#ref_item_objects .concept}

<b>Note:</b> The item.setTitle parameter is not applicable to Tabbed Folder form items.

Table 1. Item (item) and App Page Item (apItem) Objects<br>
The item object represents a particular item on a page, and provides access to its properties. For Sections and Tab Folders, access to their child items is also granted.

<table class="table-wrap">
<thead>
<th width="250">Object
<th>Description
</thead>

<tr>
<td>item.addClasses(classes)<br>
apItem.addClasses(classes)
<td>Adds a list of custom class names to an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.<br>
<br>
Example:
```javascript
item.addClasses("emphasized error");
```

<tr>
<td>item.clearRequiredMessage()apItem.clearRequiredMessage()
<td>Validates the item data, but prevents the required error message from displaying.

<tr>
<td>item.connectEvent (eventName, callbackFunction)<br>
apItem.connectEvent (eventName, callbackFunction)
<td>Connects a function to an event on the item. Useful for utility functions defined in external JavaScript™ files to hook behavior into the item dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using item.disconnectEvent.<br>
<br>
Example:<br>
Connect a listener to the <b>onItemChange</b> event to make a section visible. This could be placed in the form <b>onLoad</b> event:  
```javascript
var hndl = item.connectEvent('onItemChange', function() {
   if(item.getBOAttr().getValue() === 'Yes')
      form.getBO().F_SectionA.setVisible(true);
}});
```

<tr>
<td>item.disconnectEvent (eventHandle)<br>
apItem.disconnectEvent (eventHandle)
<td>Disconnects the event handler specified by the passed-in event handle object that was returned by an item.connectEvent call.If you connect an item event, you must also disconnect it in the same event. Otherwise, multiple versions of the connected code are attached every time the event is triggered.<br>
<br>
Example:<br>
If the connect event is placed in the item <b>onShow</b> then the listener needs to be disconnected: 
```javascript
var hndl = item.connectEvent('onItemChange', function()
{
   if(item.getBOAttr().getValue() === 'Yes')
     form.getBO().F_SectionA.setVisible(true);
   }
   item.disconnectEvent(hndl);
});
```

<tr>
<td>item.getActive()<br>
apItem.getActive()
<td>Returns true if this item is active, or false if it is made read only by a rule, stage, or JavaScript.

<tr>
<td>apItem.getAppPage()
<td>Returns the page object to which this item belongs.

<tr>
<td>item.getBO()
<td>Returns the Business Object for the entire form.

<tr>
<td>item.getBOAttr()
<td>An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.<br>
<br>
Example:<br>
Get data element for an item and set its value:
```javascript
item.getBOAttr().setValue(45);
```

<tr>
<td>item.getChildren()
<td>If this item contains children, for example Section, or Tab Folder, it returns a list object that provides access to all direct children items. The list object has the getLength() function and get(index) function for accessing the objects in the list.<br>
<br>
Example:<br>
Reset all numbers inside a section to 0:
```javascript
var list = item.getChildren();
for(var i=0; i<list.getLength(); i++)
{
   if(list.get(i).getType() === 'number')
      list.get(i).getBOAttr().setValue(0);
}
```

<tr>
<td>item.getClasses()<br>
apItem.getClasses()
<td>Returns an Array of custom class names currently applied to an item.

<tr>
<td>item.getDisplayValue()<br>
apItem.getDisplayValue()
<td>Returns the current value that is being displayed. It can be used in onItemLiveChange to get current, but not yet committed value.

<tr>
<td>item.getHoverText()<br>
apItem.getHoverText()
<td>Returns the current value set as hover text.

<tr>
<td>item.getHintText()<br>
apItem.getHintText()
<td>Returns the value set as <b>Hint</b> text.

<tr>
<td>item.getId()<br>
apItem.getId()
<td>Returns the unique ID, within the application, of this item. For example, F_FirstName.

<tr>
<td>apItem.getInvalidMessage()
<td>An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.

<tr>
<td>item.getPage()
<td>Returns the page object to which this item belongs.<br>
<br>
Example:<br>
Get the form object:
```javascript
var form = item.getPage().getForm();
```

<tr>
<td>item.getParent()<br>
apItem.getParent()
<td>Returns the object that is the direct parent of the item, which can be a page, section, or tab folder.

<tr>
<td>item.getPlaceholderText()apItem.getPlaceholderText()
<td>Returns the current value set as place holder text.

<tr>
<td>apItem.getRequired()
<td>Gets a value set previously using setRequired().

<tr>
<td>item.getRows()
<td>Returns the current value set as the number of rows displayed. This method gets the number of rows the text area displayed.<br>
<br>
<b>Note:</b> This parameter works only on multi-line input areas.

<tr>
<td>item.getStartLabel()
<td>This method gets the value of the label displayed at the start of a numeric or choice slider.

<tr>
<td>item.getStopLabel()
<td>This method gets the value of the label displayed at the end of a numeric or choice slider.

<tr>
<td>item.getStyle()
<td>Returns the current value set for display style.<br>
<br>
<b>Note:</b> This parameter works only on <b>Date</b> and <b>Time</b> input fields.

<tr>
<td>item.getTitle()<br>
apItem.getTitle()
<td>Returns the current value used as the field title.

<tr>
<td>item.getType()<br>
apItem.getType()
<td>Returns a string identifying the object type.
<table>
<thead>
<th>Palette item<th>Type<th>Palette item<th>Type
</thead>
<tr>
  <td>Attachment<td>attachment<td>Paragraph Text<td>textArea
<tr>
  <td>Button<td>button<td>Password<td>password
<tr>
  <td>Check Box<td>checkBox<td>Section<td>section
<tr>
  <td>Currency<td>currency<td>Select Many<td>checkGroup
<tr>
  <td>Date<td>date<td>Select One<td>radioGroup
<tr>
  <td>Dropdown<td>comboBox<td>Single Line<td>text
<tr>
  <td>Email Address<td>emailAddress<td>Survey<td>survey
<tr>
  <td>Folder Tab<td>tabFolderTab<td>Survey Question<td>surveyQuestion
<tr>
  <td>HTML Fragment<td>htmlArea<td>Tabbed folder<td>tabFolder
<tr>
  <td>Image<td>image<td>Table<td>aggregationListContainer
<tr>
  <td>Line<td>horizontalLine<td>Text<td>richText
<tr>
  <td>Media<td>media<td>Time<td>time
<tr>
  <td>Number<td>number<td>Timestamp<td>timeStamp
<tr>
  <td>Numeric Slider<td>horizontalSlider<td>Web Link<td>staticWebLink
<tr>
  <td>Page<td>page<td>Website<td>weblink
<tr>
  <td>Page Navigation<td>pageNavigator<td>Name Picker<td>name
<tr>
  <td>Rich text<td>richTextArea<td>Data Grid<td>dataGrid
</table>

<tr>
<td>apItem.getValid()
<td>Gets a value set previously using setValid().

<tr>
<td>item.getValue()<br>
apItem.getValue()
<td>Returns the current value. Its type depends on the data type.<br>
<br>
For example, <b>String</b> [multi-value fields return a delimited list with __#__ as the delimiter], <b>Number</b> [number, currency], <b>Boolean</b>, <b>Date</b> [date, timestamp, time], or <b>Object</b> [attachment].

<tr>
<td>item.getVisible()<br>
apItem.getVisible()
<td>Returns true if this item is visible (does not take into account which page is being shown) or false if it is hidden by a rule, stage, or JavaScript, or if its parent is hidden.

<tr>
<td>apItem.isMissing()
<td>Returns true if this item is required and it has no value.

<tr>
<td>apItem.isRequired()
<td>Returns true if the item is required, otherwise false.

<tr>
<td>apItem.isValid()
<td>Returns true if the data is valid. Returns false if the data is invalid.

<tr>
<td>item.removeClasses(classes)<br>
apItem.removeClasses(classes)
<td>Removes a list of custom class names from an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.<br>
<br>
Example:<br>
```javascript
item.removeClasses("emphasized");
```

<tr>
<td>item.setActive(active)<br>
apItem.setActive(active)
<td>Sets whether this item is inactive, or read only.<br>
<b>Note:</b> If this item is made inactive by a rule or stage, then you cannot make it active with JavaScript.

<tr>
<td>item.setDisplayValue(pValue)<br>
apItem.setDisplayValue(pValue)
<td>Takes a string or number in pValue. This method sets the value being displayed. If the user is editing, then it will update the value they are trying to enter. If the user is not editing, then it will be the same as setValue(). This method works on direct input items such as single line, multi line, number, currency, email and website.

<tr>
<td>item.setFocus()<br>
apItem.setFocus()
<td>Causes this item to receive focus. This option has no effect on items that cannot have focus, are invisible, or are read-only.

<tr>
<td>item.setHintText(pValue)<br>
apItem.setHintText(pValue)
<td>Takes a pValue string. This method sets the text that is used for hover text on input items. If an empty value is provided, the hint text area is removed.

<tr>
<td>item.setHoverText(pValue)<br>
apItem.setHoverText(pValue)
<td>Takes a pValue string. This method sets the text that is used for <b>Hint</b> text on input items. If an empty value is provided, no hover help is displayed.

<tr>
<td>apItem.setRequired(required)
<td>You can override non-required data to be required with this method. Passing true causes its data to be required and prevents submission if it is not set. Setting the valid to false clears any previously overridden value.

<tr>
<td>item.setRows(pValue)
<td>Takes a pValue number. This method sets the number of rows the text area displays.<br>
<b>Note:</b> Whenever possible, do not exceed 40 rows.

<tr>
<td>item.setPlaceholderText(pValue)<br>
apItem.setPlaceholderText(pValue)
<td>Takes a pValue string. This method sets the text used as placeholder text on input items.

<tr>
<td>item.setStartLabel(pValue)
<td>Takes a pValue string. This method sets the value of the label displayed at the start of a numeric or choice slider.

<tr>
<td>item.setStopLabel(pValue)
<td>Takes a pValue string. This method sets the value of the label displayed at the end of a numeric or choice slider.

<tr>
<td>item.setStyle(pValue)
<td>Takes a pValue string. This method sets the style used to display time and dates. Valid values are numeric, short, medium, long, and full. Valid values for time are numeric, short and medium.

<tr>
<td>item.setTitle(pValue)<br>
apItem.setTitle(pValue)
<td>Takes a pValue string. This method sets the text used for a field titles on input items. If an empty value is provided, the title is removed.

<tr>
<td>apItem.setValid(valid, msg)
<td>You can override valid data to be invalid with this method. Passing false causes the data to be invalid, and prevents submission. You can optionally provide a custom error message. Setting the valid to true clears any previously overridden valid value.

<tr>
<td>item.setValue(pValue)<br>
apItem.setValue(pValue)
<td>Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String.<br>
<br>
<b>Note:</b> The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.

<tr>
<td>item.setVisible(visible)<br>
apItem.setVisible(visible)
<td>Sets whether this item is visible.<br><br>
<b>Note:</b> If this item is made invisible by a rule or stage, or because a parent is hidden, then you cannot unhide it by calling this function.

<tr>
<td>apItem.validate()
<td>Triggers the validation of the data item.

<tr>
<td>item.getColumnHeaders()
<td>Returns a JSON object that contains the id, title and width of each header displayed for the table.<br>
<br>
 Sample JSON output:<br>
```javascript
[
  {id:"F_Currency1",title:"La Currency",width:20},
  {id:"F_Date1",title:"La Date"}
]
```

```javascript
var headers =  page.F_Table1.getColumnHeaders();
for(var h in headers) {
  alert("ID=" + get(headers,h).id +
  ", title=" + get(headers,h).title + 
  ", width=" + get(headers,h).width);
}
```

<tr>
<td>item.setColumnHeaders(headers)
<td>Function accepts a JSON object that can be used to set the id, title and width of each column in the table.<br>
<br>
This is helpful, for example, to change the language of the column header displayed.  
```javascript 
var headers = new Array(); 
set(headers, 0, {id: "F_Currency1", title: "La Currency", width: 20}); 
set(headers, 1, {id: "F_Date1", title: "La Date"}); 
page.F_Table1.setColumnHeaders(headers); 
```

</table>
<br>
<br>
Table 2. Item Object - Drop Down only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>

<td>item.getOptions()
<td>Returns the array of options currently shown in the drop-down. Each object in the array has a "title" property that is shown in the interface, and a "value" property that is saved into the data.<br>
<br>
Example:<br>
Get the title of a specific dropdown value:
```javascript
var displayedValue = "";
var savedValue = BO.F_DropDown1.getValue();
var opts = page.F_DropDown1.getOptions();
for(var i=0; i<opts.length; i++) {
  var opt = get(opts, i);
  if(opt.value === savedValue) {
    displayedValue = opt.title;
    break;
  }
}
```

<tr>
<td>item.setOptions(options)
<td>Changes the list of options to show in the drop-down. It must be an array of objects. Each object must have a "title" property that is shown in the interface, and a "value" property that is saved into the data.<br>
<br>
Example:<br>
Provide custom list for the drop-down:
```javascript
var options = new Array();
     options.push({title:'Banana', value:'BA'});
     options.push({title:'Apple', value:'AP'});
     options.push({title:'Orange', value:'OR'});
     item.setOptions(options);
```
</table>
<br>
<br>
Table 3. Item Object - Weblink only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<tr>
<td>item.setDisplayValue(display)
<td>Sets the display value that the user sees as the link in the browser.

<tr>
<td>item.setLinkValue(link)
<td>Sets the URL to which the link navigates when this item is clicked.
</table>
<br>
<br>
Table 4. Item Object - HTML Fragment only
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>

<tr>
<td>item.getContent()
<td>Gets the currently shown content for this interface item.

<tr>
<td>item.setContent(content)
<td>Shows content in this interface only item. The content is evaluated as HTML code.
</table>
<br>
<br>
Table 5. Item Object - Text only
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<td>item.setContent(content)<td>
Shows content in this interface-only item. In Text, it is the raw text to show, no special formatting is supported.
</table>
<br>
<br>
Table 6. Item Object - Button only<br>
<table class="table-wrap">
<thead>
<th width="250">Object
<th>Description
</thead>
<td>item.setAlternativeText(pText)
<td>Sets the alt text of the image assigned to the button.

<tr>
<td>item.setContent(content)
<td>Sets the label that is shown on the button.

<tr>
<td>item.setDisabledImageUrl(pUrl)
<td>Sets the background of the button to the image at the public URL when the button is disabled.

<tr>
<td>item.setImageHeight(pHeight)
<td>Sets explicit height in pixels for the image.

<tr>
<td>item.setImageUrl(pUrl)
<td>Sets the background of the button to the image at the public URL.

<tr>
<td>item.setImageWidth(pWidth)
<td>Sets explicit width in pixels for the image.

<tr>
<td>item.setMouseDownImageUrl(pUrl)
<td>Sets the background of the button to the image at the public URL when the mouse down event is triggered.

<tr>
<td>item.setMouseOverImageUrl(pUrl)
<td>Sets the background of the button to the image at the public URL when the mouse over event is triggered.
</table>

<br>
<br>
Table 7. Item Object - Image only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<td>item.getHeight()
<td>Returns the current image height. Can be zero or blank.

<tr>
<td>item.getURL()
<td>Gets the current URL shown by this image item.

<tr>
<td>item.getWidth()
<td>Returns the current image width. Can be zero or blank.

<tr>
<td>item.setHeight(height)
<td>Sets explicit height in pixels for the image. Setting "0" removes the explicit height.

<tr>
<td>item.setURL(newURL)
<td>Sets the URL shown by this image item.

<tr>
<td>item.setWidth(width)
<td>Sets explicit width in pixels for the image. Setting "0" removes the explicit width.
</table>

<br>
<br>
Table 8. Item Object - Section only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<td>item.getExpanded()
<td>Returns true if the section is expanded and false if it is collapsed.

<tr>
<td>item.setExpanded(expanded)
<td>Sets the expanded state of the section. If true, the section is expanded. If false, then it is collapsed.
</table>

<br>
<br>
Table 9. Item Object - Tabbed Folder only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>

<td>item.getSelectionIndex()
<td>Returns the index of the currently selected tab.<br>
<br>
Example:<br>
Set 12 into the first item in the currently shown tab:
```javascript
var sel = item.getSelectionIndex();
var tabs = item.getChildren();
var selTab = tabs.get(sel);
var tabChildren = selTab.getChildren();
tabChildren.get(0).getBOAttr().setValue(12);
```

<tr>
<td>item.getTabTitleList()
<td>Returns an array of all the tab titles in this folder.

<tr>
<td>item.setSelectedTab(tabTitle)
<td>Selects the Tab that matches the tabTitle string.

<tr>
<td>item.setTabTitle(tabIndex, pTitle)
<td>Updates the title of a tab within a <b>Tabbed Folder</b> by using a <b>tabIndex</b> integer and <b>pTitle</b> string value. <b>tabIndex</b> denotes the location of the tab within the list of available tabs from left-to-right. For bidirectional languages, the order is right-to-left.<br>
<br>
Example:<br>
On the form, a Tabbed folder contains 5 tabs: Red, Orange, Yellow, Green, Blue. The default start number of the <b>tabIndex</b> is 0.<br>
<br>
In our example tabbed folder, the <b>tabIndex</b> number 0 is the Red tab which is furthest left, while 4 is the tab furthest to the right.<br>
<br>
In a bidirectional language, the order is reversed. Tab 0 is assigned to Blue, which is the tab furthest to the right.<br>

<tr>
<td>item.setTabTitleList (pTitleArray)
<td>Updates the titles of tabs within a <b>Tabbed Folder</b> from a list of strings by using a <b>pTitleArray</b> array of string values. The list of tabs is updated respective to the order of strings that are defined in the array. If there are more array values than tabs in the form, the additional values are ignored.<br>
<br>
Example:<br>
```javascript
item.setTabTitleList(['Monday','Tuesday','Wednesday','Thursday','Friday']);
```
</table>

<br>
<br>
Table 10. Item Object - Table only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<tr>
<td>item.getSelection()
<td>Returns the Business Object of the selected row or null if there is no selection.

<tr>
<td>item.setSelection(BO)
<td>Selects the last Business Object in the table.<br>
<br>
Example:<br>
Select that last row in the table:
```javascript
var lastIndex = item.getBOAttr().getLength()-1;
     var lastRow = item.getBOAttr().get(lastIndex);
     item.setSelection(lastRow);
```

<tr>
<td>item.showAdd(show)
<td>If show is true, then the <b>Add</b> button is made visible.If false, then the <b>Add</b> button is hidden.

<tr>
<td>item.showEdit(show)
<td>If show is true, then the <b>Edit</b> button is made visible. If false, then the <b>Edit</b> button is hidden.

<tr>
<td>item.showRemove(show)
<td>If show is true, then the <b>Remove</b> button is made visible. If false, then the <b>Remove</b> button is hidden.

</table>

<br>
<br>
Table 11. Item Object - Survey only
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<tr>
<td>item.getOptions()
<td>Returns an array of all the options for the survey questions. Each option has a value property, that gets saved in the data, and a display property, the title of at the beginning of the survey.
</table>

<br>
<br>
Table 12. Item Object - DataGrid only<br>
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>
<tr>
<td>item.getDisplayedData()
<td>
<ul>
  <li>Boolean: Checkbox</li>
  <li>Number : Number, Currency, Numeric Slider</li>
  <li>Date: Date, Time, Timestamp</li>
  <li>Object: Attachment</li>
    <ul>
      <li><code>uid</code>: The identifier of the attachment.</li>
      <li><code>filename</code>: the file name of the attachment.</li>
      <li><code>viewUrl</code>: The url to view the attachment.</li>
      <li><code>downloadUrl</code>: The url to download the attachment.</li>
    </ul>
  <li>Object: Name Picker</li>
  <li>Object: Select Many</li>
    <ul>
      <li><code>savedValues</code>: An array of all the saved values.</li>
      <li><code>displayValues</code>: An array of all the display values.
      <li><code>displayString</code>: All the list values provided as a comma-separated string.</li>
    </ul>
  <li>String: All other items</li>
</ul>
<br>
Examples:<br>
Render all the row data displayed in the data grid as JSON:
```javascript 
appPage.F_Text2.setContent(toJson(appPage.F_DataGrid1.getDisplayedData(), true));
```
<br>
Calculate the sum of a column from displayed data:
```javascript 
var data = appPage.F_DataGrid1.getDisplayedData();
var sum = 0;
for(var d in data) {
  var dObj = get(data, d);
  sum += dObj.F_Number1;
}
alert("Sum = " + sum);
```

<tr>
<td>item.isAllDataDisplayed()
<td>Returns true if all the submitted data for the form connected to the data grid is rendered on screen in a single page.<br>
<br>
Example:<br>
If all the known data is being displayed, then do something with that data. In this example the sum of a column is calculated:
```javascript 
if(appPage.F_DataGrid1.isAllDataDisplayed()) {
  var allData = appPage.F_DataGrid1.getDisplayedData();
  var sum = 0;
  for(var d in allData) {
    var dObj = get(allData, d);
    sum += dObj.F_Number1;
  }
  alert("Sum = " + sum);
}
```

<tr>
<td>item.isColumnVisible (columnId)
<td>Returns true if the specified column is visible in the data grid.<br>
<br>
Example:<br>
```javascript 
appPage.F_DataGrid1.isColumnVisble("F_SingleLine1");
```

<tr>
<td>item.refresh()
<td>Forces the data grid to reload. For example, a submission with "apps as a service" may have been triggered and the content in the data grid is stale.<br>
<br>
Example:<br>
Refresh the data grid after calling a service that changes (i.e. adds to, removes from, or updates) the data to which the data grid is connected:
```javascript 
var srv = form.getServiceConfiguration('SC_theService');
srv.connectEvent("onCallFinished", function(success)
{
  if(success) {
    try {
      appPage.F_DataGrid1.refresh();
    } catch (err) {
      alert("SC_theService: " + err);
    }
  }
});
```

<tr>
<td>item.selectFirstRow()
<td>Selects the first row in the data grid.

<tr>
<td>item.setColumnHeader (columnId, pHeaderValue)
<td>Sets the header identified by columnId, to the value provided in pHeaderValue.<br>
<br>
Example:<br>
See above for columnId values.<br>
<br>
Set the header of a column to another language:
```javascript 
appPage.F_DataGrid1.setColumnHeader("createdBy",
 "Créé par");
```

<tr>
<td>item.setColumnVisible(columnId, boolVal)
<td>Controls the visibility of the column identified by columnId. If boolVal is true, the column is shown. If boolVal is false, the column is hidden.<br>
<br>
Example:<br>
See above for columnId values.

Hide a column from the data grid if user is not part of a specific role:
```javascript 
var isAdmin = app.getCurrentUserRoles().contains("Administrator");
item.setColumnVisible("F_AdminOnly1", isAdmin);
```

<tr>
<td>item.resetFilters()
<td>Returns the filters to what was specified in the data grid configuration.

<tr>
<td>item.setFilters([filter], filterOp)
<td>Set filters for the data grid, this will override any filters specified in the data grid configuration.<br>
[filter] is an array of filter objects. <br>
filterOp is either "and" or "or" and is required if there is more than one filter.<br>
<br>
A filter is made up of the following:
<ul>
  <li>name: the id of a meta-data attribute or a field of the form configured to the data grid.<br>
  <b>Note:</b> The field id does not have to be displayed in the data grid.</li>
  <li>operator: as documented in <a href="ref_data_rest_api_list_filter.html">Filtering Data REST API results</a>.</li>
  <li>value: the value to search</li>
<br>
Examples:<br>
Set a filter to show records that are older than one week and in the "ST_Triage" stage:
```javascript 
var now = new Date(); 
var aWeekAgo = new Date (now.getTime() - (7*24*60*60*1000)); 
var filters = [ 
    {name : "created", operator: "before", value: aWeekAgo}, 
    {name: "stageId", operator: "equals", value: "ST_Triage"}   
]; 
page.F_DataGrid1.setFilters(filters, "and"); 

```
<br>
Set a filter to show records between two dates, from fields on the same app page as the data grid:
```javascript 
var filters = [
  {
    name: "F_BirthDate", 
    operator: "between", 
    value: [appPage.F_StartDate.getValue(), appPage.F_EndDate.getValue()]
  }
];
appPage.F_DataGrid2.setFilters(filters, "and");
```
<br>
Remove all filters:
```javascript 
appPage.F_DataGrid1.setFilters(null);
```

</table>

**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)
