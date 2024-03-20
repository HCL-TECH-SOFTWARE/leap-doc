# Data objects {#dataobjects .reference}

This topic describes and gives samples for data objects used within the HCL Leap JavaScript™ API.

Table 1. Business Object (BO)

*The object that contains all the data for an instance of a form.*

|Object|Description|Example|
|------|-----------|-------|
|BO.<itemId\>|Accesses the Business Object Attribute data for an individual item on the form.|Set the value of a number item on the form: <br> `BO.F_Age.setValue(12);`|
|BO.setValid\(valid, msg\)|Setting **valid** to “false” overrides the validity of the form and prevents submission, showing the user the message provided. Setting **valid** to “true” removes any previous override. However, it will not override other ways in which the form might be invalid.|Place this code in the **onItemChange** event of a field to constrain the input to a specific value. <br><br> if(BOA.getValue() < 15 &#124;&#124; BOA.getValue() > 35) { BOA.setValid(false, "The age must be between 16 and 35");}|
|BO.getValid\(\)|Returns the current value of the overridden valid state of the form as set by **BO.setValid\(\)**.| |
|BO.isValid\(\)|Returns true if every field in the form is valid and false otherwise. This is different from getValid\(\) which returns the overridden valid state of the form as set by **BO.setValid\(\).**| |
|BO.getInvalidMessages\(\)|This function returns an array of the error messages of any invalid fields in the form. If there are no invalid fields, the function returns an empty array.| |
|BO.getCurrentStage\(\)|Returns the current stage of the form.|If the form is in the Submitted stage then show the user a custom message in the **onLoad**: <br> <code> if(BO.getCurrentStage() === 'ST_Submitted') <br> alert('Reminder: This form is complete and cannot be modified'); </code>|
|BO.getDataId\(\)|Returns the unique ID that represents this data item or will represent it if it has never been submitted.| |
|BO.getChildren\(\)|Returns a list object that provides access to all the individual Business Object Attribute data. The list object has getLength\(\) function, and get\(index\) function for accessing the objects in the list.| |

Table 2. Business Object Attribute

*The object that contains the individual data mapped to items on the form.*

|Object|Description|Example|
|------|-----------|-------|
|BOA.getValue\(\)|Returns the current value. The type of the returned value depends on the type of item. <br> -   Boolean: Checkbox <br> -   Number : Number, Currency, Numeric Slider <br> -   Date: Date, Time, Timestamp <br> -   Object: Attachment <br> -   Multi-Value String: Select Many, Survey Question \(when "Allow selection of multiple values" checked\). Values will be delimited with "\_\_\#\_\_" <br> -   String: All other items|<code> var s = ""; //string <br> s = BO.F_SingleLine1.getValue(); <br> s = BO.F_Paragraph1.getValue(); <br><br> var n = 0; //number or currency <br> n = BO.F_Number1.getValue(); <br> n = BO.F_Currency1.getValue(); <br><br> var d = new Date(); //date or timestamp <br> d = BO.F_Date1.getValue(); <br> d = BO.F_TimeStamp1.getValue(); <br><br> var b = false; //boolean <br> b = BO.F_CheckBox1.getValue(); <br><br> var o = null; //object <br> o = BO.F_Attachment1.getValue(); <br> alert("ID: " + o.id + ", filename: " + o.fileName + ", uid: " + o.uid);</code>|
|BOA.setValue\(value\)|Sets the value of this data item. The correct data type should be provided based on the Business Object Attribute’s type. Some type conversion is done where possible, for example, a Number converted to a String. <br><br> **Note:** The attachment data takes an object with a uid property, an id property, and a filename property. Modifying attachment data is not recommended in most circumstances.|<code> //string <br> BO.F_SingleLine1.setValue("Sample String"); <br> BO.F_Paragraph1.setValue("Sample String"); <br><br> //number or currency <br> BO.F_Number1.setValue(25); <br> BO.F_Currency1.setValue(123.65); <br><br> //date or timestamp <br> BO.F_Date1.setValue(new Date()); <br> BO.F_TimeStamp1.setValue(new Date()); <br><br> //boolean <br> BO.F_CheckBox1.setValue(true); <br><br> //object <br> BO.F_Attachment1.setValue({uid: 'ccb92c12-d435-4288-baff-878d8d3c2923', id: '25', fileName: 'myfile.txt'}); </code>|
|BOA.getId\(\)|Returns the ID of this data item that is unique per form.| |
|BOA.getBO\(\)|Returns the Business Object for the entire form.| |
|BOA.getType\(\)|Returns a string that indicates the type of data. For example, string, number, boolean, currency, time, date, timeStamp, or attachment.| |
|BOA.connectEvent\(eventName, callbackFunction\)|Used for connecting an event listener to a Business Object Attribute. You can define code to execute when the listener detects that the event is triggered. The only supported event for a Business Object Attribute is **onChange**. <br><br> **Note:** If you connect an event, it must be disconnected using BOA.disconnectEvent\(eventHandle\).|Place this in the **onShow** event of the field to display a message box when the item changes. <br> <code> var hdl = BOA.connectEvent("onChange", function(newValue) <br> { <br> alert("Field content is " + newValue); <br> BOA.disconnectEvent(hdl); <br> }); </code>|
|BOA.disconnectEvent\(eventHandle\)|Disconnects the event handler specified by the passed-in event handle object that was returned by a BOA.connectEvent call. If you create a listener in the event of a form object, you must disconnect it. Otherwise, duplicate listeners are created every time the event is triggered.|<code>var hdl = BOA.connectEvent("onChange", function (newValue) <br> { <br> alert("Field content is " + newValue); <br> BOA.disconnectEvent(hdl); <br> });</code>|
|BOA.setValid\(valid, msg\)|You can override valid data to be invalid with this method. By passing “false”, you cause the data to be invalid, and prevent submission. You can optionally provide a custom error message. Setting the valid to “true” clears any previously overridden valid value. <br><br> **Note:** You cannot set a Business Object Attribute to valid which actually has invalid data, or is set invalid by a rule.|Force the user to enter more than 3 characters for their name by adding this code to the items onItemChange: <br> <code>if(BOA.getValue().length < 3) <br> BOA.setValid(false, 'Name must be at least 3 characters'); <br> else BOA.setValid(true);</code>|
|BOA.getValid\(\)|Gets a value set previously using setValid\(\).| |
|BOA.setRequired\(required\)|You can override non-required data to be required with this method. By passing “true”, you cause its data to be required and prevent submission if it is not set. Setting the valid to “false” clears any previously overridden value. <br><br> **Note:** If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it unrequired.| |
|BOA.getRequired\(\)|Gets a value set previously using setRequired\(\).| |
|BOA.isValid\(\)|Returns true if the data is valid. Returns false if the data is invalid.| |
|BOA.getInvalidMessage\(\)|Returns the current error messages for this data, or null if the data is valid.| |
|BOA.isRequired\(\)|Returns true if this item is required.| |
|BOA.isMissing\(\)|Returns true if this item is required and it has no value.| |
|BOA.validate\(\)|Triggers the validation of the data item.| |

Table 3. Business Object List for lists of Business Objects

*This object contains a list of Business Objects. It provides data to Table items rather than the standard Business Object Attribute. Each entry in the table corresponds to a Business Object in the list.*

|Object|Description|
|------|-----------|
|BOL.getLength\(\)|Returns the number of Business Objects in the list.|
|BOL.get\(index\)|Returns the Business Object at the specified index.|
|BOL.createNew\(\)|Creates a new empty Business Object ready to be inserted into the list using the add\(\) method.|
|BOL.add\(bo\)|Adds a Business Object of the appropriate type to the list. Can be one created with a call to the createNew\(\) method or removed from the list with a remove\(\) call.|
|BOL.remove\(bo\)|Removes the Business Object from the list. Returns true if successful, false if not.|
|BOL.getId\(\)|Returns the ID of this data item that is unique per form.|
|BOL.getType\(\)|Returns a string that indicates the type of Business Object List data.|
|BOL.setValid\(valid, msg\)|You can override valid data to be invalid with this method. By passing false, you cause its data to be invalid and prevent submission. You can optionally provide a custom error message. Setting valid to true clears any previously overridden valid value. <br><br> **Note:** You cannot set a Business Object List to valid that actually has invalid data, or is set invalid by a rule.|
|BOL.getValid\(\)|Gets a value set previously using setValid\(\).|
|BOL.setRequired\(required\)|You can override non-required data to be required with this method. By passing true, you cause its data to be required and prevent submission if it is not set. Setting the valid to false clears any previously overridden value. <br><br> **Note:** If a Business Object Attribute has been set as required by a property or by a Rule, you cannot make it unrequired.|
|BOL.getRequired\(\)|Gets a value set previously using setRequired\(\).|

**Parent topic:** [Reference Objects and Functions](ref_jsapi_objects_and_functions.md)

