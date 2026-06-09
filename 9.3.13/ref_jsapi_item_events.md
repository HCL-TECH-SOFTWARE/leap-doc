# Item Events 

This topic describes the Item Events, and their parameters when using JavaScript™ API in {{fullProductName}}.

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


## beforeOptionsUpdate

This event is called before the options in a drop-down list are updated from a service call or from an API call. The array of options is passed in as pOptions and can be modified by the event code. By default, when a new options list is set into a drop-down list and the current selected item is not in the new list, it is added into the new list automatically. If you return false from this event, it does not copy the missing option into the new list.

**Example**

```javascript
pOptions.push({title:'Pizza', value:'fooditem3'});
return false;
```

**Parent topic:** [Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

