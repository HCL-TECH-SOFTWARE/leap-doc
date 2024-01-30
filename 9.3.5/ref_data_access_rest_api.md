# Data access REST API {#ref_rest_public_REST_API .reference}

The data access REST API exposes operations on application submitted data, also known as records.

The data captured by an HCL Leap application is stored in a relational database. Leap provides secure access to that data through the View Data function, which allows filters and searches, and also allows data to be exported for analysis and reports. When accessing the data using the API, all security permissions as defined in the Access rules for the application are enforced.

All examples in this documentation use the program curl, which is available on most Linux™ systems, and can be downloaded for Windows™. However, you can use any tool or library for calling the REST API. For example, the Poster add-on for FireFox is useful for experimenting with the REST API.

To get the Swagger definition for the entire Data Access REST API, use /apps-basic/anon\|secure/org/data/swagger.json. To get the Swagger definition for a given application and form, use /apps-basic/anon\|secure/org/data/\{app\_uid\}/\{form\_id\}/swagger.json.

|URL|HTTP Verb Header|Action Name|
|---|----------------|-----------|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}|GET|List|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/\{record-uid\}|GET|Retrieve|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}?freedomIdentifyKey=\{x\}|POST|Create|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/\{record-uid\}?freedomIdentifyKey=\{x\}|PUT|Update|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/\{record-uid\}?freedomIdentifyKey=\{x\}|DELETE|Delete|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/metadata|GET|Metadata|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/attachment/\{attachment-uid\}|GET|Retrieve Attachment|
|/apps-basic/secure\|anon/org/data/\{app-uid\}/\{form-id\}/attachment/|POST|Create Attachment|

-   **app-uid**: is the UID of the application
-   **form-id**: is the ID of the form
-   **record-uid**: is the UID of the record
-   **attachment-uid**: is the UID of the attachment
-   **x**: is a randomly generated, difficult to guess single-use numerical value

-   The context for the REST API \(/apps-basic/\) is different from accessing Leap in the browser \(/apps/\).
-   The /apps-basic/ context uses basic authentication rather than form-based authentication.
-   The credentials used for authentication must match the users and permissions specified by the application designer in the **Access** tab. Each form and stage can have different permissions set for each REST API action.
-   Use /anon if your applications allow anonymous access.

All dates, times, and timestamps must be listed in ISO 8601 format.

-   **[List](ref_data_rest_api_list.md)**  
This action retrieves a list of records.
-   **[Retrieve](ref_data_rest_api_retrieve.md)**  
This action retrieves a single record.
-   **[Create](ref_data_rest_api_create.md)**  
This action creates new records.
-   **[Update](ref_data_rest_api_update.md)**  
This action updates an existing record.
-   **[Delete](ref_data_rest_api_delete.md)**  
This action deletes an existing record.
-   **[Metadata](ref_data_rest_api_metadata.md)**  
This JSON-only action retrieves a description of the items in your form.
-   **[Retrieve Attachment](ref_data_rest_api_retrieve_attachment.md)**  
This action retrieves a single attachment.
-   **[Create Attachment](ref_data_rest_api_create_attachment.md)**  
This action creates a single attachment.

**Parent topic:**[REST API reference](ref_rest_api_ref.md)

