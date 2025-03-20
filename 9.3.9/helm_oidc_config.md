# Authenticating a Helm deployment with OpenID Connect (OIDC)

This topic describes how to configure an HCL Leap server that was deployed using Helm to authenticate with an external identity provider (IdP) using OpenID Connect (OIDC).

## Configuring Leap with OIDC { #section_lmm_5mt_b1c .section }

Leap can be configured to leverage OpenID Connect \(OIDC\) as the primary authentication mechanism. This means that Leap will be turned into a Relying Party \(RP\) to the specified identify provider \(IDP\). When OIDC is used, the user and group lookup feature of Leap is not available and must be disabled as part of the configuration.

The following tasks must be completed to establish this configuration:

1.  Configure the OIDC identity provider.
2.  Create a secret in Kubernetes container from the IDP server certificate.
3.  Add an OIDC definition as a server customization.
4.  Add configuration properties related to the OIDC configuration.
5.  Restart the pod.

## Configure OIDC identity Provider { #section_zj4_xmt_b1c .section }

Many different identity providers offer OIDC capability. Refer to your chosen identity provider's documentation for more details on configuration.

For detailed steps on configuring {{msEntraName}}, refer to [Configuring Microsoft Entra ID for Leap](azure_config.md).

## Create a secret in Kubernetes container from the IDP certificate { #section_cch_1nt_b1c .section }

As part of the configuration process for your identify provider, you will have created or obtained a digital certificate for configuring HTTPS. This certificate will also need to be deployed to Leap so that the two servers can communicate with each other.

!!! note
    The SSL certificate \(.crt\) and public key \(.key\) should be in PKCS12 format.

After copying the `.key` and `.crt` to the kubernetes image, create a secret using the following command:

```text
kubectl -n myns create secret tls oidccert --key="/tmp/oidc.key" --cert="/tmp/oidc.crt"
```

Next, this secret can be referenced in the yaml file:

```yaml
configuration:
  leap:
    . . .
    customCertificateSecrets:
      keycloakCert: "keycloakcert"
```

For more information, see to [Provide admin user a custom secret](helm_admin_customsecret.md).

## Add OIDC definition as a server customization { #section_vxv_fnt_b1c .section }

To configure OIDC you must define the `openidConnectClient`.  Take note of the following attributes when creating the `openidConnectClient` configuration:

The **clientId** will refer to the environment variable, for the client secret id, that is created as a result of the Kubernetes secret.  The format is <aliasName>_key.

The **clientSecret** will refer to the environment variable, for the client secret value, that is created as a result of the Kubernetes secret.  The format is <aliasName>_key.

The **scope** must be set to "openid profile" to retrieve the preferred_username claim, which is a suitable claim to use for userIdentityToCreateSubject. The application registration in Azure AD is required to have the "openid" and "profile" permissions.

For **groupIdentifier**,  the recommended value is **groups**, though this may vary depending on the {{msEntraName}} environment.

The **discoveryEndpointUrl** is likely to be https://login.microsoftonline.com/[tenant id]/v2.0/.well-known/openid-configuration

The **realmName** is used when referencing members of this repository for role mapping.

The properties that you need to specify may differ based on your identify provider. For additional information, see the [Open Liberty documentation on OpenID Connect](https://openliberty.io/docs/latest/reference/config/openidConnectClient.html).

Before moving on from this step:

-   Verify that the **discoveryEndpointURL** is valid by opening it in a browser prior to entering it in the yaml file.
-   Update the **clientId** and **clientSecret** with the proper values obtained from your IDP, by [using a custom secret](helm_admin_customsecret.md).

The entire configuration may look like the example provided:

```yaml
configuration:
  leap:
    . . .
    configOverrideFiles:
    . . .
    openIdConnect: |
      <server description="leapServer">
        <openidConnectClient id="oidc"
          clientId="${OIDC_CLIENT_ID}"
          clientSecret="${OIDC_CLIENT_SECRET}"
          signatureAlgorithm="RS256"
          authFilterRef="interceptedAuthFilter"
          mapIdentityToRegistryUser="false"
          httpsRequired="true"
          scope="openid"
          realmName="LeapOidc"
          groupIdentifier="group_membership"
          userIdentityToCreateSubject="preferred_username"
          discoveryEndpointUrl="https://myoidcserver:8443/realms/Leapdev/.well-known/openid-configuration">
        </openidConnectClient>
        <authFilter id="interceptedAuthFilter">
          <requestUrl id="authRequestUrl" matchType="contains" urlPattern="/apps/secure"/>
        </authFilter>
      </server> 
. . .
```

For more details on defining a server customization, see [Open Liberty server customizations](helm_open_liberty_custom.md).


## Add config properties related to OIDC config { #section_r3z_knt_b1c .section }

The following properties must be set to complete the OIDC configuration:

-   **postLogoutRedirectURL** - This is the URL to which Leap will redirect the browser after a user chooses to log out. This is necessary to complete the loop with the OIDC IDP.
-   **reauthOnFailedRequest**, **reauthInNewWindow** - When the user's session expires, these settings enable the user to reauthenticate in a pop-up window and not lose any unsaved work

For more details on setting Leap properties, see [Leap properties](helm_leap_properties.md).

```yaml
configuration:
  leap:
    . . .
    leapProperties: |
      ibm.nitro.NitroConfig.reauthOnFailedRequest=true 
      ibm.nitro.NitroConfig.reauthInNewWindow=true 
      ibm.nitro.LogoutServlet.postLogoutRedirectURL=https://myoidcServer.com/realms/Leap/protocol/openid-connect/logout?client_id=hcl-leap-oidc-client&post_logout_redirect_uri=https://myLeapServer.com/apps/secure/org/ide/manager.html
```

### Config with no LDAP or {{msEntraName}}

If the OIDC configuration does not include an LDAP directory or {{msEntraName}}, then you must define the following properties that will turn off user/group lookup features of Leap:

-   **userLookup** -  Set to **false** if LDAP directory is not available . Set to **true** if an LDAP is available and configure the <openidConnectClient mapIdentityToRegistryUser="true" userIdentityToCreateSubject="[attribute that matches to LDAP]" ...>
-   **userGroups** - Set to **false** if group information is not available.  Set to **true** if ID token contains group information. If true, ensure <openidConnectClient groupIdentifier="..."> matches correct claim in the ID token
- **userLookupGroups** - Set to **false** if LDAP directory is not available or if doesn't support searching for groups.  Set to **true** if directory has group information; Ensure that <openidConnectClient groupIdentifier="..."> matches to the attribute that identifies groups in the LDAP

```yaml
configuration:
  leap:
    . . .
    leapProperties: |
      ibm.nitro.NitroConfig.userLookup=false
      ibm.nitro.NitroConfig.userGroups=false
      ibm.nitro.NitroConfig.userLookupGroups=false
```

## Referencing Users and Groups in Security Role Mapping 
To assign a user or group from OIDC to one of the Leap roles (AdministrativeUsers, EditApplicationUsers, UseApplicationUsers) you must use their access id.  The access id is made up of the realmName (defined in the 'openidConnectClient' definition) and the user or group name.  

To assign a user from OIDC to a Leap security role you would use {realmName}/{userName}:
```yaml
configuration:
  leap:
    ...
    roleMapping:
      ...
      EditApplicationsUsers:
        MappedUsersAccessIDs:
        - LeapOidc/john.oidc
```

To assign a group from OIDC to a Leap security role you would use {realmName}/{groupName}:
```yaml
configuration:
  leap:
    ...
    roleMapping:
      ...
      EditApplicationsUsers:
        MappedGroupsAccessIDs:
        - LeapOidc//Group1
```
!!! note
    there is an extra slash in the group name because that is part of the definition in the IDP used for this example. Other IDPs may differ in how they define the group name, if in doubt leverage the logging trace string to identify the correct value.

## Troubleshooting
To get more information about how Liberty perceives the logged in user, add the trace string 'com.ibm.ws.security.authentication.*=all'.  This will provide useful information for understanding the user and group values.  An example output in the trace.log, after logging in, looks like:

```text
    Principal: WSPrincipal:john.oidc
    Public Credential: com.ibm.ws.security.credentials.wscred.WSCredentialImpl@cb847b2d,realmName=LeapOidc,securityName=john.oidc,realmSecurityName=LeapOidc/john.oidc,uniqueSecurityName=john.oidc,primaryGroupId=null,accessId=user:LeapOidc/john.oidc,groupIds=[group:LeapOidc//Group2]
    Private Credential: IDToken:{"exp":1710363581,"iat":1710363281,"auth_time":1710363280,"jti":"f343b1fe-6a9a-482f-a85e-1cf46f4eb1b8","iss":"https://myoidcserver:8443/realms/Leapdev","aud":"hcl-leap-oidc-client","sub":"9b8cd571-5d09-4de2-ba2d-22b985424831","typ":"ID","azp":"hcl-leap-oidc-client","session_state":"fff63a5e-8269-4e69-b4c3-9d4135c028da","at_hash":"ePO9yDI6IGdX1iDG17CNWQ","acr":"1","sid":"fff63a5e-8269-4e69-b4c3-9d4135c028da","group_membership":["/Group2"],"email_verified":false,"realmName":"Leapdev","name":"John Oidc","groups":["default-roles-leapdev","offline_access","uma_authorization"],"preferred_username":"john.oidc","given_name":"John","family_name":"Oidc","email":"john.oidc@acme.com"} 
```
!!! note
    If the groupIds array is empty then the 'openidConnectClient' is not configured properly; the group claim may be missing from the token or the 'groupIdentifier' may not be set to the correct value.

## Restart the pod { #section_zq2_vmt_b1c .section }

After restarting the Leap pod, accessing Leap should redirect you to authenticate using your OIDC IDP.

## Sample {{msEntraName}} Configuration { #sample_entra_config .section }

The following is an example of a Leap configuration against {{msEntraName}} as the IDP using ODIC and with user/group searches enabled.

1. You must [prepare the {{msEntraName}} tenant for Leap](azure_config.md).

2. [Create a kubernetes secret](azure_lookups.md#kubernetes-create-credential-for-leap) that references the {{msEntraName}} application's client secret id and value. In this example, the secret name was "azureAlias".  Provide the name of the secret in the **customSecrets** section of the .yaml file.

    ```
    configuration:
      leap:
        customSecrets:
          azure-credentials: "leap-azure-credentials"
    . . .
    ```

3. Define the Leap properties to enable the user/group searching against {{msEntraName}}.  We have also included the properties that improve the re-authentication experience when a user session expires.

    For further details on the Leap configuration required to integrate with {{msEntraName}}, refer to [Integrating with a Microsoft Entra ID directory](azure_lookups.md).

    ```
    configuration:
      leap:
        . . .
        leapProperties: |
          ibm.nitro.SetupAll.setupStatus = start
          ibm.nitro.NitroConfig.reauthOnFailedRequest=true
          ibm.nitro.NitroConfig.reauthInNewWindow=true
          ibm.nitro.NitroConfig.memberManagerType=ms-azure-ad
          ibm.nitro.NitroConfig.GraphApiMemberManager.credentialAlias=azureAlias
          ibm.nitro.NitroConfig.GraphApiMemberManager.tenantId=11111111-1111-1111-1111-111111111111
          . . .
    . . .
    ```

Define the OIDC configuration for your {{msEntraName}} tenant.

Take note of the following points in creating the `openidConnectClient`:

- **clientId** and **clientSecret** reference the environment variables created as a result of the kubernetes secret
- the **discoveryEndpoint** includes the {{msEntraName}} **tenant id**
- the **realmName** provides a handle that can be used in the **roleMapping** definition

```
configuration:
  leap:
    . . .
    configOverrideFiles:
      azureOidc: |
        <server description="leapServer">
          <openidConnectClient id="oidc"
            clientId="${azureAlias_key}"
            clientSecret="${azureAlias_secret}"
            signatureAlgorithm="RS256"
            authFilterRef="interceptedAuthFilter"
            mapIdentityToRegistryUser="false"
            httpsRequired="true"
            scope="openid profile"
            realmName="LeapOidc"
            groupIdentifier="groups"
            userIdentityToCreateSubject="preferred_username"
            discoveryEndpointUrl="https://login.microsoftonline.com/11111111-1111-1111-1111-111111111111/v2.0/.well-known/openid-configuration">
          </openidConnectClient>
          <authFilter id="interceptedAuthFilter">
            <requestUrl id="authRequestUrl" matchType="contains" urlPattern="/apps/secure" />
          </authFilter>
          <ssl id="defaultSSLConfig" trustDefaultCerts="true" />
        </server>
. . .
```

Define role mappings for users or groups access to Leap

```
configuration:
  leap:
    . . .
    roleMapping:
      EditApplicationsUsers:
        # These are a couple of users provide by the Entra ID sample pack
        # The "LeapOidc/" prefix matches the realmName of the <openIdConnectClient> config
        MappedUsersAccessIDs:
          - LeapOidc/AdeleV@vprl0.onmicrosoft.com
          - LeapOidc/AlexW@vprl0.onmicrosoft.com
        MappedGroupsAccessIDs:
          # "Leap Authors" group
          - LeapOidc/372863bc-001f-42b5-b877-38f6afc4b417
. . .
```

**Parent topic:** [Kubernetes Helm deployment](kubernetes_helm_deployment.md)