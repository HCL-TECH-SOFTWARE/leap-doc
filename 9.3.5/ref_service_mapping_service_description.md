# Mapping Data for a Service Description 

The serviceMapping element of the Service Description contains all the information needed for the HCL Leap server to map data from the Service Description inbound data to the Service Transport

## Mapping Data { .section}

Each serviceMapping consists of two elements: constants, and mapping. The constants element, defines constant values that can be mapped into the output structure. The mapping element and its child mapping elements allow mapping of the Service Description parameters to the Service Transport, or the Service Transport data to the Service Description parameters.

All the named constants available during mapping must be declared within the optional constants element. If no constants are required during mapping, the constants element can be omitted. If the constants element is present, it can contain one or more constant elements. Each constant element contains two elements: id and value, which specify the ID of the constant and its value.

The id of a constant must contain characters that are allowed in a URL path, which are \[A-Z\], \[a-z\], \[0-9\], hyphen \(-\), and underscore \(\_\).

The text of the value element is used as the value of the constant. Any XML or JSON markup that exists inside the value element is not present at run time. Literal XML values can be produced by either wrapping the contents of the element in a CDATA section, or escaping any angle brackets.

Mapping Service Description parameters to Service Transport parameters, and vice versa, is defined using mapping elements. A root mapping element must be placed as a child of serviceDescription. This root mapping contains other mapping elements that describe how data is to be mapped. The source and target of a mapping are declared using attributes on the mapping element. These attributes are: source, sourceType, sourceRef, target, targetType, and targetRef. Each mapping element can also have child mapping elements that allow repeating structures and large XML or JSON documents to be produced.

**Mapping Structure**

The input and output of both Service Descriptions and Service Transports is a simple map of key value pairs. A value can be either a string, or a list of maps of key value pairs. Leap does not support a map as a value. A value of a key in one map cannot be another map, it must be either a string or a list of maps. The mapping elements within a Service Description instruct Leap on how to produce one such structure from another, potentially extracting values from strings treated as XML or JSON.

**Mapping Definition**

Each mapping element within a Service Description describes how Leap must map data from a source to a destination. Each mapping is made up of a source, and a target. The value of the source and target attributes is a colon separated value containing the scheme of the value and its name. Valid values for the scheme depend on the binding in which the mapping is located, and whether the scheme refers to the source or target of the mapping. For inbound mapping, the source scheme must be parameter or constant, and the target must be transport. For outbound mapping, the source scheme must be transport or constant, and the target must be parameter. A summary of the valid schemes and their contexts are listed in Table 1. The name component of a scheme identifies the key to use when looking up a value or where to place the result.

Table 1. Summary of valid schemes and their contexts
<br>

|Scheme|Inbound|Inbound|Outbound|Outbound|
|------|-------|-------|--------|--------|
|Type|Source|Target|Source|Target|
|constant|Yes|No|Yes|No|
|parameter|Yes|No|No|Yes|
|transport|No|Yes|Yes|No|
<br>


Both the source and target have a type which instructs Leap how to work with the value. Both ends of a mapping can contain a reference, which allows a subset of the source to be placed at a specific location within the target. Valid values for type are string, xml, jsonand list, with string being the default. If the type is xml or json, the reference represents an XPath expression that determines which nodes are affected by the mapping. A source reference is used to extract a subset of the value identified by the source scheme. A target reference is used to construct the path where the value extracted from the source is placed. If there are no nodes that match a target reference, the node and its missing parent nodes are created. For this reason, only simple XPath predicates, those that use only the and operator, are permitted. In all other cases, the value of the reference is not used and is omitted.
<br>

Each mapping element can also contain sub-mappings, which allow repeating structures to be iterated over and built. At run time, Leap server processes the mapping elements in top-down order. Nested mappings evaluate their source and target in the context of their parent source or target mapping.

## Run time Mapping { .section}

At runtime, Leap server performs the following operations for each mapping element. Each mapping element is evaluated in the order in which it occurs within the root mapping element.

1.  Look up the source.
2.  Convert the source value if required \(parse as XML or JSON\).
3.  Resolve the source reference.
4.  Look up the target, if present.
5.  Convert the target value if required \(parent as XML or JSON\).
6.  Resolve the target reference.
7.  Map the source value to the target value.
8.  Evaluate child mapping elements.

To look up the source, the Leap server first needs to determine the scheme. If the scheme is constant, the identified constant is looked up and returned. If there is no constant with the given name, an empty string is used. If the scheme is parameter or transport, then the current context is searched for the named item. For top-level mapping elements, this is the root of the parameter structure. For child mapping elements, this is the result of the lookup, conversion, and resolve operation on its parent. If the named value cannot be found in the current context, the parent context is checked until there are no more parent contexts. If the value does not exist in any context, an empty string is used.

The value returned by the lookup operation is then converted into the type specified for the source or target. If the conversion produced an XML or JSON value, the reference is resolved, which returns a subset of the original value.

The same lookup, conversion, and resolve operations are then performed on the target of the mapping. Once both the source and target are resolved, the mapping operation begins. Generally, the cardinality of the target matches the source. For example, if a list is the source, then the target must be a list. Similarly, if a single value is the source, then the target must be a single value.

When the source is a single value, that value is assigned directly to the target value. When the source is a list, a new list is created to contain the results. For each item in the source list, the child mappings of the current mapping element are evaluated. The results of these mappings are added to the list being constructed. When all the source items are evaluated, the list is assigned to the target value.

For more information on creating a Service Description that returns JSON, see the [Leap wiki](https://hclwiki.atlassian.net/wiki/spaces/HL/pages/461239/Creating+a+Service+Description+for+a+Service+that+Returns+JSON).

**Parent topic: **[Service Description](ref_service_service_description.md)

