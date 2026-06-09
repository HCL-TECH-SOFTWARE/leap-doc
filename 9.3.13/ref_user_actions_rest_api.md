# User Actions REST API

A REST endpoint for executing user actions.

## Authentication

All REST API calls must be made by an authenticated user who is assigned to the [AdministrativeUsers](in_leap_roles.md#administrativeusers) role. Use basic authentication when exercising the API through code. Basic authentication requires a Base64-encoded string containing the username and password.

## REST actions

The following table lists the types of actions that are available and the URLs associated with those actions.

|URL|HTTP Verb|ActionName|
|---|---------|----------|
|/{{apiContext}}/secure/org/admin/user|PUT|decommission|

## Decommission

Removes all data from the user record that can be linked to a person.  The ```login_id``` and ```display_name``` will be changed to a value like "anonxxxxxx" and ```email``` will be deleted.  You must provide the login id of the user record to modify.

You can find user login id:

{% if isLeap %}
- by accessing the database directly in the ```LOGIN_ID``` column of the FREEDOM.USERS table.
{% endif %}
{% if isDLeap %}
- by accessing the user record in the Domino directory
{% endif %}

Providing an invalid login id will result in a 404 error.

**Method:** ```PUT```

**Sample payload:**

```
{
  "action": "decommission"
   "loginId" : "ssmith"
}
```

**Sample response**

```
{
    "newLoginId": "anon858826"
}
```

**Parent topic:** [REST API reference](ref_rest_api_ref.md)