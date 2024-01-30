# Extending {#extendingformsexperiencebuilder .concept}

You can extend the functionality of HCL Leap through the use of customized cascading style sheets, Javascript APIs, and REST APIs, and Service Oriented Architecture modifications.

**Service Description:**Leap has a powerful, and extensible, Service Oriented Architecture \(SOA\) integration feature. The Service Description provides a human-readable view on a service that uses a Service Transport. Service Descriptions are files stored on the server that make a service available toLeap when designing an application. For more information about creating a Service Description, see [Service Oriented Architecture](cr_using_apps_exposing_service_to.md).

**JavaScript API:**HCL Leap provides a JavaScript™ API allowing designers to extend the customization provided by formulas, stages, rules, and services. The JavaScript is triggered on events tied to the user interface items in an application. The API has full access to the “Business Object” of the application. All JavaScript is covered by the security sandbox model. See the [JavaScript API Reference](ref_javascript_api.md#) document for full details on the available API methods, business object, security model, and event model.

**Data Access REST API:** The data captured by an HCL Leap application is stored in a relational database. Leap provides secure access to that data through the View Data function, which allows filters and searches, and also allows data to be exported for analysis. You might want to access the data directly for analysis and reporting. To allow this access, we provide a REST API that allows you access the data programmatically. When accessing the data using the API, all security permissions as defined in the Access rules for the application are enforced. For full details on this API, see [Data access REST API](ref_data_access_rest_api.md).

-   **[Using custom style sheets](ex_css_toc.md)**  
HCL Leap allows the use of custom CSS themes that can be uploaded into an application to style the user interface to meet customer needs.
-   **[Adding services](services_toc.md)**  
The following topics describe how to add services to your Leap applications.

