# Item objects { #ref_item_objects .concept }

## Common Functions

This page describes the form item (item) and App Page Item (apItem) Objects.
The object (item/apItem) represents a particular item on a page or appPage, and provides access to its properties. For Sections and Tab Folders, access to their child items is also granted.

### addClasses

Adds a list of custom class names to an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names. If any of the given class names are invalid CSS class names, then no classes are added and false is returned.

**Syntax**

```javascript
item.addClasses(classes)
apItem.addClasses(classes)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| classes       | List of CSS classnames separated by spaces, or an array of class names. |

**Example**

```javascript
// form
item.addClasses("emphasized error");

// app page
apItem.addClasses("emphasized error");
```

### clearRequiredMessage

Validates the item data, but prevents the required error message from displaying.

**Syntax**

```javascript
item.clearRequiredMessage()
apItem.clearRequiredMessage()
```

### connectEvent

Connects a function to an event on the item. Useful for utility functions defined in external JavaScript™ files to hook behavior into the item dynamically. Returns a handle object that represents the connection of the function to that event name. That handle can be used to disconnect this same event using item.disconnectEvent.

**Syntax**

```javascript
item.connectEvent (eventName, callbackFunction)
apItem.connectEvent (eventName, callbackFunction)
```

**Example**

```javascript
// Connect a listener to the onItemChange event to make a section visible. 
// This could be placed in the form onLoad event:  
var hndl = item.connectEvent('onItemChange', function() {
   if(item.getBOAttr().getValue() === 'Yes')
      form.getBO().F_SectionA.setVisible(true);
}});
```

### disconnectEvent

Disconnects the event handler specified by the passed-in event handle object that was returned by an item.connectEvent call.If you connect an item event, you must also disconnect it in the same event. Otherwise, multiple versions of the connected code are attached every time the event is triggered.

**Syntax**

```javascript
item.disconnectEvent (eventHandle)
apItem.disconnectEvent (eventHandle)
```

**Example**

```javascript
// If the connect event is placed in the item onShow then the listener needs to be disconnected: 
var hndl = item.connectEvent('onItemChange', function()
{
   if(item.getBOAttr().getValue() === 'Yes')
     form.getBO().F_SectionA.setVisible(true);
   }
   item.disconnectEvent(hndl);
});
```

### getActive

Returns true if this item is active, or false if it is made read only by a rule, stage, or JavaScript.

**Syntax**

```javascript
item.getActive()
apItem.getActive()
```

### getAppPage

Returns the page object to which this item belongs.

**Syntax**

```javascript
apItem.getAppPage()
```

### getBO

Returns the Business Object for the entire form.

**Syntax**

```javascript
item.getBO()
```

### getBOAttr

An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.

**Syntax**

```javascript
item.getBOAttr()
```

**Example**

```javascript
// Get data element for an item and set its value
item.getBOAttr().setValue(45);
```

### getChildren

If this item contains children, for example Section, or Tab Folder, it returns a list object that provides access to all direct children items. The list object has the getLength() function and get(index) function for accessing the objects in the list.

**Syntax**

```javascript
item.getChildren()
```

**Example**

```javascript
// Reset all numbers inside a section to 0
var list = item.getChildren();
for(var i=0; i<list.getLength(); i++)
{
   if(list.get(i).getType() === 'number')
      list.get(i).getBOAttr().setValue(0);
}
```

### getClasses

Returns an Array of custom class names currently applied to an item.

**Syntax**

```javascript
item.getClasses()
apItem.getClasses()
```

### getDisplayValue

Returns the current value that is being displayed. It can be used in onItemLiveChange to get current, but not yet committed value.

**Syntax**

```javascript
item.getDisplayValue()
apItem.getDisplayValue()
```

### getHoverText

Returns the current value set as hover text.

**Syntax**

```javascript
item.getHoverText()
apItem.getHoverText()
```

### getHintText

Returns the value set as **Hint** text.

**Syntax**

```javascript
item.getHintText()
apItem.getHintText()
```

### getId

Returns the unique ID, within the application, of this item. For example, F_FirstName.

**Syntax**

```javascript
item.getId()
apItem.getId()
```

### getInvalidMessage

An interface item that is collecting data, this method returns the Business Object Attribute that contains that data. If it is an interface-only item, then it returns null.

**Syntax**

```javascript
apItem.getInvalidMessage()
```

### getPage

Returns the page object to which this item belongs.

**Syntax**

```javascript
item.getPage()
```

**Example:**

```javascript
// Get the form object
var form = item.getPage().getForm();
```

### getParent

Returns the object that is the direct parent of the item, which can be a page, section, or tab folder.

**Syntax**

```javascript
apItem.getParent()
```

### getPlaceholderText

Returns the current value set as place holder text.

**Syntax**

```javascript
item.getPlaceholderText()
apItem.getPlaceholderText()
```

### getRequired

Gets a value set previously using setRequired().

**Syntax**

```javascript
apItem.getRequired()
```

### getStartLabel

This method gets the value of the label displayed at the start of a numeric or choice slider.

**Syntax**

```javascript
item.getStartLabel()
```

### getStopLabel

This method gets the value of the label displayed at the end of a numeric or choice slider.

**Syntax**

```javascript
item.getStopLabel()
```

### getStyle

Returns the current value set for display style.

!!! note
    This parameter works only on **Date** and **Time** input fields.

**Syntax**

```javascript
item.getStyle()
```

### getTitle

Returns the current value used as the field title.

**Syntax**

```javascript
item.getTitle()
apItem.getTitle()
```

### getType

Returns a string identifying the object type.

| Palette Item  | Type        | Palette Item  | Type        |
| :------------ | :---------- | :------------ | :---------- |
| Attachment| attachment | Password | password |
| Button | button | Rich text | richTextArea
| Check Box | checkBox | Section | section |
| Currency | currency | Select Many | checkGroup |
| Date | date | Select One | radioGroup |
| Dropdown | comboBox | Single Line | text |
| Email Address | emailAddress | Survey | survey |
| Folder Tab | tabFolderTab | Survey Question | surveyQuestion |
| HTML Fragment | htmlArea | Tabbed folder | tabFolder |
| Image | image | Table | aggregationListContainer |
| Line | horizontalLine | Text | richText |
| Media | media | Time | time |
| Multi-Line | textArea | Timestamp | timeStamp |
| Number | number | Web Link | staticWebLink |
| Numeric Slider | horizontalSlider | Website | weblink |
| Page | page | Name Picker | name |
| Page Navigation | pageNavigator | Data Grid | dataGrid |

**Syntax**

```javascript
item.getType()
apItem.getType()
```

### getValid

Gets a value set previously using setValid().

**Syntax**

```javascript
apItem.getValid()
```

### getValue

Returns the current value. Its type depends on the data type.

| Palette Item  | Type        | Palette Item  | Type        |
| :------------ | :---------- | :------------ | :---------- |
| Attachment | Object | Password | String |
| Button | N/A | Rich text | N/A |
| Check Box | Boolean | Section | N/A |
| Choice Slider | String | Select Many | String, delimited by **#** |
| Currency | Number | Select One | String |
| Date | Date | Single Line | String |
| Dropdown | String | Survey | N/A |
| Email Address | String | Survey Question | String |
| Folder Tab | N/A | Tabbed folder | N/A |
| HTML Fragment | N/A | Table | N/A |
| Image | N/A | Text | N/A |
| Line | N/A |
| Link | N/A |
| Media | N/A | Time | Date |
| Multi-Line | N/A | Timestamp | Date |
| Name picker | Object| Web Link | String |
| Number | Number | Website | String |  
| Numeric Slider | Number | Name Picker | String |
| Page | N/A | Data Grid | N/A |
| Page Navigation | N/A |
| Paragraph Text | N/A |

**Syntax**

```javascript
item.getValue()
apItem.getValue()
```

### getVisible

Returns true if this item is visible (does not take into account which page is being shown) or false if it is hidden by a rule, stage, or JavaScript, or if its parent is hidden.

**Syntax**

```javascript
item.getVisible()
apItem.getVisible()
```

### isMissing

Returns true if this item is required and it has no value.

**Syntax**

```javascript
item.isMissing()
apItem.isMissing()
```

### isRequired

Returns true if the item is required, otherwise false.

**Syntax**

```javascript
apItem.isRequired()
```

### isValid

Returns true if the data is valid. Returns false if the data is invalid.

**Syntax**

```javascript
apItem.isValid()
```

### removeClasses

Removes a list of custom class names from an item for dynamic CSS styling. The classes parameter can be a single class name, multiple class names separated by spaces, or an Array of class names.

**Syntax**

```javascript
item.removeClasses(classes)
apItem.removeClasses(classes)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| classes       | List of CSS classnames separated by spaces, or an array of class names. |

**Example**

```javascript
item.removeClasses("emphasized");
```

### setActive

Sets whether this item is inactive, or read only.

!!! note
    If this item is made inactive by a rule or stage, then you cannot make it active with JavaScript.

**Syntax**

```javascript
item.setActive(active)
apItem.setActive(active)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| active        | True or False |

### setDisplayValue

This method sets the value being displayed. If the user is editing, then it will update the value they are trying to enter. If the user is not editing, then it will be the same as setValue(). This method works on direct input items such as single line, multi-line, number, currency, email and website.

**Syntax**

```javascript
item.setDisplayValue(pValue)
apItem.setDisplayValue(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String or number value |

### setFocus

Causes this item to receive focus. This option has no effect on items that cannot have focus, are invisible, or are read-only.

**Syntax**

```javascript
item.setFocus()
apItem.setFocus()
```

### setHintText

This method sets the text that is used for hover text on input items. If an empty value is provided, the hint text area is removed.

**Syntax**

```javascript
item.setHintText(pValue)
apItem.setHintText(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setHoverText

This method sets the text that is used for **Hint** text on input items. If an empty value is provided, no hover help is displayed.

**Syntax**

```javascript
item.setHoverText(pValue)
apItem.setHoverText(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setRequired

You can override non-required data to be required with this method. Passing true causes its data to be required and prevents submission if it is not set. Setting the required to false clears any previously overridden value.

**Syntax**

```javascript
apItem.setRequired(required)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| required      | True or False  |

### setPlaceholderText

This method sets the text used as placeholder text on input items.

**Syntax**

```javascript
item.setPlaceholderText(pValue)
apItem.setPlaceholderText(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setStartLabel

This method sets the value of the label displayed at the start of a numeric or choice slider.

**Syntax**

```javascript
item.setStartLabel(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setStopLabel

This method sets the value of the label displayed at the end of a numeric or choice slider.

**Syntax**

```javascript
item.setStopLabel(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setStyle

This method sets the style used to display time and dates. Valid values are numeric, short, medium, long, and full. Valid values for time are numeric, short and medium.

**Syntax**

```javascript
item.setStyle(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setTitle

This method sets the text used for a field titles on input items. If an empty value is provided, the title is removed.

!!! note
    The item.setTitle function is not applicable to Tabbed Folder form items.

**Syntax**

```javascript
item.setTitle(pValue)
apItem.setTitle(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | String  |

### setValid

You can override valid data to be invalid with this method. Passing false causes the data to be invalid, and prevents submission. You can optionally provide a custom error message. Setting the valid to true clears any previously overridden valid value.

**Syntax**

```javascript
apItem.setValid(valid, msg)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| valid         | True or false  |
| msg | Optional. Custom error message |

### setValue

Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String.

!!! note
    The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.

**Syntax**

```javascript
item.setValue(pValue)
apItem.setValue(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | Value based on objects type  |

### setVisible

Sets whether this item is visible.

!!! note
    If this item is made invisible by a rule or stage, or because a parent is hidden, then you cannot unhide it by calling this function.

**Syntax**

```javascript
item.setVisible(visible)
apItem.setVisible(visible)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| visible       | True or false. |

### validate

Triggers the validation of the data item.

**Syntax**

```javascript
apItem.validate()
```

## Drop Down Functions

Functions that only apply to the drop down palette item.

### getOptions

Returns the array of options currently shown in the drop-down. Each object in the array has a "title" property that is shown in the interface, and a "value" property that is saved into the data.

**Syntax**

```javascript
item.getOptions()
```

**Example**

```javascript
// Get the title of a specific dropdown value
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

### setOptions

Changes the list of options to show in the drop-down.

**Syntax**

```javascript
item.setOptions(options)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| options       | Array of objects. Each object must have a "title" property that is shown in the interface, and a "value" property that is saved into the data. |

**Example**

```javascript
// Provide custom list for the drop-down
var options = new Array();
options.push({title:'Banana', value:'BA'});
options.push({title:'Apple', value:'AP'});
options.push({title:'Orange', value:'OR'});
item.setOptions(options);
```

## Link Functions

Functions that only apply to the link palette item.

### setDisplayValue

Sets the display value that the user sees as the link in the browser.

**Syntax**

```javascript
item.setDisplayValue(display)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| display       | String value |

### setLinkValue

Sets the URL to which the link navigates when this item is clicked.

**Syntax**

```javascript
item.setLinkValue(link)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| link          | Url to set |

**Example**

Demonstrates how to use a Link item to launch another {{shortProductName}} form in the same application. To launch a form from a different application replace 'app.getUID()' with the uid of the target application.

```javascript
item.setLinkValue('/{{context}}/secure/1/app/' + app.getUID() + '/launch/index.html?form=F_NewForm1');
item.setDisplayValue('Launch New Form');
```

## HTML Fragment Functions

Functions that only apply to the HTML palette item.

### getContent

Gets the currently shown content for this interface item.

**Syntax**

```javascript
item.getContent()
```

### setContent

Sets content in this interface only item. The content is evaluated as HTML code.

**Syntax**

```javascript
item.setContent(content)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| content       | String, evaluated as HTML |

## Text Functions

Functions that only apply to the text palette item.

### setContent

Sets content in this interface-only item. In Text, it is the raw text to show, no special formatting is supported.

**Syntax**

```javascript
item.setContent(content)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| content       | String |

## Button Functions

Functions that only apply to the button palette item.

### setAlternativeText

Sets the alt text of the image assigned to the button.

**Syntax**

```javascript
item.setAlternativeText(pText)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pText         | String |

### setContent

Sets the label that is shown on the button.

**Syntax**

```javascript
item.setContent(content)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| content       | String |

### setDisabledImageUrl

Sets the background of the button to the image at the public URL when the button is disabled.

**Syntax**

```javascript
item.setDisabledImageUrl(pUrl)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pUrl          | Url of the image |

### setImageHeight

Sets explicit height in pixels for the image.

**Syntax**

```javascript
item.setImageHeight(pHeight)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pHeight       | Height in pixels |

### setImageUrl

Sets the background of the button to the image at the public URL.

**Syntax**

```javascript
item.setImageUrl(pUrl)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pUrl          | Url of the image |

### setImageWidth

Sets explicit width in pixels for the image.

**Syntax**

```javascript
item.setImageWidth(pWidth)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pWidth        | Width in pixels |

### setMouseDownImageUrl

Sets the background of the button to the image at the public URL when the mouse down event is triggered.

**Syntax**

```javascript
item.setMouseDownImageUrl(pUrl)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pUrl          | Url of the image |

### setMouseOverImageUrl

Sets the background of the button to the image at the public URL when the mouse over event is triggered.

**Syntax**

```javascript
item.setMouseOverImageUrl(pUrl)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pUrl          | Url of the image |

## Image Functions

Functions that only apply to the image palette item.

### getHeight

Returns the current image height. Can be zero or blank.

**Syntax**

```javascript
item.getHeight()
```

### getUrl

Gets the current URL shown by this image item.

**Syntax**

```javascript
item.getURL()
```

### getWidth

Returns the current image width. Can be zero or blank.

**Syntax**

```javascript
item.getWidth()
```

### setHeight

Sets explicit height in pixels for the image. Setting "0" removes the explicit height.

**Syntax**

```javascript
item.setHeight(height)
```

### setURL

Sets the URL shown by this image item.

**Syntax**

```javascript
item.setURL(pURL)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pUrl          | Url to set |

### setWidth

Sets explicit width in pixels for the image. Setting "0" removes the explicit width.

**Syntax**

```javascript
item.setWidth(width)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pWidth        | Width in pixels |

## Multi-Line Entry Functions

### getRows

Returns the current value set as the number of rows displayed. This method gets the number of rows the text area displayed.

**Syntax**

```javascript
item.getRows()
```

### setRows

This method sets the number of rows the text area displays.

!!! note
    Whenever possible, do not exceed 40 rows.

**Syntax**

```javascript
item.setRows(pValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pValue        | A number  |

## Section Functions

Functions that only apply to the section palette item.

### getExpanded

Returns true if the section is expanded and false if it is collapsed.

**Syntax**

```javascript
item.getExpanded()
```

### setExpanded

Sets the expanded state of the section.

**Syntax**

```javascript
item.setExpanded(expanded)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| expanded      | If true, the section is expanded. If false, then it is collapsed. |

## Tabbed Folder Functions

Functions that only apply to the tabbed folder palette item.

### getSelectionIndex

Returns the index of the currently selected tab.

**Syntax**

```javascript
item.getSelectionIndex()
```

**Example**

```javascript
// Set 12 into the first item in the currently shown tab
var sel = item.getSelectionIndex();
var tabs = item.getChildren();
var selTab = tabs.get(sel);
var tabChildren = selTab.getChildren();
tabChildren.get(0).getBOAttr().setValue(12);
```

### getTabTitleList

Returns an array of all the tab titles in this folder.

**Syntax**

```javascript
item.getTabTitleList()
```

### setSelectedTab

Selects the Tab that matches the tabTitle string.

**Syntax**

```javascript
item.setSelectedTab(tabTitle)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| tabTitle      | String matching tab title |

### setTabTitle

Updates the title of a tab within a **Tabbed Folder** by using a **tabIndex** integer and **pTitle** string value. **tabIndex** denotes the location of the tab within the list of available tabs from left-to-right. For bidirectional languages, the order is right-to-left.

**Syntax**

```javascript
item.setTabTitle(tabIndex, pTitle)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| tabIndex      | Integer.  Index of tab, starting at 0. |
| tabTitle      | String value to set the tab title |

**Example**

On the form, a Tabbed folder contains 5 tabs: Red, Orange, Yellow, Green, Blue. The default start number of the **tabIndex** is 0.

In our example tabbed folder, the **tabIndex** number 0 is the Red tab which is furthest left, while 4 is the tab furthest to the right.

In a bidirectional language, the order is reversed. Tab 0 is assigned to Blue, which is the tab furthest to the right.

### setTabTitleList

Updates the titles of tabs within a **Tabbed Folder** from a list of strings by using a **pTitleArray** array of string values. The list of tabs is updated respective to the order of strings that are defined in the array. If there are more array values than tabs in the form, the additional values are ignored.

**Syntax**

```javascript
item.setTabTitleList (pTitleArray)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pTitleArray   | Array of titles to use for tabs |

**Example**

```javascript
item.setTabTitleList(['Monday','Tuesday','Wednesday','Thursday','Friday']);
```

## Table Functions

Functions that only apply to the table palette item.

### getSelection

Returns the Business Object of the selected row or null if there is no selection.

**Syntax**

```javascript
item.getSelection()
```

**Example**

```javascript
// displays an alert showing the row number of the selected table row
var selectedRow = page.F_Table1.getSelection();

for(var i=0;i<BO.F_Table1.getLength();i++) {
  var tempRow = BO.F_Table1.get(i);
  if(tempRow === selectedRow){
    alert("Row " + i + " selected.");
    break; 
  }
}
```

### setSelection

Sets the selected row of the table to the Business Object provided.

**Syntax**

```javascript
item.setSelection(pBO)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| pBO   | The business object of a row in the table |

**Example**

```javascript
// Select that last row in the table
var lastIndex = item.getBOAttr().getLength()-1;
var lastRow = item.getBOAttr().get(lastIndex);
item.setSelection(lastRow);
```

### showAdd

If show is true, then the **Add** button is made visible. If false, then the **Add** button is hidden.

**Syntax**

```javascript
item.showAdd(show)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| show   | True or false. |

**Example**

```javascript
// hide the add button if the table has 5 rows
var theTable = BO.F_Table1;
if (theTable.getLength() <= 5)
{
  theTable.showAdd(true);
}
else
{
  theTable.showAdd(false);
}
```

### showEdit

If show is true, then the **Edit** button is made visible. If false, then the **Edit** button is hidden.

**Syntax**

```javascript
item.showEdit(show)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| show   | True or false. |

**Example**

```javascript
var selectedRow = page.F_Table1.getSelection();
if(selectedRow === null)
{
  page.F_Table1.showEdit(false);
}
else
{
  page.F_Table1.showEdit(true);
}
```

### showRemove

If show is true, then the **Remove** button is made visible. If false, then the **Remove** button is hidden.

**Syntax**

```javascript
item.showRemove(show)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| show   | True or false. |

**Example**

```javascript
// Hide the remove button if the table row field doesn't match another field's value
var selectedRow = page.F_Table1.getSelection();
if(selectedRow !== null) {
  if(selectedRow.F_SingleLine1.getValue() !== BO.F_SingleLine5.getValue()) {
    //don't allow delete
    page.F_Table1.showRemove(false);
  } else {
    page.F_Table1.showRemove(true);
  }
} else {
  page.F_Table1.showRemove(false);
}
```

### getColumnHeaders

Returns a JSON object that contains the id, title and width of each header displayed for the table.

Sample JSON output:

```javascript
[
  { id:"F_Currency1",title:"La Currency",width:20 },
  { id:"F_Date1",title:"La Date" }
]
```

**Syntax**

```javascript
item.getColumnHeaders()
```

**Example**

```javascript
var headers =  page.F_Table1.getColumnHeaders();
for(var h in headers) {
  alert("ID=" + get(headers,h).id +
  ", title=" + get(headers,h).title + 
  ", width=" + get(headers,h).width);
}
```

### setColumnHeaders

Function accepts a JSON object that can be used to set the id, title and width of each column in the table.

**Syntax**

```javascript
item.setColumnHeaders(headers)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| headers       | JSON object with id, title and with |

**Example**

```javascript
// This is helpful, for example, to change the language of the column header displayed.  
var headers = new Array(); 
set(headers, 0, {id: "F_Currency1", title: "La Currency", width: 20}); 
set(headers, 1, {id: "F_Date1", title: "La Date"}); 
page.F_Table1.setColumnHeaders(headers); 
```

## Survey Functions

Functions that only apply to the survey palette item.

## getOptions

Returns an array of all the options for the survey questions. Each option has a value property, that gets saved in the data, and a display property, the title of at the beginning of the survey.

**Syntax**

```javascript
item.getOptions()
```

**Example**

For a survey item that had the options; 'yes', 'maybe' and 'no'.

```javascript
// get the options and convert to a JSON string
var surveyQs = item.getOptions();
alert(toJson(surveyQs));
```

The returned object is an array of objects with 'value' and 'display' properties:

```json
[{"value":"Yes","display":"Yes"},{"value":"Maybe","display":"Maybe"},{"value":"No","display":"No"}]
```

## DataGrid Functions

Functions that only apply to the survey palette item.

### getDisplayedData

Gets all the data that is currently displayed in the data grid.

The data types returned is based on the field type:

| Field Type    | Datatype |
| :------------ | :---------- |
| Checkbox      | Boolean |
| Date | Date |
| Time | Date |
| Timestamp | Date |
| Number | Number |
| Currency | Number |
| Numeric Slider | Number |
| Attachment | Object |
| Name Picker | Object |
| Select Many | Object |
| All other items | String |

*Attachment*

- <code>uid</code>: The identifier of the attachment.
- <code>filename</code>: the file name of the attachment.
- <code>viewUrl</code>: The url to view the attachment.
- <code>downloadUrl</code>: The url to download the attachment.

*Name Picker*

- <code>id</code>: The id of the person or group
- <code>displayName</code>: The display name of the person or group
- <code>email</code>: The email address of the person
- <code>type</code>: The type of the user or group

*Select Many*

- <code>savedValues</code>: An array of all the saved values.
- <code>displayValues</code>: An array of all the display values.
- <code>displayString</code>: All the list values provided as a comma-separated string.
  
**Syntax**

```javascript
item.getDisplayedData()
```

**Examples:**

Render all the row data displayed in the data grid as JSON:

```javascript
appPage.F_Text2.setContent(toJson(appPage.F_DataGrid1.getDisplayedData(), true));
```

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

### isAllDataDisplayed

Returns true if all the submitted data for the form connected to the data grid is rendered on screen in a single page.

**Syntax**

```javascript
item.isAllDataDisplayed()
```

**Example**

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

### isColumnVisible

Returns true if the specified column is visible in the data grid.

**Syntax**

```javascript
item.isColumnVisible (columnId)
```

**Example**

```javascript
appPage.F_DataGrid1.isColumnVisble("F_SingleLine1");
```

### refresh

Forces the data grid to reload. For example, a submission with "apps as a service" may have been triggered and the content in the data grid is stale.

**Syntax**

```javascript
item.refresh()
```

**Example**

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

### selectFirstRow

Selects the first row in the data grid.

**Syntax**

```javascript
item.selectFirstRow()
```

### setColumnHeader

Sets the header identified by columnId, to the value provided in pHeaderValue.

**Syntax**

```javascript
item.setColumnHeader (columnId, pHeaderValue)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| columnId      | The id of the column. |
| pHeaderValue  | The string used to set the column header |

**Example**

```javascript
// Set the header of a column to another language
appPage.F_DataGrid1.setColumnHeader("createdBy", "Créé par");
```

### setColumnVisible

Controls the visibility of the column identified by columnId. If boolVal is true, the column is shown. If boolVal is false, the column is hidden.

**Syntax**

```javascript
item.setColumnVisible(columnId, boolVal)
```

**Example**

```javascript
// Hide a column from the data grid if user is not part of a specific role
var isAdmin = app.getCurrentUserRoles().contains("Administrator");
item.setColumnVisible("F_AdminOnly1", isAdmin);
```

### resetFilters

Returns the filters to what was specified in the data grid configuration.

**Syntax**

```javascript
item.resetFilters()
```

### setFilters

Set filters for the data grid, this will override any filters specified in the data grid configuration.

A filter is made up of the following:

- *name*: the id of a meta-data attribute or a field of the form configured to the data grid.

    !!! note
        The field id does not have to be displayed in the data grid.

- *operator*: as documented in [Filtering Data REST API results](ref_data_rest_api_list_filter.md).
- *value*: the value to search

**Syntax**

```javascript
item.setFilters([filter], filterOp)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| filter        | is an array of filter objects ({name: '', operator: '', value: ''}) |
| filterOp | is either "and" or "or" and is required if there is more than one filter |

**Examples**

```javascript
// Set a filter to show records that are older than one week and in the "ST_Triage" stage
var now = new Date(); 
var aWeekAgo = new Date (now.getTime() - (7*24*60*60*1000)); 
var filters = [ 
    {name : "created", operator: "before", value: aWeekAgo}, 
    {name: "stageId", operator: "equals", value: "ST_Triage"}   
]; 
page.F_DataGrid1.setFilters(filters, "and"); 

```

```javascript
// Set a filter to show records between two dates, from fields on the same app page as the data grid
var filters = [
  {
    name: "F_BirthDate", 
    operator: "between", 
    value: [appPage.F_StartDate.getValue(), appPage.F_EndDate.getValue()]
  }
];
appPage.F_DataGrid2.setFilters(filters, "and");
```

```javascript
// Remove all filters
appPage.F_DataGrid1.setFilters(null);
```

**Parent topic:** [Interface objects](ref_jsapi_user_interface_objects.md)
