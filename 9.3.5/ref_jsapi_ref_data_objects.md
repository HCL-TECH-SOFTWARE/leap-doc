# Data objects {#dataobjects .reference}

This topic describes and gives samples for data objects used within the HCL Leap JavaScript™ API.

Table 1. Business Object (BO)<br>
The object that contains all the data for an instance of a form.
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
<th>Example
</thead>

<tr>
<td>BO.&lt;itemId&gt;
<td>Accesses the Business Object Attribute data for an individual item on the form.
<td>Set the value of a number item on the form:
```javascript
BO.F_Age.setValue(12);
```
<tr>
<td>BO.setValid(valid, msg)
<td>Setting <b>valid</b> to "false" overrides the validity of the form and prevents submission, showing the user the message provided. Setting <b>valid</b> to "true" removes any previous override. However, it will not override other ways in which the form might be invalid.
<td>Place this code in the <b>onItemChange</b> event of a field to constrain the input to a specific value.
```javascript
if(BOA.getValue() < 15 || BOA.getValue() > 35) {
  BOA.setValid(false, "The age must be between 16 and 35");
}
```
<tr>
<td>BO.getValid()
<td>Returns the current value of the overridden valid state of the form as set by <b>BO.setValid()</b>.
<td>

<tr>
<td>BO.isValid()
<td>Returns true if every field in the form is valid and false otherwise. This is different from getValid() which returns the overridden valid state of the form as set by <b>BO.setValid().</b>
<td>

<tr>
<td>BO.getInvalidMessages()
<td>This function returns an array of the error messages of any invalid fields in the form. If there are no invalid fields, the function returns an empty array.
<td>

<tr>
<td>BO.getCurrentStage()
<td>Returns the current stage of the form.
<td>If the form is in the Submitted stage then show the user a custom message in the <b>onLoad</b>:
```javascript
if(BO.getCurrentStage() === 'ST_Submitted')
    alert('Reminder: This form is complete and cannot be modified');
```

<tr>
<td>BO.getDataId()
<td>Returns the unique ID that represents this data item or will represent it if it has never been submitted.
<td>

<tr>
<td>BO.getChildren()
<td>Returns a list object that provides access to all the individual Business Object Attribute data. The list object has getLength() function, and get(index) function for accessing the objects in the list.
<td>
</table>

Table 2. Business Object Attribute<br>
The object that contains the individual data mapped to items on the form.
<table class="table-wrap">
<thead>
<th width="200">Object
<td>Description
<th>Example
</thead>

<tr>
<td>BOA.getValue()
<td>Returns the current value. The type of the returned value depends on the type of item.
<ul>
    <li>Boolean: Checkbox
    <li>Number : Number, Currency, Numeric Slider
    <li>Date: Date, Time, Timestamp
    <li>Object: Attachment
    <li>Multi-Value String: Select Many, Survey Question (when "Allow selection of multiple values" checked). Values will be delimited with "__#__"
    <li>String: All other items
</ul>
<td>
```javascript
var s = ""; //string
s = BO.F_SingleLine1.getValue();
s = BO.F_Paragraph1.getValue();

var n = 0; //number or currency
n = BO.F_Number1.getValue();
n = BO.F_Currency1.getValue();

var d = new Date(); //date or timestamp
d = BO.F_Date1.getValue();
d = BO.F_TimeStamp1.getValue();

var b = false; //boolean
b = BO.F_CheckBox1.getValue();

var o = null; //object
o = BO.F_Attachment1.getValue();
alert("ID: " + o.id + ", filename: " + o.fileName + ", uid: " + o.uid);
```

<tr>
<td>BOA.setValue(value)
<td>Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String.<br>
<br>
<b>Note:</b> The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.
<td>
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

<tr>
<td>BOA.getId()
<td>Returns the ID of this data item that is unique per form.
<td>

<tr>
<td>BOA.getBO()
<td>Returns the Business Object for the entire form.
<td>

<tr>
<td>BOA.getType()
<td>Returns a string that indicates the type of data. For example, string, number, boolean, currency, time, date, timeStamp, or attachment.
<td>

<tr>
<td>BOA.connectEvent (eventName, callbackFunction)
<td>Used for connecting an event listener to a Business Object Attribute. You can define code to execute when the listener detects that the event is triggered. The only supported event for a Business Object Attribute is <b>onChange</b>.<br>
<br>
<b>Note:</b> If you connect an event, it must be disconnected using BOA.disconnectEvent(eventHandle).

<td>Place this in the <b>onShow</b> event of the field to display a message box when the item changes.
```javascript
var hdl = BOA.connectEvent("onChange", function(newValue)
{
   alert("Field content is " + newValue);
   BOA.disconnectEvent(hdl);
});
```

<tr>
<td>BOA.disconnectEvent (eventHandle)
<td>Disconnects the event handler specified by the passed-in event handle object that was returned by a BOA.connectEvent call. If you create a listener in the event of a form object, you must disconnect it. Otherwise, duplicate listeners are created every time the event is triggered.
<td>
```javascript
var hdl = BOA.connectEvent("onChange", function (newValue)
{
   alert("Field content is " + newValue);
   BOA.disconnectEvent(hdl);
});
```

<tr>
<td>BOA.setValid(valid, msg)
<td>You can override valid data to be invalid with this method. By passing "false", you cause the data to be invalid, and prevent submission. You can optionally provide a custom error message. Setting the valid to "true" clears any previously overridden valid value.<br>
<br>
<b>Note:</b> You cannot set a Business Object Attribute to valid which actually has invalid data, or is set invalid by a rule.

<td>Force the user to enter more than 3 characters for their name by adding this code to the items onItemChange:
```javascript
if(BOA.getValue().length < 3)
   BOA.setValid(false, 'Name must be at least 3 characters');
else 
   BOA.setValid(true);
```

<tr>
<td>BOA.getValid()
<td>Gets a value set previously using setValid().
<td>

<tr>
<td>BOA.setRequired(required)
<td>You can override non-required data to be required with this method. By passing "true", you cause its data to be required and prevent submission if it is not set. Setting the valid to "false" clears any previously overridden value.<br>
<br>
<b>Note:</b> If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it "unrequired".
<td>

<tr>
<td>BOA.getRequired()
<td>Gets a value set previously using setRequired().
<td>

<tr>
<td>BOA.isValid()
<td>Returns true if the data is valid. Returns false if the data is invalid.
<td>

<tr>
<td>BOA.getInvalidMessage()
<td>Returns the current error messages for this data, or null if the data is valid.
<td>

<tr>
<td>BOA.isRequired()
<td>Returns true if this item is required.
<td>

<tr>
<td>BOA.isMissing()
<td>Returns true if this item is required and it has no value.
<td>

<tr>
<td>BOA.validate()
<td>Triggers the validation of the data item.
<td>
</table>


Table 3. Business Object List for lists of Business Objects<br>
This object contains a list of Business Objects. It provides data to Table items rather than the standard Business Object Attribute. Each entry in the table corresponds to a Business Object in the list.
<table class="table-wrap">
<thead>
<th width="200">Object
<th>Description
</thead>

<tr>
<td>BOL.getLength()
<td>Returns the number of Business Objects in the list.

<tr>
<td>BOL.get(index)
<td>Returns the Business Object at the specified index.

<tr>
<td>BOL.createNew()
<td>Creates a new empty Business Object ready to be inserted into the list using the add() method.

<tr>
<td>BOL.add(bo)
<td>Adds a Business Object of the appropriate type to the list. Can be one created with a call to the createNew() method or removed from the list with a remove() call.

<tr>
<td>BOL.remove(bo)
<td>Removes the Business Object from the list. Returns true if successful, false if not.

<tr>
<td>BOL.getId()
<td>Returns the ID of this data item that is unique per form.

<tr>
<td>BOL.getType()
<td>Returns a string that indicates the type of Business Object List data.

<tr>
<td>BOL.setValid(valid, msg)
<td>You can override valid data to be invalid with this method. By passing false, you cause its data to be invalid and prevent submission. You can optionally provide a custom error message. Setting valid to true clears any previously overridden valid value.<br>
<br>
<b>Note:</b> You cannot set a Business Object List to valid that actually has invalid data, or is set invalid by a rule.

<tr>
<td>BOL.getValid()
<td>Gets a value set previously using setValid().

<tr>
<td>BOL.setRequired(required)
<td>You can override non-required data to be required with this method. By passing true, you cause its data to be required and prevent submission if it is not set. Setting the valid to false clears any previously overridden value.<br>
<br>
<b>Note:</b> If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it "unrequired".

<tr>
<td>BOL.getRequired()
<td>Gets a value set previously using setRequired().
</table>

**Parent topic: **[Reference Objects and Functions](ref_jsapi_objects_and_functions.md)
