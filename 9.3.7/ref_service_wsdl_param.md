# WSDL service description tool parameters 

Build a command to expose services for a WSDL based web device.

## Running the WSDL service description tool { .section}

At the command line prompt, type the following command to activate the tool:

```
java -jar serviceDescriptionGenerator.jar -wsdlFile=webService.wsdl
```

In this command,

**serviceDescriptionGenerator.jar**: is the name of the executable .jar file.

**-wsdlFile**:  the command you use if the WSDL file is local.

**webService.wsdl**  is the file name of the WSDL file.

Use the following options to customize the commands for your file:

Table 1. WSDL command optionsSummary of the support commands 

|Command|Description|Note|
|-------|-----------|----|
|-wsdlFile|Specifies the file location of the WSDL file|You must use either this option or the -wsdlUri option in the command you enter|
|-wsdlUri|Specifies the URI of the WSDL file|You must use either this option or the -wsdlFile option in the command you enter.|
|-saveTo|You can specify a location where the generated service descriptions will be created with this command. The default is the current working directory.|Optional|
|-defaultLocale|You can specify the locale used to generate the service description.|Optional|
| | | The default is English.|
|-transformNames|You can convert the service description parameter names to a more readable format. It supports camelCase, underscores and dashes.|Optional|
| | |The default is false.|
| | |The possible values are true or false.|
|-credentialProvider|Adds a credential provider to all generated service description.|The values are basic and cookie.|
|-realm|Use when the credential provider is set to basic.|Optional|
|-cookies|Use when the credential provider is set to cookie.|Optional|
|-log|Set the logging level of messages displayed to the user.|The default is WARNING.|
| | |The possible values are ALL, CONFIG, FINE, FINER, FINEST, INFO, OFF, SEVERE, and WARNING.|
|-help|Displays a quick reference of the commands for the tool.|Optional|

## Schema Data Type Interpretation { .section}

In cases where an element or attribute type is a union of two or more schema data types, the parameter type will be set to string.

The schema data type `xsd:anyType` is valid schema data type. However, there is no equivalent parameter type for it. Therefore, the tool is unable to create the equivalent parameter for any elements and attributes with this type.

A parameter type depends on its schema data type. The following table lists the equivalent schema data types for a given parameter type.

Table 2. Schema data types and its equivalent service parameter data type 

<table class="table-wrap">
<tr>
<td><b>Service Description Parameter Type</b> </td><td> <b>Schema Data Type</b></td>
</tr>
<tr>
<td>String
<td><ul>
<li> string></li>
<li> gYearMonth</li>
<li> gMonthDay</li>
<li> gYear</li>
<li> gDay</li>
<li> gMonth</li>
<li> hexBinary</li>
<li> base64Binary</li>
<li> anyURI</li>
<li> QName</li>
<li> NOTATION</li>
<li> normalizedString</li>
<li> token</li>
<li> language</li>
<li> Name</li>
<li> NMTOKEN</li>
<li> NCName</li>
<li> NMTOKENS</li>
<li> ID</li>
<li> IDREF</li>
<li> ENTITY</li>
</ul>
</tr>
<tr>
<td>Integer
<td><ul>
<li> integer</li>
<li> nonPositiveInteger</li>
<li> long</li>
<li> nonNegativeInteger</li>
<li> negativeInteger</li>
<li> int</li>
<li> short</li>
<li> byte</li>
<li> unsignedLong</li>
<li> postiveInteger</li>
<li> unsignedInt</li>
<li> unsignedShort</li>
<li> unsignedByte</li>
</ul>
</tr>
<tr>
<td>Boolean
<td>Boolean
</tr>
<tr>
<td>Decimal
<td>Decimal
</tr>
<tr>
<td>Float
<td>|Float
</tr>
<tr>
<td>Double
<td>Double
</tr>
<tr>
<td>Duration
<td>Duration
</tr>
<tr>
<td>DateTime
<td>DateTime
</tr>
<tr>
<td>Time
<td>Time
</tr>
<tr>
<td>Date
<td>Date
</tr>
</table>

The parameter description contains any restrictions of an element or attribute. The description contains the schema data type, all restrictions and all values of each restriction.

**Parent topic: **[Using the service description tool for WSDL web service](ref_service_wsdl_ovr.md)

