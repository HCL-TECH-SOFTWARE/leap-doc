# Swagger UI

The open source [Swagger UI](https://swagger.io/tools/swagger-ui/) is embedded in {{shortProductName}} to simplify and accelerate integration using {{shortProductName}}'s REST APIs.  This page allows you to inspect and test different REST API operations.

Direct links to this page for application and form operations are available in the **URL Links** dropdown of an expanded application on the Manage page.

To load other api definitions modify the 'url' parameter. 

For example: 

`http://myLeapServer.com/{{context}}/open/swagger-ui/index.html?url=%2F{{context}}%2Fsecure%2Forg%2Fapp%2Fopenapi.json`


## Supported Definitions

This section describes the API definitions that are currently supported.

### Generic Application Operations

Describes the programmatic operations that can be performed for any {{shortProductName}} applications.

The URL to access this definition is: 

`http://myLeapServer.com/{{context}}/open/swagger-ui/index.html?url=%2F{{context}}%2Fsecure%2Forg%2Fapp%2Fopenapi.json`

### Specific Application Operations

Describes the programmatic operations that can be performed for a specific {{shortProductName}} application.

The URL to access this definition is:

`http://myLeapServer.com/{{context}}/open/swagger-ui/index.html?url=%2F{{context}}%2Fsecure%2Forg%2Fapp%2F22b68b24-d2ad-4477-8e1b-88dc1597d8b2%2Fopenapi.json`

### Application Statistics

Describes the programmatic operations that return statistics for all applications on the server.

The URL to access this definition is:

`http://myLeapServer.com/{{context}}/open/swagger-ui/index.html?url=%2F{{context}}%2Fsecure%2Forg%2Fadmin%2Fapps%2Fopenapi.json`

{% if isLeap %}
### My Tasks

Describes the programmatic operations that return the tasks assigned to a specific user.

The URL to access this definition is:

`http://myLeapServer.com/{{context}}/open/swagger-ui/index.html?url=%2F{{context}}%2Fsecure%2Forg%2Ftasks%2Fopenapi.json`

{% endif %}

## Limitations

- You must be logged in for the Swagger UI to properly access and load the api definitions (openapi.json). If the page displays ***"Failed to load API definition"***, it could be that you are not authenticated or that your session has timed out. Reauthenticate to restore access to the api definition.

- The Swagger UI can only be used to load openapi.json files that are on the same server. Loading external files has been blocked.

- Only users with Administrator role (or a role with "create" permission) may access the api definition for a specific application.

**Parent topic:** [REST API reference](ref_rest_api_ref.md)
