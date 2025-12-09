# User Actions REST API

A REST endpoint for executing user actions.

## Authentication

All REST API calls must be made by an authenticated user who is assigned to the [AdministrativeUsers](in_leap_roles.md#administrativeusers) role. Use basic authentication when exercising the API through code. Basic authentication requires a Base64-encoded string containing the username and password.

## REST actions

The following table lists the types of actions that are available and the URLs associated with those actions.

|URL|HTTP Verb|ActionName|
|---|---------|----------|
|/apps-admin/secure/org/admin/user|PUT|decommission|