# Extending 

You can extend the functionality of {{fullProductName}} through the use of customized cascading style sheets, Javascript APIs, and REST APIs, and Service Oriented Architecture modifications.

**Service Description:**
{{shortProductName}} has a powerful, and extensible, Service Oriented Architecture \(SOA\) integration feature. The Service Description provides a human-readable view on a service that uses a Service Transport. Service Descriptions are files stored on the server that make a service available to {{shortProductName}} when designing an application. For more information about creating a Service Description, see [Service Oriented Architecture](cr_using_apps_exposing_service_to.md).

**JavaScript API:**
{{fullProductName}} provides a JavaScript™ API allowing designers to extend the customization provided by formulas, stages, rules, and services. The JavaScript is triggered on events tied to the user interface items in an application. The API has full access to the “Business Object” of the application. All JavaScript is covered by the security sandbox model. See the [JavaScript API Reference](ref_javascript_api.md#) document for full details on the available API methods, business object, security model, and event model.

**Data Access REST API:** 
The data captured by {{fullProductName}} is stored in a database. {{shortProductName}} provides secure access to that data through the **View Data** UI, which supports filtering, searching, and exporting for analysis. If you need direct access for analysis or reporting, you can use the provided REST API. All security permissions defined in the application's Access rules are enforced when accessing data through the API. For full details on this API, see [Data access REST API](ref_data_access_rest_api.md).

{% if isLeap %}
**Data Integrity:**
{{fullProductName}} includes built-in server-side validation of incoming data, detecting issues such as missing required fields or values that violate constraints like data type, length, format, or range. {{shortProductName}} can also be extended with additional business rules tailored to your organization’s needs.
{% endif %}

-   **[Using custom style sheets](ex_css_toc.md)**  
{{fullProductName}} allows the use of custom CSS themes that can be uploaded into an application to style the user interface to meet customer needs.
{% if isLeap %}
-   **[Adding services](services_toc.md)**  
The following topics describe how to add services to your {{shortProductName}} applications.
-   **[Adding custom data integrity logic](ex_add_custom_data_integrity_rules.md)**  
The following topic describes how to add customized server-side validation of incoming data.
{% endif %}

