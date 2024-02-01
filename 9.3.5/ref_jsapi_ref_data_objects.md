# Data objects {#dataobjects .reference}

This topic describes and gives samples for data objects used within the HCL Leap JavaScript™ API.

|Object|Description|Example|
|------|-----------|-------|
|BO.<itemId\>|Accesses the Business Object Attribute data for an individual item on the form.|Set the value of a number item on the form:```
BO.F_Age.setValue(12);
```

|
|BO.setValid\(valid, msg\)|Setting **valid** to “false” overrides the validity of the form and prevents submission, showing the user the message provided. Setting **valid** to “true” removes any previous override. However, it will not override other ways in which the form might be invalid.|Place this code in the **onItemChange** event of a field to constrain the input to a specific value.```
if(BOA.getValue() < 15 || BOA.getValue() > 35) {
    BOA.setValid(false, "The age must be between 16 and 35");
}
```

|
|BO.getValid\(\)|Returns the current value of the overridden valid state of the form as set by **BO.setValid\(\)**.| |
|BO.isValid\(\)

|Returns true if every field in the form is valid and false otherwise. This is different from getValid\(\) which returns the overridden valid state of the form as set by **BO.setValid\(\).**

| |
|BO.getInvalidMessages\(\)

|This function returns an array of the error messages of any invalid fields in the form. If there are no invalid fields, the function returns an empty array.| |
|BO.getCurrentStage\(\)|Returns the current stage of the form.|If the form is in the Submitted stage then show the user a custom message in the **onLoad**:```
if(BO.getCurrentStage() === 'ST_Submitted')
    alert('Reminder: This form is complete and cannot be 
modified');
```

|
|BO.getDataId\(\)|Returns the unique ID that represents this data item or will represent it if it has never been submitted.| |
|BO.getChildren\(\)|Returns a list object that provides access to all the individual Business Object Attribute data. The list object has getLength\(\) function, and get\(index\) function for accessing the objects in the list.| |

|Object|Description|Example|
|------|-----------|-------|
|BOA.getValue\(\)|Returns the current value. The type of the returned value depends on the type of item. -   Boolean: Checkbox
-   Number : Number, Currency, Numeric Slider
-   Date: Date, Time, Timestamp
-   Object: Attachment
-   Multi-Value String: Select Many, Survey Question \(when "Allow selection of multiple values" checked\). Values will be delimited with "\_\_\#\_\_"
-   String: All other items

|```
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

|
|BOA.setValue\(value\)|Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String. **Note:** The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.

|```
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

|
|BOA.getId\(\)|Returns the ID of this data item that is unique per form.| |
|BOA.getBO\(\)|Returns the Business Object for the entire form.| |
|BOA.getType\(\)|Returns a string that indicates the type of data. For example, string, number, boolean, currency, time, date, timeStamp, or attachment.| |
|BOA.connectEvent\(eventName, callbackFunction\)|Used for connecting an event listener to a Business Object Attribute. You can define code to execute when the listener detects that the event is triggered. The only supported event for a Business Object Attribute is **onChange**.**Note:** If you connect an event, it must be disconnected using BOA.disconnectEvent\(eventHandle\).

|Place this in the **onShow** event of the field to display a message box when the item changes.```
var hdl = BOA.connectEvent("onChange", function(newValue)
{
      alert("Field content is " + newValue);
      BOA.disconnectEvent(hdl);
});
```

|
|BOA.disconnectEvent\(eventHandle\)|Disconnects the event handler specified by the passed-in event handle object that was returned by a BOA.connectEvent call. If you create a listener in the event of a form object, you must disconnect it. Otherwise, duplicate listeners are created every time the event is triggered.|```
var hdl = BOA.connectEvent("onChange", function (newValue)
{
      alert("Field content is " + newValue);
      BOA.disconnectEvent(hdl);
});
```

|
|BOA.setValid\(valid, msg\)|You can override valid data to be invalid with this method. By passing “false”, you cause the data to be invalid, and prevent submission. You can optionally provide a custom error message. Setting the valid to “true” clears any previously overridden valid value.**Note:** You cannot set a Business Object Attribute to valid which actually has invalid data, or is set invalid by a rule.

|Force the user to enter more than 3 characters for their name by adding this code to the items onItemChange:```
	if(BOA.getValue().length < 3)
		BOA.setValid(false, 'Name must be at least 3 characters');
	else BOA.setValid(true);
```

|
|BOA.getValid\(\)|Gets a value set previously using setValid\(\).| |
|BOA.setRequired\(required\)|You can override non-required data to be required with this method. By passing “true”, you cause its data to be required and prevent submission if it is not set. Setting the valid to “false” clears any previously overridden value.**Note:** If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it unrequired.

| |
|BOA.getRequired\(\)|Gets a value set previously using setRequired\(\).| |
|BOA.isValid\(\)|Returns true if the data is valid. Returns false if the data is invalid.| |
|BOA.getInvalidMessage\(\)|Returns the current error messages for this data, or null if the data is valid.| |
|BOA.isRequired\(\)|Returns true if this item is required.| |
|BOA.isMissing\(\)|Returns true if this item is required and it has no value.| |
|BOA.validate\(\)|Triggers the validation of the data item.| |

|Object|Description|
|------|-----------|
|BOL.getLength\(\)|Returns the number of Business Objects in the list.|
|BOL.get\(index\)|Returns the Business Object at the specified index.|
|BOL.createNew\(\)|Creates a new empty Business Object ready to be inserted into the list using the add\(\) method.|
|BOL.add\(bo\)|Adds a Business Object of the appropriate type to the list. Can be one created with a call to the createNew\(\) method or removed from the list with a remove\(\) call.|
|BOL.remove\(bo\)|Removes the Business Object from the list. Returns true if successful, false if not.|
|BOL.getId\(\)|Returns the ID of this data item that is unique per form.|
|BOL.getType\(\)|Returns a string that indicates the type of Business Object List data.|
|BOL.setValid\(valid, msg\)|You can override valid data to be invalid with this method. By passing false, you cause its data to be invalid and prevent submission. You can optionally provide a custom error message. Setting valid to true clears any previously overridden valid value. **Note:** You cannot set a Business Object List to valid that actually has invalid data, or is set invalid by a rule.

|
|BOL.getValid\(\)|Gets a value set previously using setValid\(\).|
|BOL.setRequired\(required\)|You can override non-required data to be required with this method. By passing true, you cause its data to be required and prevent submission if it is not set. Setting the valid to false clears any previously overridden value. **Note:** If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it unrequired.

|
|BOL.getRequired\(\)|Gets a value set previously using setRequired\(\).|

**Parent topic: **[Reference Objects and Functions](ref_jsapi_objects_and_functions.md)

