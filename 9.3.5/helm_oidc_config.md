# Configuring Leap with OIDC {#helm_oidc_config .concept}

This topic describes how to configure an HCL Leap server that was deployed using Helm with an OpenID Connect identity provider.

## Configuring Leap with OIDC {#section_lmm_5mt_b1c .section}

Leap can be configured to leverage OpenID Connect \(OIDC\) as the primary authentication mechanism. This means that Leap will be turned into a Relying Party \(RP\) to the specified identify provider \(IDP\). When OIDC is used, the user and group lookup feature of Leap is not available and must be disabled as part of the configuration.

The following tasks must be completed to establish this configuration:

1.  Configure the OIDC identity provider.
2.  Create a secret in Kubernetes container from the IDP server certificate.
3.  Add an OIDC definition as a server customization.
4.  Add configuration properties related to the OIDC configuration.
5.  Restart the pod.

## Configure OIDC identity Provider {#section_zj4_xmt_b1c .section}

Many different identity providers offer OIDC capability. Refer to your chosen identity provider's documentation for more details on configuration.

## Create a secret in Kubernetes container from the IDP certificate {#section_cch_1nt_b1c .section}

As part of the configuration process for your identify provider, you will have created or obtained a digital certificate for configuring HTTPS. This certificate will also need to be deployed to Leap so that the two servers can communicate with each other.

**Note:** The SSL certificate \(.crt\) and public key \(.key\) should be in PKCS12 format.

After copying the `.key` and `.crt` to the kubernetes image, create a secret using the following command:

``` {#codeblock_tjk_knt_b1c}
kubectl -n myns create secret tls oidccert --key="/tmp/oidc.key" --cert="/tmp/oidc.crt"
```

Next, this secret can be referenced in the yaml file:

``` {#codeblock_dyx_2nt_b1c}
configuration:
  leap:
    customCertificateSecrets:
      keycloakCert: "keycloakcert"
```

For more information, see to [helm\_admin\_customsecret.md](helm_admin_customsecret.md).

## Add OIDC definition as a server customization {#section_vxv_fnt_b1c .section}

The properties that you need to specify may differ based on your identify provider. For additional information, see the [Open Liberty documentation on OpenID Connect](https://openliberty.io/docs/latest/reference/config/openidConnectClient.html).

Before moving on from this step:

-   Verify that the discoveryEndpointURL is valid by opening it in a browser prior to entering it in the yaml file.
-   Update the clientSecret with the proper value obtained from your IDP

The following snippet is an example of an OIDC definition:

``` {#codeblock_b5j_jnt_b1c}
configOverrideFiles:
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
            userIdentityToCreateSubject="preferred_username"
            discoveryEndpointUrl="https://myoidcserver:8443/realms/Leapdev/.well-known/openid-configuration">
          </openidConnectClient>
          <authFilter id="interceptedAuthFilter">
            <requestUrl id="authRequestUrl" matchType="contains" urlPattern="/apps/secure|/apps/secured"/>
          </authFilter>
          <httpEndpoint id="defaultHttpEndpoint"
             host="*"
             httpPort="9080"
             httpsPort="9443">
             <samesite none="*" />
        </server> 
```

For more details on defining a server customization, see [helm\_open\_liberty\_custom.md](helm_open_liberty_custom.md).

## Add config properties related to OIDC config {#section_r3z_knt_b1c .section}

The following properties must be set to complete the OIDC configuration:

-   hasUserLookups - By setting this to false it will disable user lookups, which is not available when configured with OIDC.
-   hasUserGroups - By setting this to false it will disable group lookups, which is not available when configured with OIDC.
-   postLogoutRedirectURL - This is the URL to which Leap will redirect the browser after a user chooses to log out. This is necessary to complete the loop with the OIDC IDP.

``` {#codeblock_hbq_pnt_b1c}
configuration:
   leap:
     leapProperties: |
       ibm.nitro.NitroConfig.hasUserLookup=false
       ibm.nitro.NitroConfig.hasUserGroups=false 
       ibm.nitro.LogoutServlet.postLogoutRedirectURL=https://myOIDCServer.com/realms/Leap/protocol/openid-
                 connect/logout?client_id=hcl-leap-oidc-client&post_logout_redirect_uri=https://myLeapServer.com/apps/secure/org/ide/manager.html
```

For more details on setting Leap properties, see [helm\_leap\_properties.md](helm_leap_properties.md).

## Restart the pod {#section_zq2_vmt_b1c .section}

After restarting the Leap pod, accessing Leap should redirect you to authenticate using your OIDC IDP.

