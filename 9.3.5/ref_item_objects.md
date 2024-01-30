# Item objects {#ref_item_objects .concept}

**Note:** The item.setTitle parameter is not applicable to Tabbed Folder form items.

|Object|Description|Example|
|------|-----------|-------|
|item.addClasses\(classes\)apItem.addClasses\(classes\)

|Adds a list of custom class names to an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.|```
item.addClasses("emphasized error");
```

|
|item.clearRequiredMessage\(\)apItem.clearRequiredMessage\(\)

|Validates the item data, but prevents the required error message from displaying.| |
|item.connectEvent\(eventName,callbackFunction\)apItem.connectEvent\(eventName,callbackFunction\)

|Connects a function to an event on the item. Useful for utility functions defined in external JavaScript™ files to hook behavior into the item dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using item.disconnectEvent.|Connect a listener to the **onItemChange** event to make a section visible. This could be placed in the form **onLoad** event:  ```
var hndl = item.connectEvent('onItemChange', function()
     {
     if(item.getBOAttr().getValue() === 'Yes')
form.getBO().F_SectionA.setVisible(true);
     }
     });
```

|
|item.disconnectEvent\(eventHandle\)apItem.disconnectEvent\(eventHandle\)

|Disconnects the event handler specified by the passed-in event handle object that was returned by an item.connectEvent call.If you connect an item event, you must also disconnect it in the same event. Otherwise, multiple versions of the connected code are attached every time the event is triggered.

|If the connect event is placed in the item **onShow** then the listener needs to be disconnected: ```
var hndl = item.connectEvent('onItemChange', function()
{
   if(item.getBOAttr().getValue() === 'Yes')
     form.getBO().F_SectionA.setVisible(true);
   }
   item.disconnectEvent(hndl);
});
```

|
|item.getActive\(\)apItem.getActive\(\)

|Returns true if this item is active, or false if it is made read only by a rule, stage, or JavaScript.| |
|apItem.getAppPage\(\)|Returns the page object to which this item belongs.| |
|item.getBO\(\)|Returns the Business Object for the entire form.| |
|item.getBOAttr\(\)|An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.|Get data for an item and set its value:```
item.getBOAttr().setValue(45);
```

|
|item.getChildren\(\)|If this item contains children, for example Section, or Tab Folder, it returns a list object that provides access to all direct children items. The list object has the getLength\(\) function and get\(index\) function for accessing the objects in the list.|Rest all numbers inside a section to 0:```
var list = item.getChildren();
     for(var i=0; i<list.getLength(); i++)
     {
     if(list.get(i).getType() === 'number')
     list.get(i).getBOAttr().setValue(0);
     }
```

|
|item.getClasses\(\)apItem.getClasses\(\)

|Returns an Array of custom class names currently applied to an item.| |
|item.getDisplayValue\(\)apItem.getDisplayValue\(\)

|Returns the current value that is being displayed. It can be used in onItemLiveChange to get current, but not yet committed value.| |
|item.getHoverText\(\)apItem.getHoverText\(\)

|Returns the current value set as hover text.| |
|item.getHintText\(\)apItem.getHintText\(\)

|Returns the value set as **Hint** text.| |
|item.getId\(\)apItem.getId\(\)

|Returns the unique ID, within the application, of this item. For example, F\_FirstName.| |
|apItem.getInvalidMessage\(\)|An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.| |
|item.getPage\(\)|Returns the page object to which this item belongs.|Get the form object:```
var form = item.getPage().getForm();
```

|
|item.getParent\(\)apItem.getParent\(\)

|Returns the object that is the direct parent of the item, which can be a page, section, or tab folder.| |
|item.getPlaceholderText\(\)apItem.getPlaceholderText\(\)

|Returns the current value set as place holder text.| |
|apItem.getRequired\(\)|Gets a value set previously using setRequired\(\).| |
|item.getRows\(\)|Returns the current value set as the number of rows displayed. This method gets the number of rows the text area displayed.**Note:** This parameter works only on multi-line input areas.

| |
|item.getStartLabel\(\)|This method gets the value of the label displayed at the start of a numeric or choice slider.| |
|item.getStopLabel\(\)|This method gets the value of the label displayed at the end of a numeric or choice slider.| |
|item.getStyle\(\)|Returns the current value set for display style. **Note:** This parameter works only on **Date** and **Time** input fields.

| |
|item.getTitle\(\)apItem.getTitle\(\)

|Returns the current value used as the field title.| |
|item.getType\(\)apItem.getType\(\)

|Returns a string identifying the object type.||Palette item|Type|Palette item|Type|
|------------|----|------------|----|
|Attachment|attachment|Paragraph Text|textArea|
|Button|button|Password|password|
|Check Box|checkBox|Section|section|
|Currency|currency|Select Many|checkGroup|
|Date|date|Select One|radioGroup|
|Dropdown|comboBox|Single Line|text|
|Email Address|emailAddress|Survey|survey|
|Folder Tab|tabFolderTab|Survey Question|surveyQuestion|
|HTML Fragment|htmlArea|Tabbed folder|tabFolder|
|Image|image|Table|aggregationListContainer|
|Line|horizontalLine|Text|richText|
|Media|media|Time|time|
|Number|number|Timestamp|timeStamp|
|Numeric Slider|horizontalSlider|Web Link|staticWebLink|
|Page|page|Website|weblink|
|Page Navigation|pageNavigator|Name Picker|name|
|Rich text|richTextArea|Data Grid|dataGrid|

|
|apItem.getValid\(\)|Gets a value set previously using setValid\(\).| |
|item.getValue\(\)apItem.getValue\(\)

|Returns the current value. Its type depends on the data type.

 For example, **String** \[check and radio list objects return a delimited list with \_\#\_ as the delimiter\], **Number** \[number, currency\], **Boolean**, **Date** \[date, timestamp, time\], or **Object** \[attachment\].

| |
|item.getVisible\(\)apItem.getVisible\(\)

|Returns true if this item is visible \(does not take into account which page is being shown\) or false if it is hidden by a rule, stage, or JavaScript, or if its parent is hidden.| |
|apItem.isMissing\(\)|Returns true if this item is required and it has no value.| |
|apItem.isRequired\(\)|Returns true if the item is required, otherwise false.| |
|apItem.isValid\(\)|Returns true if the data is valid. Returns false if the data is invalid.| |
|item.removeClasses\(classes\)apItem.removeClasses\(classes\)

|Removes a list of custom class names from an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.|```
item.removeClasses("emphasized");
```

|
|item.setActive\(active\)apItem.setActive\(active\)

|Sets whether this item is inactive, or read only. **Note:** If this item is made inactive by a rule or stage, then you cannot make it active with JavaScript.

| |
|item.setDisplayValue\(pValue\)apItem.setDisplayValue\(pValue\)

|Takes a string or number in pValue. This method sets the value being displayed. If the user is editing, then it will update the value they are trying to enter. If the user is not editing, then it will be the same as setValue\(\). This method works on direct input items such as single line, multi line, number, currency, email and website.| |
|item.setFocus\(\)apItem.setFocus\(\)

|Causes this item to receive focus. This option has no effect on items that cannot have focus, are invisible, or are read-only.| |
|item.setHintText\(pValue\)apItem.setHintText\(pValue\)

|Takes a pValue string. This method sets the text that is used for hover text on input items. If an empty value is provided, the hint text area is removed.| |
|item.setHoverText\(pValue\)apItem.setHoverText\(pValue\)

|Takes a pValue string. This method sets the text that is used for **Hint** text on input items. If an empty value is provided, no hover help is displayed.| |
|apItem.setRequired\(required\)|You can override non-required data to be required with this method. Passing true causes its data to be required and prevents submission if it is not set. Setting the valid to false clears any previously overridden value.| |
|item.setRows\(pValue\)|Takes a pValue number. This method sets the number of rows the text area displays.**Note:** Whenever possible, do not exceed 40 rows.

| |
|item.setPlaceholderText\(pValue\)apItem.setPlaceholderText\(pValue\)

|Takes a pValue string. This method sets the text used as placeholder text on input items.| |
|item.setStartLabel\(pValue\)|Takes a pValue string. This method sets the value of the label displayed at the start of a numeric or choice slider.| |
|item.setStopLabel\(pValue\)|Takes a pValue string. This method sets the value of the label displayed at the end of a numeric or choice slider.| |
|item.setStyle\(pValue\)|Takes a pValue string. This method sets the style used to display time and dates. Valid values are numeric, short, medium, long, and full. Valid values for time are numeric, short and medium.| |
|item.setTitle\(pValue\)apItem.setTitle\(pValue\)

|Takes a pValue string. This method sets the text used for a field titles on input items. If an empty value is provided, the title is removed.| |
|apItem.setValid\(valid, msg\)|You can override valid data to be invalid with this method. Passing false causes the data to be invalid, and prevents submission. You can optionally provide a custom error message. Setting the valid to true clears any previously overridden valid value.| |
|item.setValue\(pValue\)apItem.setValue\(pValue\)

|Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String.

**Note:** The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.

| |
|item.setVisible\(visible\)apItem.setVisible\(visible\)

|Sets whether this item is visible. **Note:** If this item is made invisible by a rule or stage, or because a parent is hidden, then you cannot unhide it by calling this function.

| |
|apItem.validate\(\)|Triggers the validation of the data item.| |
|item.getColumnHeaders\(\)

|Returns a JSON object that contains the id, title and width of each header displayed for the table.

 Sample JSON output:

```
[{id:"F_Currency1",title:"La Currency",width:20},
{id:"F_Date1",title:"La Date"}]
```

|```
var headers =  page.F_Table1.getColumnHeaders();
for(var h in headers) {
  alert("ID=" + get(headers,h).id +
  ", title=" + get(headers,h).title + 
  ", width=" + get(headers,h).width);
}
```

|
|item.setColumnHeaders\(headers\)

|Function accepts a JSON object that can be used to set the id, title and width of each column in the table.

 This is helpful, for example, to change the language of the column header displayed.

|``` {#codeblock_hpl_rqh_hwb}
var headers = new Array(); 
set(headers, 0, {id: "F_Currency1", title: "La Currency", width: 20}); 
set(headers, 1, {id: "F_Date1", title: "La Date"}); 
page.F_Table1.setColumnHeaders(headers); 
```

|

|Object|Description|Example|
|------|-----------|-------|
|item.getOptions\(\)|Returns the array of options currently shown in the drop-down. Each object in the array has a “title” property that is shown in the interface, and a “value” property that is saved into the data.|Get the title of a specific dropdown value:```
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

|
|item.setOptions\(options\)|Changes the list of options to show in the drop-down. It must be an array of objects. Each object must have a “title” property that is shown in the interface, and a “value” property that is saved into the data.|Provide custom list for the drop-down:```
var options = new Array();
     options.push({title:'Banana',value:'BA'});
     options.push({title:'Apple',value:'AP'});
     options.push({title:'Orange',value:'OR'});
     item.setOptions(options);
```

|

|Object|Description|
|------|-----------|
|item.setDisplayValue\(display\)|Sets the display value that the user sees as the link in the browser.|
|item.setLinkValue\(link\)|Sets the URL to which the link navigates when this item is clicked.|

|Object|Description|
|------|-----------|
|item.getContent\(\)|Gets the currently shown content for this interface item.|
|item.setContent\(content\)|Shows content in this interface only item. The content is evaluated as HTML code.|

|Object|Description|
|------|-----------|
|item.setContent\(content\)|Shows content in this interface-only item. In Text, it is the raw text to show, no special formatting is supported.|

|Object|Description|
|------|-----------|
|item.setAlternativeText\(pText\)|Sets the alt text of the image assigned to the button.|
|item.setContent\(content\)|Sets the label that is shown on the button.|
|item.setDisabledImageUrl\(pUrl\)|Sets the background of the button to the image at the public URL when the button is disabled.|
|item.setImageHeight\(pHeight\)|Sets explicit height in pixels for the image.|
|item.setImageUrl\(pUrl\)|Sets the background of the button to the image at the public URL.|
|item.setImageWidth\(pWidth\)|Sets explicit width in pixels for the image.|
|item.setMouseDownImageUrl\(pUrl\)|Sets the background of the button to the image at the public URL when the mouse down event is triggered.|
|item.setMouseOverImageUrl\(pUrl\)|Sets the background of the button to the image at the public URL when the mouse over event is triggered.|

|Object|Description|
|------|-----------|
|item.getHeight\(\)|Returns the current image height. Can be zero or blank.|
|item.getURL\(\)|Gets the current URL shown by this image item.|
|item.getWidth\(\)|Returns the current image width. Can be zero or blank.|
|item.setHeight\(height\)|Sets explicit height in pixels for the image. Setting “0” removes the explicit height.|
|item.setURL\(newURL\)|Sets the URL shown by this image item.|
|item.setWidth\(width\)|Sets explicit width in pixels for the image. Setting “0” removes the explicit width.|

|Object|Description|
|------|-----------|
|item.getExpanded\(\)|Returns true if the section is expanded and false if it is collapsed.|
|item.setExpanded\(expanded\)|Sets the expanded state of the section. If true, the section is expanded. If false, then it is collapsed.|

|Object|Description|Example|
|------|-----------|-------|
|item.getSelectionIndex\(\)|Returns the index of the currently selected tab.|Set 12 into the first item in the currently shown tab:```
var sel = item.getSelectionIndex();
     var tabs = item.getChildren();
     var selTab = tabs.get(sel);
     var tabChildren = selTab.getChildren();
     tabChildren.get(0).getBOAttr().setValue(12);
```

|
|item.getTabTitleList\(\)|Returns an array of all the tab titles in this folder.| |
|item.setSelectedTab\(tabTitle\)|Takes a tabTable string. Selects the Tab that matches the tabTable string.| |
|item.setTabTitle\(tabIndex,pTitle\)|Updates the title of a tab within a **Tabbed Folder** by using a **tabIndex** integer and **pTitle** string value. **tabIndex** denotes the location of the tab within the list of available tabs from left-to-right. For bidirectional languages, the order is right-to-left.|On the form, a Tabbed folder contains 5 tabs: Red, Orange, Yellow, Green, Blue. The default start number of the **tabIndex** is 0.

 In our example tabbed folder, the **tabIndex** number 0 is the Red tab which is furthest left, while 4 is the tab furthest to the right.

 In a bidirectional language, the order is reversed. Tab 0 is assigned to Blue, which is the tab furthest to the right.

|
|item.setTabTitleList\(pTitleArray\)|Updates the titles of tabs within a **Tabbed Folder** from a list of strings by using a **pTitleArray** array of string values. The list of tabs is updated respective to the order of strings that are defined in the array. If there are more array values than tabs in the form, the additional values are ignored.|```
item.setTabTitleList(['Monday','Tuesday','Wednesday','Thursday','Friday']);
```

|

|Object|Description|Example|
|------|-----------|-------|
|item.getSelection\(\)|Returns the Business Object of the selected row or null if there is no selection.| |
|item.setSelection\(BO\)|Selects the last Business Object in the table.|Select that last row in the table:```
var lastIndex = item.getBOAttr().getLength()-1;
     var lastRow = item.getBOAttr().get(lastIndex);
     item.setSelection(lastRow);
```

|
|item.showAdd\(show\)|If show is true, then the **Add** button is made visible.If false, then the **Add** button is hidden.

| |
|item.showEdit\(show\)|If show is true, then the **Edit** button is made visible. If false, then the **Edit** button is hidden.

| |
|item.showRemove\(show\)|If show is true, then the **Remove** button is made visible. If false, then the **Remove** button is hidden.

| |

|Object|Description|
|------|-----------|
|item.getOptions\(\)|Returns an array of all the options for the survey questions. Each option has a value property, that gets saved in the data, and a display property, the title of at the beginning of the survey.|

|Object|Description|Example|
|------|-----------|-------|
|item.getDisplayedData\(\)|-   Boolean: Checkbox
-   Number : Number, Currency, Numeric Slider
-   Date: Date, Time, Timestamp
-   Object: Attachment
    -   `uid`: The identifier of the attachment.
    -   `filename`: the file name of the attachment.
    -   `viewUrl`: The url to view the attachment.
    -   `downloadUrl`: The url to download the attachment.
-   Object: Name Picker
-   Object: Select Many
    -   `savedValues`: An array of all the saved values.
    -   `displayValues`: An array of all the display values.
    -   `displayString`: All the list values provided as a comma-separated string.
-   String: All other items

|Render all the row data displayed in the data grid as JSON:

 ``` {#codeblock_fzz_2dq_5qb}
appPage.F_Text2.setContent(toJson(appPage.F_DataGrid1.getDisplayedData(), true));
```

 Calculate the sum of a column from displayed data:

``` {#codeblock_znv_gdq_5qb}
var data = appPage.F_DataGrid1.getDisplayedData();
  var sum = 0;
  for(var d in data) {
    var dObj = get(data, d);
    sum += dObj.F_Number1;
  }
  alert("Sum = " + sum);

```

|
|item.isAllDataDisplayed\(\)|Returns true if all the submitted data for the form connected to the data grid is rendered on screen in a single page.|If all the known data is being displayed, then do something with that data. In this example the sum of a column is calculated:

``` {#codeblock_ebh_p3q_5qb}
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

|
|item.isColumnVisible\(columnId\)|Returns true if the specified column is visible in the data grid.|``` {#codeblock_zyh_s3q_5qb}
appPage.F_DataGrid1.isColumnVisble(“F_SingleLine1”);
```

|
|item.refresh\(\)|Forces the data grid to reload. For example, a submission with “apps as a service” may have been triggered and the content in the data grid is stale.|Refresh the data grid after calling a service that changes \(i.e. adds to, removes from, or updates\) the data to which the data grid is connected:

 ``` {#codeblock_csc_x3q_5qb}
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

|
|item.selectFirstRow\(\)|Selects the first row in the data grid.| |
|item.setColumnHeader\(columnId, pHeaderValue\)|Sets the header identified by columnId, to the value provided in pHeaderValue.|See above for columnId values.

 Set the header of a column to another language:

 ``` {#codeblock_rt3_djq_5qb}
appPage.F_DataGrid1.setColumnHeader("createdBy",
 "Créé par");
```

|
|item.setColumnVisible\(columnId, boolVal\)|Controls the visibility of the column identified by columnId. If boolVal is true, the column is shown. If boolVal is false, the column is hidden.|See above for columnId values.

 Hide a column from the data grid if user is not part of a specific role:

 ``` {#codeblock_dz3_3jq_5qb}
var isAdmin = app.getCurrentUserRoles().contains("Administrator");
item.setColumnVisible("F_AdminOnly1", isAdmin);
```

|
|item.resetFilters\(\)|Returns the filters to what was specified in the data grid configuration.| |
|item.setFilters\(\[filter\], filterOp\)|Set filters for the data grid, this will override any filters specified in the data grid configuration. \[filter\] is an array of filter objects. filterOp is either “and” or “or” and is required if there is more than one filter. A filter is made up of the following:

-   name: the id of a meta-data attribute or a field of the form configured to the data grid.

**Note:** The field id does not have to be displayed in the data grid.

-   operator: as documented in [Filtering Data REST API results](ref_data_rest_api_list_filter.md).
-   value: the value to search

|Set a filter to show records that are older than one week and in the “ST\_Triage” stage:

 ``` {#codeblock_ls3_yjq_5qb}
var now = new Date(); 
var aWeekAgo = new Date (now.getTime() - (7*24*60*60*1000)); 
var filters = [ 
    {name : "created", operator: "before", value: aWeekAgo}, 
    {name: "stageId", operator: "equals", value: "ST_Triage"}   
]; 
page.F_DataGrid1.setFilters(filters, "and"); 

```

 Set a filter to show records between two dates, from fields on the same app page as the data grid:

``` {#codeblock_kp5_5ls_lsb}
var filters = [
    {name: "F_BirthDate", operator: "between", value: [appPage.F_StartDate.getValue(), appPage.F_EndDate.getValue()]}
];

appPage.F_DataGrid2.setFilters(filters, "and");
```

 Remove all filters:

 ``` {#codeblock_nyv_zjq_5qb}
appPage.F_DataGrid1.setFilters(null);
```

|

**Parent topic:**[Interface objects](ref_jsapi_user_interface_objects.md)

