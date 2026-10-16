# My Tasks REST API

My Tasks REST API provides the records that have been assigned to the logged on user.

To access the api definition in the Swagger UI, use ../{{context}}/open/swagger-ui/index.html?url=%2Fsecure%2Forg%2Ftasks%2Fopenapi.json.

## Authentication

All REST API calls must be made as an authenticated user. You must use basic authentication if you want to exercise the API with code. The primary mechanism for basic authentication is to use a Base64 encoded string for the username and password.

## REST actions

The following table lists the types of actions that are available and the URLs associated with those actions.

|URL|HTTP Verb|ActionName|
|---|---------|----------|
|/{{apiContext}}/secure/org/tasks|GET|list|


**Parent topic:** [REST API reference](ref_rest_api_ref.md)