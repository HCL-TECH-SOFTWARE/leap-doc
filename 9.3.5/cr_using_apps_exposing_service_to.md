# Service Oriented Architecture – Exposing a service to HCL Leap {#exposingaservicetofeb .concept}

The following information is an overview of Service Oriented Architecture built into Leap, and describes how to expose a service to Leap.

The Leap has an extensible services architecture which allows Leap applications to send and receive data from any external system. The Services Architecture consists of the following components:

-   **Service Transports** – The Service Transport is the Java™ code responsible for communicating with an external service, such as a public REST service. It can send data out to the external service or receive data from the external service. The transport also uses JDBC to store and retrieve data from any database. Alternatively, the transport can simply implement a “service” itself, such as a unit conversion library. You can add any custom transport installation to the Leap installation by placing an appropriate JAR file in a specific directory on the Leap server; however, Leap already includes a generic HTTP transport which can send and receive data over the internet or intranet, and will suffice for many use cases. For more information, see [Service Description](ref_service_service_description.md).
-   **Service Descriptions** – The Service Description provides the interface for a Service Transport. A Service Description is usually described by an XML file, although it is also possible to programmatically create a Service Description. The Service Description specifies a service's name, description, input parameters, and output parameters. These attributes are what appear to the application designer when they are hooking up services to a Leap application.
-   **Data Mapping** – Each service description can contain an optional “mapping” component which describes how the data coming from the Service Transport can be mapped to the outputs defined in the Service Description, or vice versa. The advantage of the mapping component is that it allows multiple Service Descriptions, each with its own name, description, input, and outputs to use to use the same generic transport. By using XPath-like references, the mapping component supports the mapping of complex data structures such as an XML document. The mapping of constant values is also supported.
-   **Service Configuration** – The Service Configuration is another layer of mapping meant for application designers. It maps items in the form to the inputs and outputs of the Service Description. The application designer is responsible for creating service configurations and connecting form items to the service inputs and outputs. Service configurations are stored inside the application.

## Supporting documents { .section}

Use the following documents to gain a better understanding of the steps required to expose a service to Leap.

**Understanding the HTTP transport** – The HTTP Service Transport provides a mechanism to communicate with HTTP servers. The transport allows configuration of the URL to request, HTTP method to use, query parameters, and request headers. When combined with the service mapping engine of Leap, the HTTP Service Transport can extract data from an HTTP response and make it available to your application. The HTTP Service Transport can be used to communicate with any standard HTTP server. While there are some limits on the capabilities of the HTTP Service Transport, it is all that is needed to communicate with a basic HTTP server, or RESTful service, in most cases. For more information, see [HTTP Service Transport](ref_service_http_service_transport.md)

**Creating and deploying service descriptions** – The Service Description provides an interface to Leap mapping interface, and an interface to a Service Transport. For more information on creating Service Descriptions, see [Service Description](ref_service_service_description.md)

**Parent topic:**[Incorporating web services into your applications](cr_using_apps_as_services_toc.md)

