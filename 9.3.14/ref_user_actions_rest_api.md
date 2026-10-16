# User Actions REST API

A REST endpoint for executing user actions.

## Authentication

All REST API calls must be made by an authenticated user who is assigned to the [AdministrativeUsers](in_leap_roles.md#administrativeusers) role. Use basic authentication when exercising the API through code. Basic authentication requires a Base64-encoded string containing the username and password.

## REST actions

The following table lists the types of actions that are available and the URLs associated with those actions.

|Endpoint|HTTP Verb|ActionName|
|---|---------|----------|
|/{{apiContext}}/secure/org/admin/user|PUT|decommission|
|/{{apiContext}}/secure/org/admin/user|PUT|updateUser|

## Decommission

Removes all data from the user record that can be linked to a person.  The `login_id` and `display_name` will be changed to a value like "anonxxxxxx" and `email` will be deleted.  You must provide the login id of the user record to modify.

You can find user login id:

{% if isLeap %}
- by accessing the database directly in the `LOGIN_ID` column of the FREEDOM.USERS table.
{% endif %}
{% if isDLeap %}
- by accessing the user record in the Domino directory
{% endif %}

Providing an invalid login id will result in a 404 error.

**Method:** `PUT`

**Parameters**
|Field|Type|Required|Description|
|---|---------|----------|------|
|loginId|string|yes|Login id of the user to decommission|
|action|string|yes|Must be `decommission`|

**Sample payload:**

```
{
  "action": "decommission",
   "loginId" : "ssmith"
}
```

**Sample response:**

```
{
    "newLoginId": "anon858826"
}
```

## Update User

Used to change the display name or email of a user.

!!!note
    When a user logs in, their display name and email address are verified against the configured user repository.  If the user detail is different, {{shortLeapProductName}} will update its local record.  The primary purpose for this function is to force the user information to update rather than waiting till the user accesses the system.

You only need to provide the attribute that you are changing, you are not required to provide both email and displayName.

The request must be made by a user account that is part of the [AdministratorUsers](in_leap_roles.md#administrativeusers) group.

**Method:** `PUT`

**Parameters**
|Field|Type|Required|Description|
|---|---------|----------|------|
|loginId|string|yes|Login id of the user to update|
|action|string|yes|Must be `updateUser`|
|email|string|no|New email address|
|displayName|string|no|New display name|

**Sample Payload:**

```
{
    "loginId": "fford",
    "action": "updateUser",
    "email": "fford@acme.com",
    "displayName": "Frank Gerald Ford"
}
```

**Sample Response:**

```
{
    "actionResult": {
        "loginId": "fford",
        "displayName": "Frank Gerald Ford",
        "success": true,
        "email": null
    }
}
```


**Parent topic:** [REST API reference](ref_rest_api_ref.md)