# Configuring {{msEntraName}} for Leap { #Azure .concept}

## Prerequisites

- A {{msEntraName}} tenant must be set up before proceeding
- Access to the IBM Integrated Solutions Console
- Leap needs to be working and installed on IBM WebSphere or OpenLiberty
- Leap must be secured with TLS and accessed over the https protocol
- Access to the operating system where HCL Leap is installed
- Access to the {{msEntraName}} Portal, with access to create an App Registration
- Users in {{msEntraName}} must have an email attribute to be shared with Leap


## Steps for the configuration:

1. Register HCL Leap as an application in the {{msEntraName}} tenant.

2. Create a client secret for the {{msEntraName}} application.

3. Define the application permissions.


## Registering Leap application with {{msEntraName}}

You must register an application on your {{msEntraName}} tenant.  For details, refer to [Register an application](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app?tabs=certificate%2Cexpose-a-web-api).

During the app registration you must supply a redirect URI, it should be set to https://[myLeapServer]/oidcclient/redirect/oidc

!!!note
    Replace [myLeapServer] with your Leap server hostname


## Create a client secret

The **client secret id** and **client secret value** are used to retrieve an access token for all requests to {{msEntraName}}.

Perform the steps detailed below to create a client secret.

1. Login to {{msEntraName}} admin center.
2. Browse to **Identity** > **Applications** > **App registrations**, then select your application.
3. Select **Certificates & secrets**.
4. Select **Client secrets**, and then select **New client secret**.
5. Provide a description of the secret, and a duration.
6. Select **Add**.

!!!note
    The HCL Leap integration with {{msEntraName}} must use a client secret and does not support using certificates at this time.


## Define application permissions

The minimum set of permissions that are required for Leap to interact with {{msEntraName}} are **User.ReadBasic.All**, **Group.Read.All**, **openid**, and **profile**.

Perform the steps detailed below to define the application permissions.

1. Login to {{msEntraName}} Admin.
2. Navigate to **Identity** > **Applications** > **App registrations**, then select your application.
3. Select **API Permissions**.
4. Click **Add a Permission**.
5. Click **Microsoft Graph**.
6. Click **Application permissions**.
7. In the search field, type "User.Read", select **User.ReadBasic.All** and click **Add permissions**.
8. Repeat steps 4-6.
9. In the search field, type "Group", select **Group.Read.All** and click **Add permissions**.
10. Repeat steps 4-5.
11. Click **Delegated permissions**. Expand **OpenId permissions**, select **openid** and **profile** and click **Add permissions**.

**Parent topic:** [Integrating with {{msEntraName}}](azure_toc.md)