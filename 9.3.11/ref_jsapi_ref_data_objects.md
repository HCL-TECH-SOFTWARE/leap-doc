# Data objects { #dataobjects .reference }

This topic describes and gives samples for data objects used within the {{fullProductName}} JavaScript™ API.

## Business Object (BO)

The object that contains all the data for an instance of a form.

### BO.&lt;itemId&gt;

Accesses the Business Object Attribute data for an individual item on the form.

**Syntax**
```javascript
BO.itemId
```

**Example**

Set the value of a number item on the form:
```javascript
BO.F_Age.setValue(12);
```


### getChildren

Returns a list object that provides access to all the individual Business Object Attribute data. The list object has getLength() function, and get(index) function for accessing the objects in the list.

**Syntax**
```javascript
BO.getChildren()
```


### getCurrentStage

Returns the current stage of the form.

**Syntax**
```javascript
BO.getCurrentStage()
```

**Example**

If the form is in the Submitted stage then show the user a custom message in the **onLoad**:

```javascript
if(BO.getCurrentStage() === 'ST_Submitted')
    alert('Reminder: This form is complete and cannot be modified');
```


### getDataId

Returns the unique ID that represents this data item or will represent it if it has never been submitted.

**Syntax**
```javascript
BO.getDataId()
```


### getInvalidMessages

This function returns an array of the error messages of any invalid fields in the form. If there are no invalid fields, the function returns an empty array.

**Syntax**
```javascript
BO.getInvalidMessages()
```


### getValid

Returns the current value of the overridden valid state of the form as set by **BO.setValid()**.

**Syntax**
```javascript
BO.getValid()
```


### isValid

Returns true if every field in the form is valid and false otherwise. This is different from getValid() which returns the overridden valid state of the form as set by **BO.setValid().**

**Syntax**
```javascript
BO.isValid()
```


### setValid

Changes the valid state of the object.

Setting **valid** to "false" overrides the validity of the form and prevents submission, showing the user the message provided. 

Setting **valid** to "true" removes any previous override. However, it will not override other ways in which the form might be invalid.

**Syntax**
```javascript
BO.setValid(valid, msg)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| valid | True or false. |
| msg | A string message to display when invalid |

**Example**

Place this code in the **onItemChange** event of a field to constrain the input to a specific value.

```javascript
if(BOA.getValue() < 15 || BOA.getValue() > 35) {
  BOA.setValid(false, "The age must be between 16 and 35");
}
```


## Business Object Attribute (BOA)

The object that contains the individual data mapped to items on the form.  'BOA' will return the business object for the item in scope where this is used.


### connectEvent

Used for connecting an event listener to a Business Object Attribute. You can define code to execute when the listener detects that the event is triggered. The only supported event for a Business Object Attribute is **onChange**.

!!! note
    If you connect an event, it must be disconnected using BOA.disconnectEvent(eventHandle).

**Syntax**
```javascript
BOA.connectEvent (eventName, callbackFunction)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| eventName     | Only supported event is 'onChange' |
| callbackFunction | A function that is executed based on the service eventName |

**Example**

Place this in the **onShow** event of the field to display a message box when the item changes.
```javascript
var hdl = BOA.connectEvent("onChange", function(newValue)
{
   alert("Field content is " + newValue);
   BOA.disconnectEvent(hdl);
});
```


### disconnectEvent

Disconnects the event handler specified by the passed-in event handle object that was returned by a BOA.connectEvent call. 

If you create a listener in the event of a form object, you must disconnect it. Otherwise, duplicate listeners are created every time the event is triggered.

**Syntax**
```javascript
BOA.disconnectEvent (eventHandle)
```

**Example**
```javascript
var hdl = BOA.connectEvent("onChange", function (newValue)
{
   alert("Field content is " + newValue);
   BOA.disconnectEvent(hdl);
});
```


### getBO

Returns the Business Object for the entire form.

**Syntax**
```javascript
BOA.getBO()
```


### getId

Returns the ID of this data item that is unique per form.

**Syntax**
```javascript
BOA.getId()
```


### getInvalidMessage

Returns the current error messages for this data, or null if the data is valid.

**Syntax**
```javascript
BOA.getInvalidMessage()
```


### getRequired

Gets a value set previously using setRequired().

**Syntax**
```javascript
BOA.getRequired()
```


### getType

Returns a string that indicates the type of data. For example, string, number, boolean, currency, time, date, timeStamp, or attachment.

**Syntax**
```javascript
BOA.getType()
```

### getValid

Gets a value set previously using setValid().

**Syntax**
```javascript
BOA.getValid()
```


### getValue

Returns the current value. The type of the returned value depends on the type of item.
   - Boolean: Checkbox
   - Number : Number, Currency, Numeric Slider
   - Date: Date, Time, Timestamp
   - Object: Attachment
   - Multi-Value String: Select Many, Survey Question (when "Allow selection of multiple values" checked). Values will be delimited with "__#__"
   - String: All other items


**Syntax**
```javascript
BOA.getValue()
```

**Example**

In the **onItemChange** event of 'F_SingleLine1' you could write the following to get its value
```javascript

BOA.getValue()
```

Other ways to get the same value:
```javascript
// app level scope
app.getForm('F_Form1').getBO().F_SingleLine1.getValue();

// form level scope
form.getBO().F_SingleLine1.getValue();

// page level scope
page.F_SingleLine1.getValue();
```


### isMissing

Returns true if this item is required and it has no value.

**Syntax**
```javascript
BOA.isMissing()
```


### isRequired

Returns true if this item is required.

**Syntax**
```javascript
BOA.isRequired()
```

### isValid

Returns true if the data is valid. Returns false if the data is invalid.

**Syntax**
```javascript
BOA.isValid()
```


### setRequired

You can override non-required data to be required with this method. By passing "true", you cause its data to be required and prevent submission if it is not set. Setting the valid to "false" clears any previously overridden value.

!!! note
    If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it "unrequired".

**Syntax**
```javascript
BOA.setRequired(required)
```


### setValid

You can override valid data to be invalid with this method. By passing "false", you cause the data to be invalid, and prevent submission. You can optionally provide a custom error message. Setting the valid to "true" clears any previously overridden valid value.

!!! note
    You cannot set a Business Object Attribute to valid which actually has invalid data, or is set invalid by a rule.

**Syntax**
```javascript
BOA.setValid(valid, msg)
```

**Example**

Force the user to enter more than 3 characters for their name by adding this code to the items **onItemChange**:
```javascript
if(BOA.getValue().length < 3)
   BOA.setValid(false, 'Name must be at least 3 characters');
else 
   BOA.setValid(true);
```


### setValue

Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String.

!!! note
    The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.

**Syntax**
```javascript
BOA.setValue(value)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| value | Value to set based on datatype of the item |

**Example**
```javascript
//string
BO.F_SingleLine1.setValue("Sample String");
BO.F_Paragraph1.setValue("Sample String");

//number or currency
BO.F_Number1.setValue(25);
BO.F_Currency1.setValue(123.65);

//date or timestamp
BO.F_Date1.setValue(new Date());
BO.F_TimeStamp1.setValue(new Date());

//boolean
BO.F_CheckBox1.setValue(true);

//object
BO.F_Attachment1.setValue({uid: 'ccb92c12-d435-4288-baff-878d8d3c2923', id: '25', fileName: 'myfile.txt'}); 
```


### validate

Triggers the validation of the data item.

**Syntax**
```javascript
BOA.validate()
```


## Business Object List for lists of Business Objects

This object contains a list of Business Objects. It provides data to Table items rather than the standard Business Object Attribute. Each entry in the table corresponds to a Business Object in the list.

### add

Adds a Business Object of the appropriate type to the list. Can be one created with a call to the createNew() method or removed from the list with a remove() call.

**Syntax**
```javascript
BOL.add(bo)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| bo     | The business object for the row |


**Example**
```javascript
var tbl = BO.F_Table1;
var tmpRow = tbl.createNew();
tmpRow.F_SingleLine1.setValue("1");
tbl.add(tmpRow);
```


### createNew

Creates a new empty Business Object ready to be inserted into the list using the add() method.

**Syntax**
```javascript
BOL.createNew()
```

**Example**
```javascript
var tbl = BO.F_Table1;
var tmpRow = tbl.createNew();
tmpRow.F_SingleLine1.setValue("1");
tbl.add(tmpRow);
```

### get

Returns the Business Object at the specified index.

**Syntax**
```javascript
BOL.get(index)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| index     | The index of the BO in this list.  Starting at 0. |


### getById

Returns the Business Object with the given ID

**Syntax**
```javascript
BOL.getById(boId)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| boId     | The ID of the BO in this list. |


### getId

Returns the ID of this data item that is unique per form.

**Syntax**
```javascript
BOL.getId()
```


### getLength

Returns the number of Business Objects in the list.

**Syntax**
```javascript
BOL.getLength()
```


### getRequired

Gets a value set previously using setRequired().

**Syntax**
```javascript
BOL.getRequired()
```


### getType

Returns a string that indicates the type of Business Object List data.

**Syntax**
```javascript
BOL.getType()
```


### getValid

Gets a value set previously using setValid().

**Syntax**
```javascript
BOL.getValid()
```


### remove

Removes the Business Object from the list. Returns true if successful, false if not.

**Syntax**
```javascript
BOL.remove(bo)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| bo     | The business object for the row |


### setRequired

You can override non-required data to be required with this method. By passing true, you cause its data to be required and prevent submission if it is not set. Setting the valid to false clears any previously overridden value.<br>

!!! note
    If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it "unrequired".

**Syntax**
```javascript
BOL.setRequired(required)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| required     | True or False |


### setValid

You can override valid data to be invalid with this method. By passing false, you cause its data to be invalid and prevent submission. You can optionally provide a custom error message. Setting valid to true clears any previously overridden valid value.

!!! note
    You cannot set a Business Object List to valid that actually has invalid data, or is set invalid by a rule.

**Syntax**
```javascript
BOL.setValid(valid, msg)
```

**Parameters**

| Parameter     | Description |
| :------------ | :---------- |
| valid     | True or False. |
| msg | A message to display if the object is invalid |


**Parent topic:** [Reference Objects and Functions](ref_jsapi_objects_and_functions.md)
