# Application statistics REST API { #app_stats_restapi .concept }

Application statistics REST API exposes statistics data on all applications, such as an application's last updated date, record count, attachment size etc.

Statistics are collected by a timer task which can be configured by an administrator using [Configuration properties](co_configuration_properties.md).

To access the api definition in the Swagger UI, use ../{{context}}/open/swagger-ui/index.html?url=%2fsecure%2forg%2fadmin%2fapps%2fopenapi.json.

-   Authentication

    All REST API calls must be made as an authenticated user in Administrator or Super Administrator role. If you want to exercise the API with code, you may use basic authentication. The primary mechanism is to use basic authentication where the username and password are a Base64 encoded string.

-   REST actions

    The following table lists the types of actions that are available and the URLs associated with those actions.

    |URL|HTTP Verb|ActionName|
    |---|---------|----------|
    |/{{apiContext}}/secure/org/admin/apps|GET|list|
    |/{{apiContext}}/secure/org/admin/apps/\{app-uid\}|GET|app detail|

!!! note
    `{app-uid}` is the UID of the application.


## List { #section_p5n_2bc_kyb .section }

This action retrieves a list of all apps, available query parameters:

-   `forceRefresh`: executes statistics collection on all apps. Default value: `false`

-   `includeForms`: whether includes app forms information in response. Default value: `false`

-   `includeAdmins`: whether includes app administrators information in response. Default value: `false`

-   `format`: \(case sensitive\) acceptable values:
    - JSON: `json` or `application/json`
    - Spreadsheet: `xlsx` or `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
-   `filename`: (optional) only used when `pFormat` is set to `xlsx` format. The file extension must be `.xlsx`.

!!! note
    If this parameter is not specified, the default file name is **app.xlsx**.


## App detail { #section_qwb_qbc_kyb .section }

This action retrieves the details for a single app.

**Parent topic:** [REST API reference](ref_rest_api_ref.md)

