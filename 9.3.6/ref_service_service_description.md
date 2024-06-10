# Service Description 

A Service Description provides a specific interface to a Service Transport. The Service Description describes the inputs and outputs when you configure services within the HCL Leap mapping user interface.

## Elements of a Service Description { .section}

A Service Description is represented as an XML document that follows an XML schema. This single XML document contains all the information for a single Service Description: name, description, input and output parameters, and input and output mapping. For a full listing of the XML schema, refer to [Appendix A - Service Description schema](ref_service_service_description.md#ServDescAppendixA). The top-level element in a **Service Description** is the serviceDescription element. This element, and all of its childs, must be in the XML namespace with a URI of http://www.ibm.com/xmlns/prod/forms/services/serviceDescription/1.0.

**ID**

Each Service Description must contain a unique id that identifies it to the Leap server. The id can contain any characters that are valid as a component of a URL path. These characters include:

   - Alphabetical letters – \[A-Z\], and \[a-z\]
    -   Numerals – \[0-9\]
    -   Hyphens – \[-\]
    -   Underscore – \[\_\]

  Because a Service Description ID is a surrogate for the Service Description itself, this ID does not must be descriptive. Any UUID is a valid choice for a Service Description ID because it guarantees uniqueness and contains only characters that are valid in a URL path component.

**Transport ID**

A Service Description must reference a Service Transport to perform its underlying operation. Each Service Transport has its own unique transportId that uniquely identifies it to the Leap server. The ID for a Service Transport must be made available by its developer.

**Name and Description**

To help users build Leap applications with services, each Service Description contains both a name, and a description. The name and description elements allow you to localize a Leap Service Description in multiple languages using duplicate elements, each with a different xml:lang attribute and contents.See [Localizing Service Descriptions](ref_service_localizing_service_description.md) for information about how to provide names and descriptions in multiple languages.

**Default Locale**

If the Service Description is not localized in the language of a particular user, the defaultLocale contains the locale in which the name and description must be presented. For example, if a user asks for the Service Description in French, but the Service Description has only English and Spanish strings, the English is returned if en is set as the defaultLocale.

**Credentials**

The credentials contains the configuration for a Credentials Provider. The ID of the credentials provider is specified in the **providerId** attribute. The **credentials element** can contain zero or more **property** elements to configure the properties of the specified **Credentials** Provider. 

Each **property** element must contain a name attribute whose value is the name of the property being configured, and a **value** attribute that contains the value of the property.
Not all **Credentials** Providers are applicable to all Service Transports. Therefore, the documentation for each Service Transport must be consulted before you configure the **credentials** element. If the configured Service Transport does not understand the provider that is specified by **providerId**, the Service Description is not available.

**Bindings**

Every Service Description must specify its input and output structures. These structures outline the ID, name, description, and type of each parameter and any **subparameters**. In addition to the parameter structure, bindings might also contain a section that declares how data going into the Service Transport is mapped from the input structure and how data coming from the Service Transport is mapped to the output structure.

There are two top-level elements for bindings: inbound, and outbound. Inbound defines the binding for data coming into the Service Description from the Builder Application. Outbound defines the data going to the Leap application from the Service Description. Only one of each of these elements can be present within a single Service Description, and each must be placed as a child of the **serviceDescription** element.

Directly underneath inbound and outbound are two elements that define the main components of a binding: parameters and **serviceMapping**. The parameters element contains all the information that is related to the parameters. The contents of the **serviceMapping** element instructs Leap how to map data coming from the parameters into data for the transport and vice versa.

**Parameters**

The **parameters** element contains zero or more **parameter** elements. Each parameter element defines a single parameter coming into or being returned from the Service Description. Each **parameter** element must have an **id**, **type**, **name**, and **description**. The id element uniquely identifies the parameter within the binding. The type element specifies the type of data that is expected to be contained within the parameter. The following data types are supported: **STRING, BOOLEAN, DECIMAL, FLOAT, DOUBLE, INTEGER, DATETIME, TIME, DATE,** and **LIST**.

As with the name and description child elements of the **serviceDescription** element, these childs of parameter specify the name and description of the parameter that is used in Leap. These elements can also be localized using the **xml:lang** attribute.

Optionally, the mandatory element can be included for inbound bindings to specify whether the parameter must be bound before starting the Service Description. Valid values for this element are true and false, with the latter being the default.

Each parameter element can have a child element that is called parameters which is a container for child parameters. The contents of the parameters element is one or more parameter elements. If a parameter contains **subparameters**, its type is set to LIST. At run time, the parameter contains a list of structures with each of the **subparameters**.

**Service Mapping**

The **serviceMapping** element contains all the information that is needed for the Leap server to map data between the Service Description parameters, and the Service Transport. For more information, see [Mapping Data for a Service Description](ref_service_mapping_service_description.md).

## XML Namespaces { .section}

XML namespace declarations must be defined on the **serviceMapping** element or higher.

## Sample Service Descriptions { .section}

Each example in this section includes a list of the Service Descriptions and a discussion of how each Service Description operates. The Service Descriptions in this section rely solely on the Service Transports that are shipped with the Leap server. Where applicable, sample and setup instructions are included.

**Example 1: Simple Mapping**

The following Service Description uses the HTTP Service Transport to make a request to a web server and return the content type of the response. In this example, the URL to which the request is made comes as an inbound parameter from the Builder application.

```xml
1: <?xml version="1.0" encoding="UTF-8"?>  
2: <serviceDescription>  
3:   <id>get-content-type</id>  
4:   <defaultLocale>en-us</defaultLocale>  
5:   <transportId>HTTPServiceTransport</transportId>  
6:   <name xml:lang="en-us">Get Content Type</name>  
7:   <description xml:lang="en-us">  
8: 	Retrieves the content type of the response from an HTTP server for the configured URL.  
9:   </description> 
10:   <inbound> 
11: 	<parameters> 
12: 	  <parameter> 
13: 		<id>request-url</id> 
14: 		<type>STRING</type> 
15: 		<name xml:lang="en-us">URL</name> 
16: 		<description xml:lang="en-us">URL to request.</description> 
17: 		<mandatory>true</mandatory> 
18: 	  </parameter> 
19: 	</parameters> 
20:   </inbound> 
21:   <outbound> 
22: 	<parameters> 
23: 	  <parameter> 
24: 		<id>response-header-content-type</id> 
25: 		<type>STRING</type> 
26: 		<name xml:lang="en-us">Content Type</name> 
27: 		<description xml:lang="en-us">Content Type of the response.</description> 
28: 	  </parameter> 
29: 	</parameters> 
30:   </outbound> 
31: </serviceDescription>
```

All Service Descriptions begin with a **serviceDescription** element, and in this example, it is defined in line 2. The **serviceDescription** element contains all the information that is needed for the Leap server to work with the Service Description. The unique ID of this Service Description is **get-content-type** as defined in line 3. The unique ID is not exposed to a user, but it must be unique. 
Line 5 declares the ID of the Service Transport to use, which is **HTTPServiceTransport**, and this is the unique ID of the HTTP Service Transport. Lines 7 and 8 define the **name** and **description** of the Service Description, which are presented to the user when designing applications.

Lines 10-20 define the inbound bindings, and lines 21-30 define the outbound bindings. As mentioned previously, the inbound bindings refer to the parameters that are flowing from the application to the Service Transport. The outbound bindings refer to the parameters that are flowing in the opposite direction.

Lines 11-19 contain all the inbound parameters, of which there is only one.
<br>
The parameter that is defined in lines 12-18 represents the URL to which a request is made. According to the HTTP Service Transport documentation, the parameter that contains the URL to which the request is made must be called **request-url**.

Line 13 defines the **id** of the parameter so that it matches the expectations of the HTTP Service Transport.

The **name** and **description** are defined in lines 15 and 16, and line 17 specifies that this parameter must be supplied in order for this Service Description to operate.

Lines 21-30 define the outbound parameters for the Service Description. In this case, there is only one output parameter: the content type of the response. The HTTP Service Transport dynamically creates new parameters that are based on the information that is returned in the HTTP response. In particular, response headers are converted to lowercase and are prefixed with **response-header-**. Since this Service Description is interested in the Content-Type header, the outbound parameter **response-header-content-type** is created in lines 23-28 to contain this data.

**Example 2: Augmenting Parameters with Constants**

The following Service Description returns the same information as Example 1. However, in this case, we do not want the Leap application to supply the URL. Instead, the URL is declared using a constant, and mapped into the inbound parameters for the Service Transport.

```xml
1: <?xml version="1.0" encoding="UTF-8"?>
2: <serviceDescription>
3:   <id>get-content-type-with-constant</id>
4:   <defaultLocale>en-us</defaultLocale>
5:   <transportId>HTTPServiceTransport</transportId>
6:   <name xml:lang="en-us">Get Content Type with Constant</name>
7:   <description xml:lang="en-us">
8: 	Retreives the content type of the response from an HTTP server.
9:   </description>
10:   <inbound>
11: 	<serviceMapping>
12: 	  <constants>
13: 		<constant>
14: 		  <id>url-to-request</id>
15: 		  <value>http://www.ibm.com</value>
16: 		</constant>
17: 	  </constants>
18: 	  <mapping>
19: 		<mapping source="constant:url-to-request" sourceType="string" target="transport:request-url" targetType="string"/>
20: 	  </mapping>
21: 	</serviceMapping>
22:   </inbound>
23:   <outbound>
24: 	<parameters>
25: 	  <parameter>
26: 		<id>response-header-content-type</id>
27: 		<type>STRING</type>
28: 		<name xml:lang="en-us">Content Type</name>
29: 		<description xml:lang="en-us">Content Type of the response.</description>
30: 	  </parameter>
31: 	</parameters>
32:   </outbound>
33: </serviceDescription>
```

Like Example 1, the Service Description makes a request to an HTTP server and returns the content type of the response. However, this Service Description differs from the Example 1 because there are no input parameters to this service. The request-url HTTP Service Transport parameter is mapped into the transport via a constant.

Lines 12-17 define the constants section. There is a single constant that is defined in lines 13-16. This constant has an id of **url-to-request** specified in line 14, and a value of http://www.ibm.com, specified in line 15. The id of the constant is used when creating the parameter structure that is passed to the Service Transport. This constant is referenced in line 19 within the mapping section.

Lines 18-20 contain the mapping information. Since there is only one parameter to be sent, there is only one mapping, which is defined in line 19. This mapping specifies that the value of the Service Transport parameter named **request-url** is specified by the value of the constant named **url-to-request**.

**Example 3: Lists of Data**

The following Service Description demonstrates the use of nested parameters. This example is the same as the Service Description used for the Countries by Region service that is shipped with Leap. This example describes how to specify a region and return a list of the names of countries within that region.

```xml
1: <?xml version="1.0" encoding="UTF-8"?>
2: <serviceDescription>
3:   <id>countries-by-region</id>
4:   <defaultLocale>en-us</defaultLocale>
5:   <transportId>4647b8cf-093f-11e0-89dd-001e4cf83606</transportId>
6:   <name xml:lang="en-us">
7: 	Countries by Region using Service Description
8:   </name>
9:   <description xml:lang="en-us">
10: 	Given a region, return a list of country information in that region.
11:   </description>
12:   <inbound>
13: 	<parameters>
14: 	  <parameter>
15: 		<id>region</id>
16: 		<type>STRING</type>
17: 		<name xml:lang="en-us">Region</name>
18: 		<description xml:lang="en-us">
19: 		  One of "Africa", "America, North", "America, South", "Asia", "Europe", or "Oceania"
20: 		</description>
21: 		<mandatory>true</mandatory>
22: 	  </parameter>
23: 	</parameters>
24:   </inbound>
25:   <outbound>
26: 	<parameters>
27: 	  <parameter>
28: 		<id>countries</id>
29: 		<type>LIST</type>
30: 		<name xml:lang="en-us">Countries"</name>
31: 		<description xml:lang="en-us">List of country information</description>
32: 		<parameters>
33: 		  <parameter>
34: 			<id>name</id>
35: 			<type>STRING</type>
36: 			<name xml:lang="en-us">Name</name>
37: 			<description xml:lang="en-us">Name of Country</description>
38: 		  </parameter>
39: 		</parameters>
40: 	  </parameter>
41: 	</parameters>
42:   </outbound>
43: </serviceDescription>
```

As with the other Service Description examples, this Service Description has its own unique ID, defined in line 3, a name, which is defined in lines 6-8, and a description, which is defined in lines 9-11. This Service Description uses the sample Countries by Region Service Transport, which is shipped with the Leap , and is identified by its id in line 5.

Because this Service Description has a single inbound parameter, the parameters element, in lines 13-23, of the inbound bindings in lines 12-24. parameters contains only a single parameter, which is defined in lines 14-22. The id of this parameter is region, which is what is expected by the Countries by Region Service Transport.

Since there can be multiple countries within a region, the outbound bindings, which are defined in lines 25-42, must contain a list parameter to contain all the information for each country. The outbound structure for this Service Description consists of a parameter that is called countries that contains a list of maps. Each of the maps that are contained within the countries list consists of a single name key that contains the name of a country. This structure is defined within the parameters element, which is defined in lines 26-41, of the outbound bindings section. The top-level parameter, countries, is defined between lines 27 and 40. Since the countries parameter contains other parameters, its type is set as LIST in line 29. All the parameters of the list entries are defined within the parameters element inside the countries parameter that is defined in lines 32-39. The single name **subparameter** is defined in lines 33-38.

Since the inbound and outbound bindings directly match what is returned by the Countries by Region Service Transport, there is no need for any mapping information. This service can be set up such that the name **subparameter** is mapped to list-like items such as drop-down options or an item in a table.

**Example 4: Mapping XML into Parameters**

The following Service Description extracts data from an XML document that is returned from an HTTP request using the HTTP Service Transport.

```xml
1: <?xml version="1.0" encoding="UTF-8"?>
2: <serviceDescription>
3:   <id>address-lookup</id>
4:   <defaultLocale>en-us</defaultLocale>
5:   <transportId>HTTPServiceTransport</transportId>
6:   <name xml:lang="en-us">Address Lookup</name>
7:   <description xml:lang="en-us">Returns information related to a postal code or address.</description>
8:   <inbound>
9: 	<parameters>
10: 	  <parameter>
11: 		<id>address</id>
12: 		<type>STRING</type>
13: 		<name xml:lang="en-us">Address or Postal Code</name>
14: 		<description xml:lang="en-us"></description>
15: 		<mandatory>true</mandatory>
16: 	  </parameter>
17: 	</parameters>
18: 	<serviceMapping>
19: 	  <constants>
20: 		<constant>
21: 		  <id>request-url</id>
22: 		  <value>http://maps.googleapis.com/maps/api/geocode/xml</value>
23: 		</constant>
24: 		<constant>
25: 		  <id>false-constant</id>
26: 		  <value>false</value>
27: 		</constant>
28: 		<constant>
29: 		  <id>request-method</id>
30: 		  <value>GET</value>
31: 		</constant>
32: 	  </constants>
33: 	  <mapping>
34: 		<mapping target="transport:request-url" source="constant:request-url"/>
35: 		<mapping target="transport:request-method" source="constant:request-method"/>
36: 		<mapping target="transport:request-query-address" source="parameter:address"/>
37: 		<mapping target="transport:request-query-sensor" source="constant:false-constant"/>
38: 	  </mapping>
39: 	</serviceMapping>
40:   </inbound>
41:   <outbound>
42: 	<parameters>
43: 	  <parameter>
44: 		<id>latitude</id>
45: 		<type>STRING</type>
46: 		<name xml:lang="en-us">Latitude</name>
47: 		<description xml:lang="en-us"></description>
48: 	  </parameter>
49: 	  <parameter>
50: 		<id>longitude</id>
51: 		<type>STRING</type>
52: 		<name xml:lang="en-us">Longitude</name>
53: 		<description xml:lang="en-us"></description>
54: 	  </parameter>
55: 	  <parameter>
56: 		<id>address-information</id>
57: 		<type>LIST</type>
58: 		<name xml:lang="en-us">Address Information</name>
59: 		<description xml:lang="en-us"></description>
60: 		<parameters>
61: 		  <parameter>
62: 			<id>long-name</id>
63: 			<type>STRING</type>
64: 			<name xml:lang="en-us">Long Name</name>
65: 			<description xml:lang="en-us"></description>
66: 		  </parameter>
67: 		  <parameter>
68: 			<id>short-name</id>
69: 			<type>STRING</type>
70: 			<name xml:lang="en-us">Short Name</name>
71: 			<description xml:lang="en-us"></description>
72: 		  </parameter>
73: 		  <parameter>
74: 			<id>type-1</id>
75: 			<type>STRING</type>
76: 			<name xml:lang="en-us">Type</name>
77: 			<description xml:lang="en-us"></description>
78: 		  </parameter>
79: 		  <parameter>
80: 			<id>type-2</id>
81: 			<type>STRING</type>
82: 			<name xml:lang="en-us">Type(2)</name>
83: 			<description xml:lang="en-us"></description>
84: 		  </parameter>
85: 		</parameters>
86: 	  </parameter>
87: 	</parameters>
88: 	<serviceMapping>
89: 	  <mapping>
90: 		<mapping source="transport:response-entity" 
91: 				 sourceRef="GeocodeResponse/result[1]/geometry/location/lat" 
92: 				 sourceType="xml" 
93: 				 target="parameter:latitude"/>
94: 		<mapping source="transport:response-entity" 
95: 				 sourceRef="GeocodeResponse/result[1]/geometry/location/lng" 
96: 				 sourceType="xml" 
97: 				 target="parameter:longitude"/>
98: 		<mapping source="transport:response-entity" 
99: 				 sourceRef="GeocodeResponse/result[1]/address_component" 
100: 				 sourceType="xml" 
101: 				 target="parameter:address-information">
102: 		  <mapping sourceRef="long_name" target="parameter:long-name"/>
103: 		  <mapping sourceRef="short_name" target="parameter:short-name"/>
104: 		  <mapping sourceRef="type[1]" target="parameter:type-1"/>
105: 		  <mapping sourceRef="type[2]" target="parameter:type-2"/>
106: 		</mapping>
107: 	  </mapping>
108: 	</serviceMapping>
109:   </outbound>
110: </serviceDescription>
```

This Service Description performs a reverse address lookup using a free Google web service. As with the other Service Description examples, the standard prologue of id, **transportId**, name, and description is specified in lines 3-7. This service has a single parameter, address, that can be assigned by an application, as specified in lines 10-16. Since this parameter is required to perform the address look-up, it is marked as mandatory in line 15.

Since this Service Description uses the HTTP Service Transport, a **request-url** must be specified. The URL used in this request takes the form http://maps.googleapis.com/maps/api/geocode/xml?address=\[address\]&sensor=\[true\|false\]. Because there are query parameters that must be sent, this Service Description uses the HTTP Service Transport support for query parameters by prefixing the name of the parameter with request-query-. However, because some of these query parameters are not exposed to the user, you must create a mapping section to map some constant values. The inbound binding constant section, in lines 19-32, defines the three constants that are used: **request-url**, lines 20-23, false-constant, lines 24-27, and **request-method**, lines 28-31. These constants contain the URL to which to request is made, a constant string value false for the sensor query parameter, and the request method. While some of these constants, including **request-url** and request-method, match the name of the parameter to which they are applied, there is no requirement that they match. Parameter names that match do not automatically get a constant value if it has the same name. All mapping must be explicitly defined.

In lines 33-38, the mapping section of the inbound binding maps the constants and Service Description parameters to the Service Transport parameters. Each of the mapping elements is fairly self-explanatory: the **request-url** constant is mapped to the **request-url** transport parameter; the request-method constant is mapped to the request-method transport parameter; the address parameter is mapped to the request-query-address transport parameter; and the constant false-constant is mapped to the sensor transport parameter.

The HTTP Service Transport then builds a URL out of the **request-url**, **request-query-address**, and **request-query-sensor** parameters, and makes a request to that URL using the HTTP method given in the request-method parameter. The response body that is returned by this request is placed in the response-entity transport parameter, which is then taken apart by the mapping section of the outbound bindings.

This service expects the response-entity to be similar to the following:<br>

```xml
1: <?xml version="1.0" encoding="UTF-8"?> 
2: <GeocodeResponse> 
3:  <status>OK</status> 
4:  <result> 
5:   <type>street_address</type> 
6:   <formatted_address>1 New Orchard Rd, Armonk, NY, USA</formatted_address> 
7:   <address_component> 
8:    <long_name>1</long_name> 
9:    <short_name>1</short_name> 
10:    <type>street_number</type> 
11:   </address_component> 
12:   <address_component> 
13:    <long_name>New Orchard Rd</long_name> 
14:    <short_name>New Orchard Rd</short_name> 
15:    <type>route</type> 
16:   </address_component> 
17:   <address_component> 
18:    <long_name>Armonk</long_name> 
19:    <short_name>Armonk</short_name> 
20:    <type>locality</type> 
21:    <type>political</type> 
22:   </address_component> 
23:   <address_component> 
24:    <long_name>Westchester</long_name> 
25:    <short_name>Westchester</short_name> 
26:    <type>administrative_area_level_2</type> 
27:    <type>political</type> 
28:   </address_component> 
29:   <address_component> 
30:    <long_name>New York</long_name> 
31:    <short_name>NY</short_name> 
32:    <type>administrative_area_level_1</type> 
33:    <type>political</type> 
34:   </address_component> 
35:   <address_component> 
36:    <long_name>United States</long_name> 
37:    <short_name>US</short_name> 
38:    <type>country</type> 
39:    <type>political</type> 
40:   </address_component> 
41:   <geometry> 
42:    <location> 
43:     <lat>41.1083018</lat> 
44:     <lng>-73.7204677</lng> 
45:    </location> 
46:    <location_type>ROOFTOP</location_type> 
47:    <viewport> 
48:     <southwest> 
49:      <lat>41.1051542</lat> 
50:      <lng>-73.7236153</lng> 
51:     </southwest> 
52:     <northeast> 
53:      <lat>41.1114494</lat> 
54:      <lng>-73.7173201</lng> 
55:     </northeast> 
56:    </viewport> 
57:   </geometry> 
58:  </result> 
59: </GeocodeResponse>
```

There is much data in this response, but only some of it is needed for this Service Description. The latitude, longitude, and a list of the address information from the first result is required. To get only the required information, the Service Description outlines the parameters that it expects to return in the parameters section, in lines 42-87. The Service Description then uses the mapping section, in lines 88-108, to extract the required data from the response-entity transport parameter. Each of the parameters in the parameters section is self-explanatory. Latitude and longitude are top-level parameters because there is only one of each of them in a single result. However, there are several address\_component elements, each of which are returned. Therefore, the address-information parameter is a list parameter that contains subparameters, one for each of the pieces of information in an address\_component that the Service Description wants to make available.

In lines 88-108, the service mapping section defines all the mapping that must be performed to extract the data from the XML response. Latitude, which is specified in lines 90-93, and longitude, which is specified in lines 94-97, each extract the data using a single **XPath** expression. The source type for each is set to XML. Mapping of a repeating structure is accomplished in a similar fashion. Lines 98-101 define the mapping for the address-information parameter. The **XPath** expression for **address-information** returns a **nodeset** as there are several nodes that match the expression GeocodeResponse/result/address\_component. For each node that is returned, a new structure is created to contain the result of each of the submappings. Each of the submappings places its target into the newly created structure. Since the source of each of the submappings is one of the matched nodes, the mapping elements do not specify a source. It is assumed to be the inherited context. Similarly, the reference is evaluated within the context of the source, which is inherited. After each of the submappings is evaluated for a single source, the structure is added to a running list and the submappings are evaluated again for the next result in the source list. When all the sources are processed, the list that was collecting the results of the map is assigned to the address-information parameter.

**Example 5. Service Description for JSON response**

This example uses the same lookup service but receives a JSON response instead of XML.

This service description provides three different kinds of output based on what the Google API returns:

1. Individual output parameters that will automatically select the first item returned

2. A list of the search results that contains fields for all of the return parameters

3. A list that returns the address components in the raw format of the service

This demonstrates the variety of output formats and the flexibility that you have in manipulating the response data to suit your needs.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<serviceDescription>
  <id>address-lookup-json</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Address Lookup (JSON)</name>
  <description xml:lang="en-us">Returns information related to a postal code or address.</description>
  <inbound>
	<parameters>
	  <parameter>
			<id>address</id>
			<type>STRING</type>
			<name xml:lang="en-us">Address or Postal Code</name>
			<description xml:lang="en-us">The address you want to search for</description>
			<mandatory>true</mandatory>
		</parameter>
	  <parameter>
			<id>components</id>
			<type>STRING</type>
			<name xml:lang="en-us">Components to Return</name>
			<description xml:lang="en-us"><![CDATA[A filter consists of a list of component:value pairs separated by a pipe (|). Only the results that match all the filters will be returned.
				The components that can be filtered include:
	i) route matches long or short name of a route.
	ii) locality matches against both locality and sublocality types. 
	iii) administrative_area matches all the administrative_area levels. 
	iv) postal_code matches postal_code and postal_code_prefix.
	v) country matches a country name or a two letter ISO 3166-1 country code.]]></description>
			<mandatory>false</mandatory>
	  </parameter>
	</parameters>
	<serviceMapping>
	  <constants>
			<constant>
			  <id>request-url</id>
			  <value>http://maps.googleapis.com/maps/api/geocode/json</value>
			</constant>
			<constant>
			  <id>false</id>
			  <value>false</value>
			</constant>
			<constant>
			  <id>request-method</id>
			  <value>GET</value>
			</constant>
			<constant>
			  <id>ignore_empty</id>
			  <value>true</value>
			</constant>
	  </constants>
	  <mapping xmlns="">
			<mapping target="out:request-url" source="constant:request-url"/>
			<mapping target="out:request-method" source="constant:request-method"/>
			<mapping target="out:request-query-address" source="parameter:address"/>
			<mapping target="out:request-query-components" source="parameter:components"/>
			<mapping target="out:request-query-sensor" source="constant:false"/>
			<mapping target="transport:request-ignore-empty-query" source="constant:ignore_empty" sourceType="STRING" targetType="STRING"/>
	  </mapping>
	</serviceMapping>
  </inbound>
  <outbound>
	<parameters>
		<parameter>
			<id>status</id>
			<type>STRING</type>
			<name xml:lang="en-us">Status Code</name>
			<description xml:lang="en-us">The "status" field within the Geocoding response object contains the status of the request, and may contain debugging information to help you track down why geocoding is not working. The "status" field may contain the following values:
	i) "OK" indicates that no errors occurred; the address was successfully parsed and at least one geocode was returned. 
	ii) "ZERO_RESULTS" indicates that the geocode was successful but returned no results. This may occur if the geocoder was passed a non-existent address. 
	iii) "OVER_QUERY_LIMIT" indicates that you are over your quota.
	iv) "REQUEST_DENIED" indicates that your request was denied.
	v) "INVALID_REQUEST" generally indicates that the query (address, components or latlng) is missing. 
	vi) "UNKNOWN_ERROR" indicates that the request could not be processed due to a server error. The request may succeed if you try again.</description>
	  </parameter>
	  <parameter>
			<id>formatted-address</id>
			<type>STRING</type>
			<name xml:lang="en-us">Street Address</name>
			<description xml:lang="en-us">The fully formatted street address.</description>
	  </parameter>

	  <parameter>
			<id>street-number</id>
			<type>STRING</type>
			<name xml:lang="en-us">Street Number</name>
			<description xml:lang="en-us">The street number of the specified address</description>
	  </parameter>

	  <parameter>
			<id>street-name</id>
			<type>STRING</type>
			<name xml:lang="en-us">Street Name</name>
			<description xml:lang="en-us">The street name of the specified address</description>
	  </parameter>

	  <parameter>
			<id>city</id>
			<type>STRING</type>
			<name xml:lang="en-us">City</name>
			<description xml:lang="en-us">The city of the specified address</description>
	  </parameter>

	  <parameter>
			<id>state</id>
			<type>STRING</type>
			<name xml:lang="en-us">State</name>
			<description xml:lang="en-us">The state of the specified address</description>
	  </parameter>

	  <parameter>
			<id>country</id>
			<type>STRING</type>
			<name xml:lang="en-us">Country</name>
			<description xml:lang="en-us">The country of the specified address</description>
	  </parameter>

	  <parameter>
			<id>postal-code</id>
			<type>STRING</type>
			<name xml:lang="en-us">Zip/Postal Code</name>
			<description xml:lang="en-us">The zip/postal code of the specified address</description>
	  </parameter>

	  <parameter>
			<id>latitude</id>
			<type>STRING</type>
			<name xml:lang="en-us">Latitude</name>
			<description xml:lang="en-us">The latitude of the specified address</description>
	  </parameter>

	  <parameter>
			<id>longitude</id>
			<type>STRING</type>
			<name xml:lang="en-us">Longitude</name>
			<description xml:lang="en-us">The longitude of the specified address</description>
	  </parameter>

	  <parameter>
			<id>latitude-longitude</id>
			<type>STRING</type>
			<name xml:lang="en-us">Latitude and Longitude</name>
			<description xml:lang="en-us">The latitude and longitude of the address in one formatted string</description>
	  </parameter>
	  
	  <!-- -->
	  <parameter>
			<id>results</id>
			<type>LIST</type>
			<name xml:lang="en-us">Results</name>
			<description xml:lang="en-us"></description>
			<parameters>
			  <parameter>
					<id>list-formatted-address</id>
					<type>STRING</type>
					<name xml:lang="en-us">Street Address</name>
					<description xml:lang="en-us">The fully formatted street address.</description>
			  </parameter>
		
			  <parameter>
					<id>list-street-number</id>
					<type>STRING</type>
					<name xml:lang="en-us">Street Number</name>
					<description xml:lang="en-us">The street number of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-street-name</id>
					<type>STRING</type>
					<name xml:lang="en-us">Street Name</name>
					<description xml:lang="en-us">The street name of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-city</id>
					<type>STRING</type>
					<name xml:lang="en-us">City</name>
					<description xml:lang="en-us">The city of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-state</id>
					<type>STRING</type>
					<name xml:lang="en-us">State</name>
					<description xml:lang="en-us">The state of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-country</id>
					<type>STRING</type>
					<name xml:lang="en-us">Country</name>
					<description xml:lang="en-us">The country of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-postal-code</id>
					<type>STRING</type>
					<name xml:lang="en-us">Zip/Postal Code</name>
					<description xml:lang="en-us">The zip/postal code of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-latitude</id>
					<type>STRING</type>
					<name xml:lang="en-us">Latitude</name>
					<description xml:lang="en-us">The latitude of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-longitude</id>
					<type>STRING</type>
					<name xml:lang="en-us">Longitude</name>
					<description xml:lang="en-us">The longitude of the specified address</description>
			  </parameter>
		
			  <parameter>
					<id>list-latitude-longitude</id>
					<type>STRING</type>
					<name xml:lang="en-us">Latitude and Longitude</name>
					<description xml:lang="en-us">The latitude and longitude of the address in one formatted string</description>
			  </parameter>
			</parameters>
	  </parameter>
	  <!-- -->

	  <parameter>
			<id>address-information</id>
			<type>LIST</type>
			<name xml:lang="en-us">Address Information</name>
			<description xml:lang="en-us"></description>
			<parameters>
			  <parameter>
					<id>long-name</id>
					<type>STRING</type>
					<name xml:lang="en-us">Long Name</name>
					<description xml:lang="en-us">The long name of an address component</description>
			  </parameter>
			  <parameter>
					<id>short-name</id>
					<type>STRING</type>
					<name xml:lang="en-us">Short Name</name>
					<description xml:lang="en-us">The short name of an address component</description>
			  </parameter>
			  <parameter>
					<id>type-1</id>
					<type>STRING</type>
					<name xml:lang="en-us">Type</name>
					<description xml:lang="en-us">The type of an address component</description>
			  </parameter>
			  <parameter>
					<id>type-2</id>
					<type>STRING</type>
					<name xml:lang="en-us">Type(2)</name>
					<description xml:lang="en-us">The secondary type of an address component</description>
			  </parameter>
			</parameters>
	  </parameter>

	</parameters>
	<serviceMapping xmlns="">
	  <mapping>
		<!-- Returns the first item and breaks out each component into its own output parameter -->
		<mapping source="transport:response-entity" sourceRef="status" sourceType="json" target="parameter:status"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/formatted_address" sourceType="json" target="parameter:formatted-address"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='street_number']/long_name" sourceType="json" target="parameter:street-number"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='route']/long_name" sourceType="json" target="parameter:street-name"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='locality']/long_name" sourceType="json" target="parameter:city"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='administrative_area_level_1']/long_name" sourceType="json" target="parameter:state"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='country']/long_name" sourceType="json" target="parameter:country"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/address_components[types='postal_code']/long_name" sourceType="json" target="parameter:postal-code"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/geometry/location/lat" sourceType="json" target="parameter:latitude"/>
		<mapping source="transport:response-entity" sourceRef="results[1]/geometry/location/lng" sourceType="json" target="parameter:longitude"/>
		<mapping source="transport:response-entity" sourceRef="concat(results[1]/geometry/location/lat, ',', results[1]/geometry/location/lng)"  sourceType="json" target="parameter:latitude-longitude"/>
		
		<!-- Returns all items as a table with each of its components defined as columns -->
		<!-- the parent element is "results" all the children element can then be referenced as children to this root element -->
		<mapping source="transport:response-entity" sourceRef="results" sourceType="json" target="parameter:results">
		  <mapping sourceRef="status" sourceType="json" target="parameter:status"/>
			<mapping sourceRef="formatted_address" sourceType="json" target="parameter:list-formatted-address"/>
			<mapping sourceRef="address_components[types='street_number']/long_name" sourceType="json" target="parameter:list-street-number"/>
			<mapping sourceRef="address_components[types='route']/long_name" sourceType="json" target="parameter:list-street-name"/>
			<mapping sourceRef="address_components[types='locality']/long_name" sourceType="json" target="parameter:list-city"/>
			<mapping sourceRef="address_components[types='administrative_area_level_1']/long_name" sourceType="json" target="parameter:list-state"/>
			<mapping sourceRef="address_components[types='country']/long_name" sourceType="json" target="parameter:list-country"/>
			<mapping sourceRef="address_components[types='postal_code']/long_name" sourceType="json" target="parameter:list-postal-code"/>
			<mapping sourceRef="geometry/location/lat" sourceType="json" target="parameter:list-latitude"/>
			<mapping sourceRef="geometry/location/lng" sourceType="json" target="parameter:list-longitude"/>
			<mapping sourceRef="concat(geometry/location/lat, ',', geometry/location/lng)"  sourceType="json" target="parameter:list-latitude-longitude"/>
		</mapping>

 		<!-- All the objects are returned in this table structure that mimics the JSON return structure -->
		<mapping source="transport:response-entity" sourceRef="results/address_components" sourceType="json" target="parameter:address-information">
		  <mapping sourceRef="long_name" target="parameter:long-name"/>
		  <mapping sourceRef="short_name" target="parameter:short-name"/>
		  <mapping sourceRef="types[1]" target="parameter:type-1"/>
		  <mapping sourceRef="types[2]" target="parameter:type-2"/>
		</mapping>

	  </mapping>
	</serviceMapping>
  </outbound>
</serviceDescription>
```

Note a few things:

1. The outer mapping references the root results element

2. All the rows will be represented by the child mappings.  The child mappings use relative references to specify where the source comes from (sourceRef).  This means that the "results" list object will contain all the rows that are returned from the service call.  Each row will have the parameters that are defined by all the inner/child mappings.

3. XPath is used to parse the JSON results and place each data item into its own named parameter,  for example: 
```xml
address_components[types='route']/long_nameequals list-street-name
```

4. A new output parameter was added and set to the concatenation of the latitude and longitude.


-   **[Localizing Service Descriptions](ref_service_localizing_service_description.md)**  
The name and description elements allow you to localize an HCL Leap Service Description in multiple languages using duplicate elements, each with a different xml:lang attribute and contents.
-   **[Mapping Data for a Service Description](ref_service_mapping_service_description.md)**  
The serviceMapping element of the Service Description contains all the information needed for the HCL Leap server to map data from the Service Description inbound data to the Service Transport
-   **[Deploying a Service Description](ref_service_deploying_service_description.md)**  
This topic contains information about how to deploy an HCL Leap Service Description.
-   **[Troubleshooting a service description](ref_service_troubleshooting_service_description.md)**
How to troubleshoot a custom service description that is not working.

**Parent topic:** [Services](ref_services_toc.md)

