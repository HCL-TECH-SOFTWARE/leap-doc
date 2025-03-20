# Using the service description tool for WSDL web service { #usingtheservicedescriptionfromwsdltool .reference }

This tool is used to build a service description to expose services for WSDL based web service.

## Overview { .section}

This tool is built specifically for users who have a WSDL that defines the web service. The user can supply the WSDL file and the tool generates the service descriptions for each operation defined in the WSDL. The tool generates a service description for each operation for each binding for each service port. It is a command line tool.

## Requirements { .section}

You must have a valid WSDL file to use this tool. You can point to the file on the web with a URL or on a local machine with a file path.

The binding style for your WSDL must be RPC/Encoded or Document/Literal and must be declared in the file. The tool reads the binding style with the following attributes on its XPath values:

```
wsdl:binding/soap:binding/@style=[document|rpc] 
wsdl:binding/wsdl:operation/wsdl:input/@use= [literal|encoded].
```

You can use a WSDL file that declares the schema within the file, or you can use an external schema that is included or imported using a file path or URL. The tool scans for a schema file mySchema.xsd base on the relative path you specify.

-   **[WSDL service description tool parameters](ref_service_wsdl_param.md)**  
Build a command to expose services for a WSDL based web device.
-   **[Troubleshooting the WSDL service description generator - FAQ](tr_troubleshooting_wsdl_sd_tool.md)**  
Use the following information to help you troubleshoot your WSDL service description generator.

**Parent topic:** [Services](ref_services_toc.md)

