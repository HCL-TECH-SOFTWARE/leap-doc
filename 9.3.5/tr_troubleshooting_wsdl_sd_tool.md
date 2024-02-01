# Troubleshooting the WSDL service description generator - FAQ {#troubleshootingthewsdlservicedescriptiongenerator .reference}

Use the following information to help you troubleshoot your WSDL service description generator.

## Is my schema valid? { .section}

Make sure that all prefixes are bound to a namespace Usually schemas contains the following namespace declarations in `<xsd:schema>`:

```
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
targetNamespace="[value varies]"
xmlns:tns="[usually the same as targetNamespace]"
```

When a schema includes or imports other schemas, make sure that the schema is accessible through the @schemaLocation. If the @schemaLocation is a URL, verify that you can access the URL and that the URL is indeed a schema. If the @schemaLocation is an absolute file path verify that the .xsd file exists in that path. If the @schemaLocation is a relative file path make sure that the .xsd file exists in that path relative to where the importing schema is stored.

When a WSDL file is manually retrieved from the web and stored locally, you must clearly indicate the path. If the WSDL file imports an external schema with a relative URL, you must either change the schema location to point to the full URL, or save a copy of the schema and change the schema location to point to the local copy of the schema.

## Is my WSDL file valid? { .section}

Check namespace declarations. Usually WSDL files contaims the following namespace declarations in `<wsdl:definitions>`:

```
xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
targetNamespace="[value varies]"
xmlns:tns="[usually the same as targetNamespace]"
```

Several WSDL file tags have an attribute @name. According to the WSDL schema, the @name is of type NCName. It is a string without any colons. For example, `<wsdl:definitions name="ABCOrg:WebService">` is invalid.

Check the WSDL tags for case sensitivity errors. For example, `<wsdl:porttype>` is invalid, but `<wsdl:portType>` is valid.

Make sure that the binding style is specified. Binding style can either be Document/Literal or RPC/Encoded. This information is declared in this style: `wsdl:binding/soap:binding/@style`. This example can either be Document or RPC. `wsdl:binding/wsdl:operation/wsdl:input/soap:body/@used` can either be Literal or Encoded.

Make sure that the request URL is specified. This information is located here: `wsdl:service/wsdl:port/soap:address/ @location`.

Make sure that for every `<wsdl:port>` under `<wsdl:service>` has a matching `<wsdl:binding>`. Make sure that all `<wsdl:binding>` has a matching `<wsdl:portType>`.

Make sure that all `<wsdl:input>` and `<wsdl:output>` of all `<wsdl:operation>` under all `<wsdl:portType>` references a valid `<wsdl:message>`.

Make sure that all `<wsdl:message>` contains at least one `<wsdl:part>`.

If the WSDL binding style is Document/Literal, make sure that all `<wsdl:part>` uses `@element` and references an element declaration in a schema. If the WSDL binding style is RPC/Encoded, make sure that all `<wsdl:part>` uses `@type` and references an actual schema data type such as `xsd:string`, a schema `<xsd:simpleType>`, or a `<xsd:complexType>`.

## Is my service mapping reference correct? { .section}

Incorrect references often happen on RPC/Encoded outbound mapping references. This is the format of the tool, with namespace omitted.

```
<SOAP-ENV:Envelope>
  <SOAP-ENV:Body>
    <tns:[operation name+"Response"]>
      <[part name]>
        <!--Succeeding section base on schema-->
      </[part name]>
      <[part name]>
        <!--Succeeding section base on schema-->
      </[part name]>
      …
    </tns:[operation name+"Response"]>
  <SOAP-ENV:Body>
<SOAP-ENV:Envelope>
```

The following example uses a different SOAP convention that does not work with this tool:

```
<SOAP-ENV:Envelope>
  <SOAP-ENV:Body>
    <tns:[operation name+"Response"]>
      <return>
        <[part name]>
          <!--Succeeding section base on schema-->
        </[part name]>
        <[part name]>
          <!--Succeeding section base on schema-->
        </[part name]>
        …
      </return>
    </tns:[operation name+"Response"]>
  <SOAP-ENV:Body>
<SOAP-ENV:Envelope>
```

```
<SOAP-ENV:Envelope>
  <SOAP-ENV:Body>
    <tns:[operation name+"Response"]>
      <soapVal>
        <[part name]>
          <!--Succeeding section base on schema-->
        </[part name]>
        <[part name]>
          <!--Succeeding section base on schema-->
        </[part name]>
        …
      </soapVal>
    </tns:[operation name+"Response"]>
  <SOAP-ENV:Body>
<SOAP-ENV:Envelope>
```

```
<SOAP-ENV:Envelope>
  <SOAP-ENV:Body>
    <tns:[operation name+"Response"]>
      <[message name]>
        <!--Succeeding section base on schema-->
      </[message name]>
    </tns:[operation name+"Response"]>
  <SOAP-ENV:Body>
<SOAP-ENV:Envelope>
```

This is how RPC/Encoded declare a recurring simple type element:

```
<element name="elem" type="tns:ArrayOfString"/>

<complexType name="ArrayOfString">
  <complexContent>
    <restriction base="SOAP-ENC:Array">
      <attribute ref="SOAP-ENC:arrayType"    
            wsdl:arrayType="string[]/></></></>
```

Then, the tool expects a SOAP message of the following format:

```
…
<elem>
  <item>…</item>
  <item>…</item>
  …
</elem>
… 
```

If the RPC/Encoded web service SOAP message uses a different convention, the tool does not work. For example,

```
…
<elem>
  <elem>…</elem>
  <elem>…</elem>
  …
</elem>
… 
```

## Why are there missing parameters or no parameters in the generated service description? { .section}

Make sure that the WSDL file has access to the schema. All imported and included schemas are accessible.

Make sure that each operation has its matching messages and each message part has its matching schema declaration. For Document/Literal binding style, the message part should reference a schema element declaration. An RPC/Encoded binding style should reference a schema complex type declaration.

Make sure that elements and attributes have a valid type. These types can either be a `<simpleType>` declaration, a `<complexType>` declaration, or a primitive schema data type such as `xsd:string` or `xsd:boolean`. The schema data type `xsd:anyType` is not mapped to a parameter.

Make sure that the schema does not use `<any>`, `<anyAttribute>` or `@abtract=true`. If it does, you must manually add the required parameters and appropriate service mapping elements.

## Why does the web service respond with an Error 415 Unsupported media type? { .section}

The tool assumes that the value of the constant Content-Type, which in turn is mapped as the HTTP header Content-Type. If the WSDL file uses SOAP 1.1, the Content-Type is set to text/xml. If the web service uses SOAP 1.2, then the Content-Type is set to Application/soap+xml.

## Why is my request-entity not being mapped correctly? { .section}

By schema declaration and convention, inbound service mapping elements `@targetRef` are based on the inbound constant `prototypicalInstance`. It is constructed based on the declared schema, and for RPC/Encoded style binding, it also follows those conventions. Similarly, the outbound service mapping elements `@sourceRef` are based on an internally created prototypical instance, which is different from the inbound constant `prototypicalInstance`, but constructed in the similar fashion.

## Why is my `targetType=STRING` when I map to an XML and use XPath in my `targetRef`. { .section}

If you use an inbound service mapping and use XPath in your `targetRef`, the `targetType=` is not set to `STRING` because of the service mapping element wrapper. Since `<mapping target="request-entity" targetType="XML">` is set to XML, so all service mapping element child `targetTypeType` are set to `STRING`.

## Why am I getting a “namespace not binded” error? { .section}

Verify that all prefixes you use in all service mapping element references are binded. Namespace declarations are in the `<serviceMapping>`.

**Parent topic: **[Using the service description tool for WSDL web service](ref_service_wsdl_ovr.md)

