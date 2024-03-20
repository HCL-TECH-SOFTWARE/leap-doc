# Item objects {#ref_item_objects .concept}

**Note:** The item.setTitle parameter is not applicable to Tabbed Folder form items.

Table 1. Item (item) and App Page Item (apItem) Objects

*The item object represents a particular item on a page, and provides access to its properties. For Sections and Tab Folders, access to their child items is also granted.*

|Object|Description|Example|
|------|-----------|-------|
|item.addClasses\(classes\) <br> apItem.addClasses\(classes\)|Adds a list of custom class names to an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.|```item.addClasses("emphasized error");```|
|item.clearRequiredMessage\(\) <br> apItem.clearRequiredMessage\(\)|Validates the item data, but prevents the required error message from displaying.| |
|item.connectEvent\(eventName,callbackFunction\) <br> apItem.connectEvent\(eventName,callbackFunction\)|Connects a function to an event on the item. Useful for utility functions defined in external JavaScript™ files to hook behavior into the item dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using item.disconnectEvent.|Connect a listener to the **onItemChange** event to make a section visible. This could be placed in the form **onLoad** event: <br> <code> var hndl = item.connectEvent('onItemChange', function() <br> { <br> if(item.getBOAttr().getValue() === 'Yes') <br> form.getBO().F_SectionA.setVisible(true); <br> } <br> }); </code>|
|item.disconnectEvent\(eventHandle\) <br> apItem.disconnectEvent\(eventHandle\)|Disconnects the event handler specified by the passed-in event handle object that was returned by an item.connectEvent call. <br><br> If you connect an item event, you must also disconnect it in the same event. Otherwise, multiple versions of the connected code are attached every time the event is triggered.|If the connect event is placed in the item **onShow** then the listener needs to be disconnected: <br> <code>var hndl = item.connectEvent('onItemChange', function() <br> { <br> if(item.getBOAttr().getValue() === 'Yes') <br> form.getBO().F_SectionA.setVisible(true); <br> } <br> item.disconnectEvent(hndl); <br> });|
|item.getActive\(\) <br> apItem.getActive\(\)|Returns true if this item is active, or false if it is made read only by a rule, stage, or JavaScript.| |
|apItem.getAppPage\(\)|Returns the page object to which this item belongs.| |
|item.getBO\(\)|Returns the Business Object for the entire form.| |
|item.getBOAttr\(\)|An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.|Get data for an item and set its value: <br> `item.getBOAttr().setValue(45);`|
|item.getChildren\(\)|If this item contains children, for example Section, or Tab Folder, it returns a list object that provides access to all direct children items. The list object has the getLength\(\) function and get\(index\) function for accessing the objects in the list.|Rest all numbers inside a section to 0: <br> <code>var list = item.getChildren(); <br> for(var i=0; i<list.getLength(); i++) <br> { <br> if(list.get(i).getType() === 'number') <br> list.get(i).getBOAttr().setValue(0); <br> }</code>|
|item.getClasses\(\) <br> apItem.getClasses\(\)|Returns an Array of custom class names currently applied to an item.| |
|item.getDisplayValue\(\) <br> apItem.getDisplayValue\(\)|Returns the current value that is being displayed. It can be used in onItemLiveChange to get current, but not yet committed value.| |
|item.getHoverText\(\) <br> apItem.getHoverText\(\)|Returns the current value set as hover text.| |
|item.getHintText\(\) <br> apItem.getHintText\(\)|Returns the value set as **Hint** text.| |
|item.getId\(\) <br> apItem.getId\(\)|Returns the unique ID, within the application, of this item. For example, F\_FirstName.| |
|apItem.getInvalidMessage\(\)|An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.| |
|item.getPage\(\)|Returns the page object to which this item belongs.|Get the form object: <br> ```var form = item.getPage().getForm();```|
|item.getParent\(\) <br> apItem.getParent\(\)|Returns the object that is the direct parent of the item, which can be a page, section, or tab folder.| |
|item.getPlaceholderText\(\) <br> apItem.getPlaceholderText\(\)|Returns the current value set as place holder text.| |
|apItem.getRequired\(\)|Gets a value set previously using setRequired\(\).| |
|item.getRows\(\)|Returns the current value set as the number of rows displayed. This method gets the number of rows the text area displayed. <br><br> **Note:** This parameter works only on multi-line input areas.| |
|item.getStartLabel\(\)|This method gets the value of the label displayed at the start of a numeric or choice slider.| |
|item.getStopLabel\(\)|This method gets the value of the label displayed at the end of a numeric or choice slider.| |
|item.getStyle\(\)|Returns the current value set for display style. <br><br> **Note:** This parameter works only on **Date** and **Time** input fields.| |
|item.getTitle\(\) <br> apItem.getTitle\(\)|Returns the current value used as the field title.| |
|item.getType\(\) <br> apItem.getType\(\)|Returns a string identifying the object type.|See Table 2|
|apItem.getValid\(\)|Gets a value set previously using setValid\(\).| |
|item.getValue\(\) <br> apItem.getValue\(\)|Returns the current value. Its type depends on the data type. <br> For example, **String** \[check and radio list objects return a delimited list with \_\#\_ as the delimiter\], **Number** \[number, currency\], **Boolean**, **Date** \[date, timestamp, time\], or **Object** \[attachment\].| |
|item.getVisible\(\) <br> apItem.getVisible\(\)|Returns true if this item is visible \(does not take into account which page is being shown\) or false if it is hidden by a rule, stage, or JavaScript, or if its parent is hidden.| |
|apItem.isMissing\(\)|Returns true if this item is required and it has no value.| |
|apItem.isRequired\(\)|Returns true if the item is required, otherwise false.| |
|apItem.isValid\(\)|Returns true if the data is valid. Returns false if the data is invalid.| |
|item.removeClasses\(classes\) <br> apItem.removeClasses\(classes\)|Removes a list of custom class names from an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.|```item.removeClasses("emphasized");```|
|item.setActive\(active\) <br> apItem.setActive\(active\)|Sets whether this item is inactive, or read only. <br><br> **Note:** If this item is made inactive by a rule or stage, then you cannot make it active with JavaScript.| |
|item.setDisplayValue\(pValue\) <br> apItem.setDisplayValue\(pValue\)|Takes a string or number in pValue. This method sets the value being displayed. If the user is editing, then it will update the value they are trying to enter. If the user is not editing, then it will be the same as setValue\(\). This method works on direct input items such as single line, multi line, number, currency, email and website.| |
|item.setFocus\(\) <br> apItem.setFocus\(\)|Causes this item to receive focus. This option has no effect on items that cannot have focus, are invisible, or are read-only.| |
|item.setHintText\(pValue\) <br> apItem.setHintText\(pValue\)|Takes a pValue string. This method sets the text that is used for hover text on input items. If an empty value is provided, the hint text area is removed.| |
|item.setHoverText\(pValue\) <br> apItem.setHoverText\(pValue\)|Takes a pValue string. This method sets the text that is used for **Hint** text on input items. If an empty value is provided, no hover help is displayed.| |
|apItem.setRequired\(required\)|You can override non-required data to be required with this method. Passing true causes its data to be required and prevents submission if it is not set. Setting the valid to false clears any previously overridden value.| |
|item.setRows\(pValue\)|Takes a pValue number. This method sets the number of rows the text area displays. <br> **Note:** Whenever possible, do not exceed 40 rows.| |
|item.setPlaceholderText\(pValue\) <br> apItem.setPlaceholderText\(pValue\)|Takes a pValue string. This method sets the text used as placeholder text on input items.| |
|item.setStartLabel\(pValue\)|Takes a pValue string. This method sets the value of the label displayed at the start of a numeric or choice slider.| |
|item.setStopLabel\(pValue\)|Takes a pValue string. This method sets the value of the label displayed at the end of a numeric or choice slider.| |
|item.setStyle\(pValue\)|Takes a pValue string. This method sets the style used to display time and dates. Valid values are numeric, short, medium, long, and full. Valid values for time are numeric, short and medium.| |
|item.setTitle\(pValue\) <br> apItem.setTitle\(pValue\)|Takes a pValue string. This method sets the text used for a field titles on input items. If an empty value is provided, the title is removed.| |
|apItem.setValid\(valid, msg\)|You can override valid data to be invalid with this method. Passing false causes the data to be invalid, and prevents submission. You can optionally provide a custom error message. Setting the valid to true clears any previously overridden valid value.| |
|item.setValue\(pValue\) <br> apItem.setValue\(pValue\)|Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String. <br><br> **Note:** The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.| |
|item.setVisible\(visible\) <br> apItem.setVisible\(visible\)|Sets whether this item is visible. <br><br> **Note:** If this item is made invisible by a rule or stage, or because a parent is hidden, then you cannot unhide it by calling this function.| |
|apItem.validate\(\)|Triggers the validation of the data item.| |
|item.getColumnHeaders\(\)|Returns a JSON object that contains the id, title and width of each header displayed for the table. <br><br> Sample JSON output: <br> ```[{id:"F_Currency1",title:"La Currency",width:20}, <br> {id:"F_Date1",title:"La Date"}]```|<code>var headers =  page.F_Table1.getColumnHeaders(); <br> for(var h in headers) { <br> alert("ID=" + get(headers,h).id + <br> ", title=" + get(headers,h).title + <br> ", width=" + get(headers,h).width); <br> }</code>|
|item.setColumnHeaders\(headers\)|Function accepts a JSON object that can be used to set the id, title and width of each column in the table. <br> This is helpful, for example, to change the language of the column header displayed.|<code>var headers = new Array(); <br> set(headers, 0, {id: "F_Currency1", title: "La Currency", width: 20}); <br> set(headers, 1, {id: "F_Date1", title: "La Date"}); <br> page.F_Table1.setColumnHeaders(headers);`|

Table 2. List of item types

|Palette item|Type|Palette item|Type|
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

Table 3. Item Object - Drop Down only

|Object|Description|Example|
|------|-----------|-------|
|item.getOptions\(\)|Returns the array of options currently shown in the drop-down. Each object in the array has a “title” property that is shown in the interface, and a “value” property that is saved into the data.|Get the title of a specific dropdown value: <br> <code> var displayedValue = ""; <br> var savedValue = BO.F_DropDown1.getValue(); <br> var opts = page.F_DropDown1.getOptions(); <br> for(var i=0; i<opts.length; i++) { <br> var opt = get(opts, i); <br> if(opt.value === savedValue) { <br> displayedValue = opt.title; <br> break; <br> } <br> } </code>|
|item.setOptions\(options\)|Changes the list of options to show in the drop-down. It must be an array of objects. Each object must have a “title” property that is shown in the interface, and a “value” property that is saved into the data.|Provide custom list for the drop-down: <br> `var options = new Array();` <br> `options.push({title:'Banana',value:'BA'});` <br> `options.push({title:'Apple',value:'AP'});` <br> `options.push({title:'Orange',value:'OR'});` <br> `item.setOptions(options);`|

Table 4. Item Object - Weblink only

|Object|Description|
|------|-----------|
|item.setDisplayValue\(display\)|Sets the display value that the user sees as the link in the browser.|
|item.setLinkValue\(link\)|Sets the URL to which the link navigates when this item is clicked.|

Table 5. Item Object - HTML Fragment only

|Object|Description|
|------|-----------|
|item.getContent\(\)|Gets the currently shown content for this interface item.|
|item.setContent\(content\)|Shows content in this interface only item. The content is evaluated as HTML code.|

Table 6. Item Object - Text only

|Object|Description|
|------|-----------|
|item.setContent\(content\)|Shows content in this interface-only item. In Text, it is the raw text to show, no special formatting is supported.|

Table 7. Item Object - Button only

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

Table 8. Item Object - Image only

|Object|Description|
|------|-----------|
|item.getHeight\(\)|Returns the current image height. Can be zero or blank.|
|item.getURL\(\)|Gets the current URL shown by this image item.|
|item.getWidth\(\)|Returns the current image width. Can be zero or blank.|
|item.setHeight\(height\)|Sets explicit height in pixels for the image. Setting “0” removes the explicit height.|
|item.setURL\(newURL\)|Sets the URL shown by this image item.|
|item.setWidth\(width\)|Sets explicit width in pixels for the image. Setting “0” removes the explicit width.|

Table 9. Item Object - Section only

|Object|Description|
|------|-----------|
|item.getExpanded\(\)|Returns true if the section is expanded and false if it is collapsed.|
|item.setExpanded\(expanded\)|Sets the expanded state of the section. If true, the section is expanded. If false, then it is collapsed.|

Table 10. Item Object - Tabbed Folder only

|Object|Description|Example|
|------|-----------|-------|
|item.getSelectionIndex\(\)|Returns the index of the currently selected tab.|Set 12 into the first item in the currently shown tab:`var sel = item.getSelectionIndex();` <br> `var tabs = item.getChildren();` <br> `var selTab = tabs.get(sel);` <br> `var tabChildren = selTab.getChildren();` <br> `tabChildren.get(0).getBOAttr().setValue(12);`|
|item.getTabTitleList\(\)|Returns an array of all the tab titles in this folder.| |
|item.setSelectedTab\(tabTitle\)|Takes a tabTable string. Selects the Tab that matches the tabTable string.| |
|item.setTabTitle\(tabIndex,pTitle\)|Updates the title of a tab within a **Tabbed Folder** by using a **tabIndex** integer and **pTitle** string value. **tabIndex** denotes the location of the tab within the list of available tabs from left-to-right. For bidirectional languages, the order is right-to-left.|On the form, a Tabbed folder contains 5 tabs: Red, Orange, Yellow, Green, Blue. The default start number of the **tabIndex** is 0. <br><br> In our example tabbed folder, the **tabIndex** number 0 is the Red tab which is furthest left, while 4 is the tab furthest to the right. <br><br> In a bidirectional language, the order is reversed. Tab 0 is assigned to Blue, which is the tab furthest to the right.|
|item.setTabTitleList\(pTitleArray\)|Updates the titles of tabs within a **Tabbed Folder** from a list of strings by using a **pTitleArray** array of string values. The list of tabs is updated respective to the order of strings that are defined in the array. If there are more array values than tabs in the form, the additional values are ignored.|```item.setTabTitleList(['Monday','Tuesday','Wednesday','Thursday','Friday']);```|

Table 11. Item Object - Table only

*See the Business Object List on the Data Objects page for more Table functionality.*

|Object|Description|Example|
|------|-----------|-------|
|item.getSelection\(\)|Returns the Business Object of the selected row or null if there is no selection.| |
|item.setSelection\(BO\)|Selects the last Business Object in the table.|Select that last row in the table: <br> `var lastIndex = item.getBOAttr().getLength()-1;` <br> `var lastRow = item.getBOAttr().get(lastIndex);` <br> `item.setSelection(lastRow);`|
|item.showAdd\(show\)|If show is true, then the **Add** button is made visible. If false, then the **Add** button is hidden.| |
|item.showEdit\(show\)|If show is true, then the **Edit** button is made visible. If false, then the **Edit** button is hidden.| |
|item.showRemove\(show\)|If show is true, then the **Remove** button is made visible. If false, then the **Remove** button is hidden.| |

Table 12. Item Object - Survey only

|Object|Description|
|------|-----------|
|item.getOptions\(\)|Returns an array of all the options for the survey questions. Each option has a value property, that gets saved in the data, and a display property, the title of at the beginning of the survey.|

Table 13. Item Object - DataGrid only

*columnId is used generically to refer to the column in the DataGrid and the corresponding data attribute of the row’s data. The built-in columns are stageId, created, createdBy, lastModified, and lastModifiedBy.*

|Object|Description|Example|
|------|-----------|-------|
|item.getDisplayedData\(\)|-   Boolean: Checkbox <br> -   Number : Number, Currency, Numeric Slider <br> -   Date: Date, Time, Timestamp <br> -   Object: Attachment <br> -   `uid`: The identifier of the attachment. <br> -   `filename`: the file name of the attachment. <br> -   `viewUrl`: The url to view the attachment. <br> -   `downloadUrl`: The url to download the attachment. <br> -   Object: Name Picker <br> -   Object: Select Many <br> -   `savedValues`: An array of all the saved values. <br> -   `displayValues`: An array of all the display values. <br> -   `displayString`: All the list values provided as a comma-separated string. <br> -   String: All other items|Render all the row data displayed in the data grid as JSON: <br> ```appPage.F_Text2.setContent(toJson(appPage.F_DataGrid1.getDisplayedData(), true));``` <br><br> Calculate the sum of a column from displayed data: <br> `var data = appPage.F_DataGrid1.getDisplayedData();` <br> `var sum = 0;` <br> `for(var d in data) {` <br> `var dObj = get(data, d);` <br> `sum += dObj.F_Number1;` <br> `}` <br> `alert("Sum = " + sum);`|
|item.isAllDataDisplayed\(\)|Returns true if all the submitted data for the form connected to the data grid is rendered on screen in a single page.|If all the known data is being displayed, then do something with that data. In this example the sum of a column is calculated: <br> <code> if(appPage.F_DataGrid1.isAllDataDisplayed()) { <br> var allData = appPage.F_DataGrid1.getDisplayedData(); <br> var sum = 0; <br> for(var d in allData) { <br> var dObj = get(allData, d); <br> sum += dObj.F_Number1; <br> } <br> alert("Sum = " + sum); <br> }</code>|
|item.isColumnVisible\(columnId\)|Returns true if the specified column is visible in the data grid.|```appPage.F_DataGrid1.isColumnVisble(“F_SingleLine1”);```|
|item.refresh\(\)|Forces the data grid to reload. For example, a submission with “apps as a service” may have been triggered and the content in the data grid is stale.|Refresh the data grid after calling a service that changes \(i.e. adds to, removes from, or updates\) the data to which the data grid is connected: <br> `var srv = form.getServiceConfiguration('SC_theService');` <br> `srv.connectEvent("onCallFinished", function(success)` <br> `{` <br> `if(success) {` <br> `try {` <br> `appPage.F_DataGrid1.refresh();` <br> `} catch (err) {` <br> `alert("SC_theService: " + err);` <br> `}` <br> `}` <br> `});`|
|item.selectFirstRow\(\)|Selects the first row in the data grid.| |
|item.setColumnHeader\(columnId, pHeaderValue\)|Sets the header identified by columnId, to the value provided in pHeaderValue.|See above for columnId values. <br><br> Set the header of a column to another language: <br> `appPage.F_DataGrid1.setColumnHeader("createdBy",` <br> `"Créé par");`|
|item.setColumnVisible\(columnId, boolVal\)|Controls the visibility of the column identified by columnId. If boolVal is true, the column is shown. If boolVal is false, the column is hidden.|See above for columnId values. <br><br> Hide a column from the data grid if user is not part of a specific role: <br> `var isAdmin = app.getCurrentUserRoles().contains("Administrator");`  <br> `item.setColumnVisible("F_AdminOnly1", isAdmin);`|
|item.resetFilters\(\)|Returns the filters to what was specified in the data grid configuration.| |
|item.setFilters\(\[filter\], filterOp\)|Set filters for the data grid, this will override any filters specified in the data grid configuration. \[filter\] is an array of filter objects. filterOp is either “and” or “or” and is required if there is more than one filter. A filter is made up of the following: <br><br> -   name: the id of a meta-data attribute or a field of the form configured to the data grid. <br><br> **Note:** The field id does not have to be displayed in the data grid. <br><br> -   operator: as documented in [Filtering Data REST API results](ref_data_rest_api_list_filter.md). <br> -   value: the value to search|Set a filter to show records that are older than one week and in the “ST\_Triage” stage: <br> `var now = new Date();` <br> `var aWeekAgo = new Date (now.getTime() - (7*24*60*60*1000));` <br> `var filters = [` <br> `{name : "created", operator: "before", value: aWeekAgo},` <br> `{name: "stageId", operator: "equals", value: "ST_Triage"}` <br> `];` <br> `page.F_DataGrid1.setFilters(filters, "and");` <br><br> Set a filter to show records between two dates, from fields on the same app page as the data grid: <br> `var filters = [` <br> `{name: "F_BirthDate", operator: "between", value: [appPage.F_StartDate.getValue(), appPage.F_EndDate.getValue()]}` <br> `];` <br> `appPage.F_DataGrid2.setFilters(filters, "and");`  <br><br> Remove all filters: <br> `appPage.F_DataGrid1.setFilters(null);`|

**Parent topic: **[Interface objects](ref_jsapi_user_interface_objects.md)

