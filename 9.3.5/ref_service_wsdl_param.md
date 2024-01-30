# WSDL service description tool parameters {#wsdlservicedescriptiontoolparameters .reference}

Build a command to expose services for a WSDL based web device.

## Running the WSDL service description tool { .section}

At the command line prompt, type the following command to activate the tool:

```
java -jar serviceDescriptionGenerator.jar -wsdlFile=webService.wsdl
```

In this command,

serviceDescriptionGenerator.jar
:   is the name of the executable .jar file.

-wsdlFile
:   The command you use if the WSDL file is local.

webService.wsdl
:   is the file name of the WSDL file.

Use the following options to customize the commands for your file:

|Command|Description|Note|
|-------|-----------|----|
|-wsdlFile|Specifies the file location of the WSDL file|You must use either this option or the -wsdlUri option in the command you enter|
|-wsdlUri|Specifies the URI of the WSDL file|You must use either this option or the -wsdlFile option in the command you enter.|
|-saveTo|You can specify a location where the generated service descriptions will be created with this command. The default is the current working directory.|Optional|
|-defaultLocale|You can specify the locale used to generate the service description.|Optional

The default is English.|
|-transformNames|You can convert the service description parameter names to a more readable format. It supports camelCase, underscores and dashes.|Optional

The default is false.

The possible values are true or false.

|
|-credentialProvider|Adds a credential provider to all generated service description.|The values are basic and cookie.|
|-realm|Use when the credential provider is set to basic.|Optional|
|-cookies|Use when the credential provider is set to cookie.|Optional|
|-log|Set the logging level of messages displayed to the user.|The default is WARNING.

The possible values are ALL, CONFIG, FINE, FINER, FINEST, INFO, OFF, SEVERE, and WARNING.

|
|-help|Displays a quick reference of the commands for the tool.|Optional|

## Schema Data Type Interpretation { .section}

In cases where an element or attribute type is a union of two or more schema data types, the parameter type will be set to string.

The schema data type `xsd:anyType` is valid schema data type. However, there is no equivalent parameter type for it. Therefore, the tool is unable to create the equivalent parameter for any elements and attributes with this type.

A parameter type depends on its schema data type. The following table lists the equivalent schema data types for a given parameter type.

|Service Description Parameter Type|Schema Data Type|
|----------------------------------|----------------|
|String|-   String
-   gYearMonth
-   gMonthDay
-   gYear
-   gDay
-   gMonth
-   hexBinary
-   base64Binary
-   anyURI
-   QName
-   NOTATION
-   normalizedString
-   token
-   language
-   Name
-   NMTOKEN
-   NCName
-   NMTOKENS
-   ID
-   IDREF
-   ENTITY

|
|Integer|-   integer
-   nonPositiveInteger
-   long
-   nonNegativeInteger
-   negativeInteger
-   int
-   short
-   byte
-   unsignedLong
-   postiveInteger
-   unsignedInt
-   unsignedShort
-   unsignedByte

|
|Boolean|Boolean|
|Decimal|Decimal|
|Float|Float|
|Double|Double|
|Duration|Duration|
|DateTime|DateTime|
|Time|Time|
|Date|Date|

The parameter description contains any restrictions of an element or attribute. The description contains the schema data type, all restrictions and all values of each restriction.

**Parent topic:**[Using the service description tool for WSDL web service](ref_service_wsdl_ovr.md)

