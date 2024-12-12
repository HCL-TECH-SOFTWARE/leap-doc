# Configuring Leap with OIDC 

This topic describes how to configure an HCL Leap server that was deployed using Helm with an OpenID Connect identity provider.

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

The properties that you need to specify may differ based on your identify provider. For additional information, see the [Open Liberty documentation on OpenID Connect](https://openliberty.io/docs/latest/reference/config/openidConnectClient.html).

Before moving on from this step:

-   Verify that the discoveryEndpointURL is valid by opening it in a browser prior to entering it in the yaml file.
-   Update the clientSecret with the proper value obtained from your IDP

The following snippet is an example of an OIDC definition:

```yaml
configOverrideFiles:
  . . .
  openIdConnect: |
    <server description="leapServer">
      <openidConnectClient id="oidc"
        clientId="hcl-leap-oidc-client"
        clientSecret="clientSecretHash"
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
```
General Notes:  

- `realmName`: Defines a qualify that can be used to refer to users and groups from this OIDC config
- `groupIdentifier`: The property of the token that contains the user's group assignments

Microsoft Azure AD Notes:  

- `scope`: A value of `"openid profile"` is required to get the `preferred_username` claim, which is a reasonable claim to use for `userIdentityToCreateSubject`. The application registration in Azure AD is required to have the "openid" and "profile" permissions.
- `groupIdentifier`: Recommended value is `"groups"`; however, this might depend on the Azure AD environment
- `discoveryEndpointUrl`: Is likely to be `https://login.microsoftonline.com/[tenant id]/v2.0/.well-known/openid-configuration`


For more details on defining a server customization, see [Open Liberty server customizations](helm_open_liberty_custom.md).


## Add config properties related to OIDC config { #section_r3z_knt_b1c .section }

The following properties must be set to complete the OIDC configuration:

-   userLookups - By setting this to false it will disable user lookups, which is not available when configured with OIDC.
-   userGroups - By setting this to false it will disable group lookups, which is not available when configured with OIDC.
-   postLogoutRedirectURL - This is the URL to which Leap will redirect the browser after a user chooses to log out. This is necessary to complete the loop with the OIDC IDP.
-   reauthOnFailedRequest, reauthInNewWindow - When the user's session expires, these settings enable the user to reauthenticate in a pop-up window and not lose any unsaved work

```yaml
configuration:
  leap:
    . . .
    leapProperties: |
      ibm.nitro.NitroConfig.userLookup=false
      ibm.nitro.NitroConfig.userGroups=false 
      ibm.nitro.NitroConfig.reauthOnFailedRequest=true 
      ibm.nitro.NitroConfig.reauthInNewWindow=true 
      ibm.nitro.LogoutServlet.postLogoutRedirectURL=https://myoidcServer.com/realms/Leap/protocol/openid-connect/logout?client_id=hcl-leap-oidc-client&post_logout_redirect_uri=https://myLeapServer.com/apps/secure/org/ide/manager.html
```

For more details on setting Leap properties, see [Leap properties](helm_leap_properties.md).

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

**Parent topic:** [Kubernetes Helm deployment](kubernetes_helm_deployment.md)