# Integrating your application with existing HCL Leap applications {#definingaservicetotheexperiencebuilder .concept}

Each Leap application can be used within another Leap applications as a service.

You can use another application to provide data to populate a drop-down menu on your form. Or, you can search a list of products that are maintained by another application. The ability to share data is a powerful feature of Leap.

To use an application as a service, the designer of an application must set the requisite permissions on the **Access** tab of the application. Access can be set for **Read**, or **Read/Write**. If you set **Read** access, other applications are able to Retrieve and Search information from a specific application. If you set **Read/Write** access, other applications are able to Retrieve, Search, Delete, and Submit information to and from a specific application. For more information about setting permissions, see [Defining permissions to share data with other applications](se_permission_for_sharing_data_with_other_apps.md).

**Note:** When you use another Leap application as a service, mandatory items must be explicitly mapped in the service mapping Inputs and Outputs. Default Items in the form do not satisfy the mandatory requirement as they are not evaluated on the server. If any value is marked as mandatory, it must have a value that is mapped to it in the mappings dialog.

When mapping input parameters, each target has a Search Operator that can change how the inputs are interpreted. For example, you can apply a search operator to create an assignment that links the input with the target, and the operator. To apply the operator, you have to set the **View** to constant and then type the operator keyword in the editable field. The following table contains the list of available search operators.

|Search Operators|Description|
|----------------|-----------|
|**equals**|Equal to|
|**notequals**|Not equal to|
|**lt**|Less than|
|**lte**|Less than or equal to|
|**gt**|Greater than|
|**gte**|Greater than or equal to|
|**Endswith**|The target ends with|
|**Startswith**|The target starts with|
|**contains**|The target contains|

The services also provide access to metadata about the records, such as author, creation time, and the current stage. When you call these services, metadata can be used to filter the results.

The search results can be sorted by form data, such as a field in an application, or by some metadata, such as the lastUpdated time. The default sort order is ascending. To change it to descending, you must prefix your sort field with “DESC”. For example, the following string sorts ascending, `"F_Name"`. The following string sorts descending, `"DESCF_Name"`.

The following values are available for you to use when you are searching with metadata:

|Metadata field|Sort key|
|--------------|--------|
|Last update time|`"lastUpdated"`|
|Author name|`"itemAuthor"`|
|Stage name|`"flowState"`|
|Line ID|`"dbId"`|

You can also limit the results by setting a Page Size that limits how many entries you return, or a Page, which limits pages to return. If you do not provide paging values, then all records that meet your filters are returned.

To see the list of applications available as services select the HCL Leap Applications entry in the **Service Catalog** list. A list of all applications and methods available for Service mapping is shown. Each application can expose the following methods that are based on Access settings:

Retrieve
:   Use **Retrieve** retrieve a single record from another application. For example, use **Retrieve** to pre-populate information that is based on an employee serial number that is entered by the user into the form. The retrieve returns a single row, and cannot be mapped to a repeating or list item.

Search
:   Use **Search** to return a list of records from another application that meets the search criteria. For example, use **Search** to populate a drop-down with a list of values from another Leap application. The results from a search must be mapped to a repeating/list, drop-down, or table item.

Delete
:   When **Delete** service method is called, it deletes the record in the target application that meets the supplied parameters. Use this method with caution as there is no way to retrieve the data after the record is deleted.

Create
:   The **Create** method is used to create a record in the target application. **Create** replicates a user interacting with, and submitting, the target form.

Update
:   The **Update** method is used to update an existing record in the target application. **Update** replicates a user interacting with, and submitting changes to a record in the target form

**Parent topic:**[Incorporating web services into your applications](cr_using_apps_as_services_toc.md)

