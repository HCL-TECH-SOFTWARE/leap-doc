# Application management REST API {#ref_rest_api_auto_deploy .reference}

The Application management REST API allows for programmatic import, export, upgrade, and delete of Leap applications.

## Authentication { .section}

To get the Swagger definition for the Application management REST API, use /apps-basic/anon\|secure/org/app/swagger.json

All REST API calls must be made as an authenticated user. If you want to exercise the API with code, then, you can use basic authentication. The authenticated user must be a valid user of Leap and must have the appropriate permission. The primary mechanism is to use basic authentication where the username and password are a Base64 encoded string.

## REST actions { .section}

The following table lists the types of actions that are available and the URLs associated with those actions.

|URL|HTTP Verb Header|Action Name|
|---|----------------|-----------|
|/apps-basic/secure/org/app/app-uid/archive?mode=source&submitted=true|GET|Export|
|/apps-basic/secure/org/app/app-uid/archive?replaceEmbeddedData=on&runDatabaseUpgradeNow=on&replaceSubmittedData=on&freedomIdentifyKey=x|POST|Upgrade|
|/apps-basic/secure/org/app?deploy=false&importData=false&freedomIdentifyKey=x|POST|Import|
|/apps-basic/secure/org/app/app-uid?freedomIdentifyKey=x|DELETE|Delete|

## Export { .section}

Exports the defined application as a .nitro\_s file. You can use the following parameters to export the application:

#### `submitted=true` 
Can be set to **true** or **false**. **true** returns the application and all submission data that exists in the application.

**Note:** If no value is passed, then the default is **true**.

## Upgrade { .section}

Allows the user to upgrade the content of an application to match the application that is contained in the POST request. You can use the following parameters to upgrade the application:

#### `replaceSubmittedData=off`
Can be **on** or **off**. **on** replaces the existing submission data with the submission data contained in the application being uploaded.

**Note:** The default for replaceSubmittedData is **off**.

#### `freedomIdentifyKey=x`
The value of *x*, must be a randomly generated, difficult to guess, single-use numerical value. The value of this URL parameter must match the value of the freedomIdentifyKey cookie. Requiring a cookie value that matches the URL parameter helps avoid possible browser vulnerabilities. See [Data REST API Delete](ref_data_rest_api_delete.md#) for more information.

The upgraded application must be uploaded to the server as multipart/form-data in the body of the POST.

## Import { .section}

Imports the specified application into the Leap server. The user that performs the import is automatically added as an administrator. You can use the following parameters to import the application:

#### `deploy=false`
Can be set to **true** or **false**. **true** automatically deploys the application as part of the import.

**Note:** The default is **false**.

#### `importData=false`
Can be set to **true** or **false**. **true** imports the submission data, or submitted records, if they were included when the application was exported.

**Note:** The default is **false**.

#### `cleanIds=false`
Can be set to **true** or **false**. **true** removes all groups and users from roles within the imported application ensuring that only the current authenticated user has access to the application.

**Note:** The default is **false**.

#### `freedomIdentifyKey=x`
The value of *x*, must be a randomly generated, difficult to guess, single-use numerical value. The value of this URL parameter must match the value of the freedomIdentifyKey cookie. Requiring a cookie value that matches the URL parameter helps avoid possible browser vulnerabilities. See [Data REST API Delete](ref_data_rest_api_delete.md#) for more information.

The application to be imported must be uploaded to the server as multipart/form-data.

## Delete { .section}

Deletes the specified application from the server.

#### `freedomIdentifyKey=x`
The value of *x*, must be a randomly generated, difficult to guess, single-use numerical value. The value of this URL parameter must match the value of the freedomIdentifyKey cookie. Requiring a cookie value that matches the URL parameter helps avoid possible browser vulnerabilities. See [Data REST API Delete](ref_data_rest_api_delete.md#) for more information.

## Basic Application Flow { .section}

This is the basic flow of an application communicating with the Leap REST API:

1.  Establish a URLConnection with the URL that matches the action you want.
2.  Set the basic authentication credentials into the URLConnection.
3.  Set extra headers or body content if required for the action.
4.  Process the response.

**Parent topic: **[REST API reference](ref_rest_api_ref.md)

