# Service Catalog {#helm_service_catalog .concept}

The serviceCatalog parameter can be used to pass service descriptions to Leap, which will be picked up by Leap automatically.

Each service definition in the .yaml is made up of a label and the xml content of the service description. The XML content will be copied into a file and placed in the service catalog.

For more information on creating service descriptions, see [Service Description](ref_service_service_description.md).

Example:

``` {#codeblock_n2n_fkt_gxb}
configuration:
  leap:
    serviceCatalog:
       sampleServiceDescription.xml: |
         <?xml version="1.0" encoding="utf-8"?>
         <serviceDescription>
         <id>sample-service-description</id>
         <defaultLocale>en</defaultLocale>
         <transportId>HTTPServiceTransport</transportId>
         <name xml:lang="en">Sample service Description</name>
         <description xml:lang="en"></description>
            . . . 
         </serviceDescription>
```

**Parent topic: **[Preparation](helm_preparation.md)

