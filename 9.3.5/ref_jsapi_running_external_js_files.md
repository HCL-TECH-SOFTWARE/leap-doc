# Running Custom JavaScript Files 

Custom JavaScript™ can also be loaded from attached JavaScript files. Any .js file that is added to the application in the **Settings** \> **Files** section is automatically loaded into your running application. An associated JavaScript file is evaluated once when the browser first loads the running application, and is not called in response to any events.

Table 1. JavaScript™ objects available in attached JavaScript™ files

<table>
<tr>
<td> <b>Variable</b> </td><td> <b>Full name</b> <td><b>Description</b></td> <td> <b>Example</b></td> <td> <b>Type</b>
</tr>
<tr>
<td>app
<td>Application object
<td>Contains functions for accessing global general information
<td>   A common use case for external .js files is utility methods to be executed later in events by custom JavaScript. One example is a function to sum up all Number values in a section:<br>

```javascript
app.getSharedData().sumNumbers = function(section)
{
	var total = 0;
	var children = section.getChildren();
	for(var i=0; i<children.getLength(); i++)
	{
		var child = children.get(i);
		if(child.getType() === 'number')
			total += child.getBOAttr().getValue();
	}
	return total;
};
```
<br>
<br>
<br>
Then from an event where you want to sum all numbers in a section:<br>
<br>

```javascript   
var sub = app.getSharedData().sumNumbers(page.F_Expense);
```
   

<td>GUI
</tr>
</table>

<br>
<br>

When JavaScript security is enabled: For added security, external JavaScript files that are referenced by URL do not load into the running application. Uploaded JavaScript files are evaluated in a safe sandbox and all content must adhere to the restrictions of the sandbox. See [JavaScript Security](ref_jsapi_javascript_security.md#) for more details. For example, functions must be defined by using the following format: `app.getSharedData().blat = function (...) { ... }`

When JavaScript security is disabled: External JavaScript files that are referenced by URL are loaded by using a `<script>` tag and does not have access to the app variable. These scripts must use `window.NitroApplication` to access the Leap API functions. JavaScript files that are uploaded to the application are evaluated by using the `eval()` function.

**Parent topic:** [JavaScript API](ref_javascript_api.md)

