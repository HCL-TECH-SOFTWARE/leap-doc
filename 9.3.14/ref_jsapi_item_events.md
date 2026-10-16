# Item Events 

This topic describes the Item Events, and their parameters when using JavaScript™ API in {{fullLeapProductName}}.

There are many events available to hook into on an item that is accessed from the item **Edit Properties** dialog.

## JavaScript™ objects

|Variable|Full name|Description|Example|Type|
|--------|---------|-----------|-------|----|
|app|Application object|Contains functions for accessing global general information|`app.isSingleFormView()`|GUI|
|page|Page object|For accessing the Page and the items on it|`page.F_Text.setContent('This a Label');`|GUI|
|form|Form object|For accessing the pages and controlling page navigation|`form.getPage('P_Page1');`|GUI|
|item|Item object|The object representing the current item|`item.setVisible(true);`|GUI|
|BO|Business Object object|Top-level data object for the form|`BO.F_Username.getValue();`|DATA|
|BOA|Business Object Attribute object|Object representing the Data for the current item. Only present for data items|`BOA.setValue("Please enter your Name");`|DATA|

## Item Events

### onClick

Called every time that the item is selected by the user.


### onHide

Called every time that the item is hidden, whether just itself or the entire page.


### onInvalid 

Only applies to data items. Called when a data item goes from being valid to invalid.


### onItemBlur

Called when the item is blurred (focus is lost).


### onItemChange

Called when the item data is changed and saved into the Business Object. For some types of items, it occurs when the user tabs or switches focus, for example, when users select Number, Single Line, Multi-Line, and Currency form items. For other items, it occurs every time they make a change, such as Check Box, Survey, or drop-down.

!!! note
    You cannot change the value of an item within this event as its value has changed, and it is locked.


### onItemFocus

Called when focus is received by an item.


### onItemLiveChange

Only applies to items which can be incrementally changed. Called every time data is entered but not yet updated to the Business Object, such as Number, Single Line, Multi-Line, and Currency.


### onMouseOut

Called every time the mouse moves out of the item bounding area (not including label).


### onMouseOver

Called every time the mouse moves into the item bounding area (not including label).


### onShow

Called every time the item goes from being hidden to being shown, whether from a page flip or because of a rule or JavaScript change.


### onValid

Only applies to data items. Called when a data item goes from being invalid to valid.


## Table Events

### onAdd

This event is called after an entry is added to the table. The newly added item data is available from the variable itemBO.

**Example**

Add a value from the new row to a subtotal field:

```javascript
var curValue = BO.F_Total.getValue();
curValue += itemBO.F_Price.getValue();
BO.F_Total.setValue(curValue);
```

### onEdit

Called after an existing row is edited by the user. The item that was edited is available from the variable itemBO.


### onRemove

Called after a row is deleted from the table by the user. The item that was deleted is available from the variable itemBO.


## Tabbed Folder Events

### onTabSelected

Called after a tab is selected.


## Section Events

### onCollapse

Called when the section is collapsed.


### onExpand

Called when the section is expanded.


## List Item Events

### beforeOptionsUpdate

This event is called before the options in a drop-down list are updated from a service call or from an API call. The array of options is passed in as pOptions and can be modified by the event code. By default, when a new options list is set into a drop-down list and the current selected item is not in the new list, it is added into the new list automatically. If you return false from this event, it does not copy the missing option into the new list.

**Example**

```javascript
pOptions.push({title:'Pizza', value:'fooditem3'});
return false;
```

## DataGrid Events

### onDataChange

This event is invoked when new data is rendered in the Data Grid.

### onHide

This event is invoked after the item is hidden (either with the entire form or just this item).

### onRowDeselect

This event is invoked when a row is deselected in the Data Grid.

### onRowSelect

This event is invoked when a row is selected in the Data Grid. The ```rowData``` object is available and contains all the data.

Every rowData object contains the general properties:
- created
- createdBy
- editUrl
- flowState
- id
- lastModified
- lastModifiedBy
- printUrl
- stageId
- stageTitle
- uid

Access the properties using the syntax rowData.<propertyName>.

```javascript
appPage.F_SelectedRowUid.setValue(rowData.uid);
```

The rowData object also contains all the form fields that were added during the DataGrid configuration.

```javascript
appPage.F_SelectedName.setValue(rowData.F_Name);
```

**Sample rowData object**

```json
{ 
    editUrl: "https://...", 
    viewUrl: "https://...", 
    printUrl: "https://...", 
    uid: "f308d85b-9bd6-449f-87b7-b09ea27fa23c", 
    id: "F054B58209264E008825872700748692", 
    stageId: "ST_Submitted", 
    stageTitle: "Submitted", 
    lastModified: Date obj, 
    lastModifiedBy: { 
        displayName: "Daisy Dixon/Acme", 
        email: "Daisy Dixon/Acme", 
        login: "CN=Daisy Dixon/O=Acme" 
    } 
    created: Date obj, 
    createdBy: { 
        displayName: "Daisy Dixon/Acme", 
        email: "Daisy Dixon/Acme", 
        login: "CN=Daisy Dixon/O=Acme" 
    }, 
    F_SingleLine1: "hello world", 
    F_EmailAddress1: "test@example.com", 
    F_Number1: 56.89, 
    F_Currency1: 12.34, 
    F_CheckBox1: true, 
    F_RichText1: "<p>this is some <span style=\"color:#2980b9\"><span style=\"font-size:18px\"><strong>rich </strong></span></span>text</p>", 
    F_DropDown1: {savedValue: "opt1", displayValue: "Option 1"}, 
    F_SelectMany1: [ 
        {savedValue: "opt1", displayValue: "Option 1"}, 
        {savedValue: "opt2", displayValue: "Option 2"} 
    ], 
    F_Attachment1: { 
        uid: "abc123", 
        fileName: "MyFile.png", 
        viewUrl: "https://...", 
        downloadUrl: "https://..."  
    }, 
    F_Name1 { 
        displayName: "Doug D'Antonio", 
        id: "CN=Doug D'Antonio/O=Acme", 
        email: "Doug D'Antonio/Acme", 
        type: "user" 
    } 
}; 
```

### onShow

This event is invoked after the item is presented (either with the entire form or just this item).


**Parent topic:** [Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

