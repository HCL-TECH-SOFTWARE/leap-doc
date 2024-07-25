# Troubleshooting a service description

This page is dedicated to helping you learn how to successfully create a service description file that connects to a web service. 

**Enable additional logging**

The first step to any troubleshooting is to enable the trace logging. Add the trace string "com.ibm.form.*=finest" using the appropriate method according to your deployment.

Now you can execute the service and there will be a trace file that contains more detailed information about the service call.

**Verify service URL**

Within the logs you will see how the URL is built up (with whatever parameters you supply)
```text
[17/04/14 13:49:12:534 EDT] 00001884 HTTPServiceTr 1 com.ibm.form.nitro.service.services.example.HTTPServiceTransport run Request URL is https://server:port/context
```

**Identify how the parameters/constants are resolved**

Take this declaration in the XML:
```xml
<constant>
  <id>Content-Type</id>
  <value><![CDATA[text/xml; charset=utf-8]]></value>
</constant>
 ```

You would then see this in the trace.log:

```text
[17/04/14 13:49:12:503 EDT] 00001884 Mapper        3 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Looking up source value with scheme constant:Content-Type
[17/04/14 13:49:12:503 EDT] 00001884 Mapper        3 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Source value is not a list, performing simple mapping
[17/04/14 13:49:12:504 EDT] 00001884 Mapper        1 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Target value is com.ibm.form.nitro.service.services.impl.mapping.MapValue@5adb4933
[17/04/14 13:49:12:504 EDT] 00001884 Mapper        3 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Resolving target transport:request-header-Content-Type
[17/04/14 13:49:12:504 EDT] 00001884 Mapper        1 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Source value is text/xml; charset=utf-8
[17/04/14 13:49:12:505 EDT] 00001884 Mapper        3 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Target value is not a string, or xml
[17/04/14 13:49:12:505 EDT] 00001884 Mapper        3 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Setting reference null to text/xml; charset=utf-8
```

**Verify the content sent by the service:**
```text
[17/04/14 13:49:12:514 EDT] 00001884 Mapper        1 com.ibm.form.nitro.service.services.impl.mapping.Mapper visit Source value is <SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"&gt;&lt;SOAP-ENV:Body&gt;<tns:UpdateListItems xmlns:tns="http://namespace/soap/"&gt;&lt;tns:listName/&gt;&lt;tns:updates&gt;<Batch OnError="Continue" ListVersion="1"><Method ID="1" Cmd="New"><Field Name="Title">223456</Field></Method></Batch></tns:updates></tns:UpdateListItems></SOAP-ENV:Body></SOAP-ENV:Envelope>
```

**Identify root cause of service failure**
```text
[17/04/14 13:49:12:539 EDT] 00001884 StandardExcep E com.ibm.form.nitro.platform.StandardExceptionMapper toResponse 4ef795f1-8929-44ab-a7b9-366453cc2401
                                 com.ibm.form.nitro.service.exception.AppAdminUserException: Unable to successfully execute service call. Reason: java.util.ArrayList incompatible with java.lang.String
```

The error in this case, means that the service description has a string variable and it is trying to be assigned to a "list" or vice versa.  After inspecting the xml file, we can see that there was an error in the servicemapping.  The following was the line in error

```xml
<mapping source="parameter:listName" 
         sourceType="NOOP" 
         target="transport:request-entity" 
         targetRef="SOAP-ENV:Envelope/SOAP-ENV:Body/tns:UpdateListItems/tns:listName" 
         targetType="STRING" 
>  
```

This mapping did not have a closing tag - therefore it was assumed to be a list object (rather then a string).  The fix was to add a trailing slash:

```xml
<mapping source="parameter:listName" 
         sourceType="NOOP" 
         target="transport:request-entity" 
         targetRef="SOAP-ENV:Envelope/SOAP-ENV:Body/tns:UpdateListItems/tns:listName" 
         targetType="STRING" 
/>  
```

**Parent Topic:** [Service Description](ref_service_service_description.md)