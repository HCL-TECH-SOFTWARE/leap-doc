# SAML configuration { #helm_saml_config .concept}

The Leap Helm chart and container offer a basic SAML configuration through the Helm values. 

To enable SAML you must:
- pass the IdP Metadata of the identity provider
- enable the SAML feature
- (optional) define an authentication filter

## Define idpMetadata

The IdP Metadata will be implemented as a Kubernetes secret. 

1. Copy the IdP Metadata from the identify provider into a file called 'idpMetadata.xml'

2. Create a kubernetes secret from the idpMetadata.xml file.

```text
# Syntax
kubectl create secret generic saml-metadata --from-file=path/idpMetadata.xml --namespace=<namespace>

# Example
kubectl create secret generic saml-metadata --from-file=./idpMetadata.xml --namespace=myns
```

3. Add the secret to the ['customSecrets' property](helm_admin_customsecret.md#as_key_file) of the yaml file.

```yaml
. . .
configuration:
  leap:
    . . .
    customSecrets:
      saml-metadata: "saml-metadata"
    . . .
. . .
```

!!! note
    The idpMetadata.xml file will be placed in the /mnt/customSecrets/saml-metadata directory on the pod.

## Enable SAML

The SAML feature must be enabled. Optionally an authentication filter can be specified that determines which requests are redirected to SAML.  You can configure more than one SAML definition and authentication filter.

The following attributes must be defined:

**id** - can be any url-safe string, ```'defaultSP'``` is the default.  If modified, you will need to update the 

**enabled** - value must be set to "true"

**idpMetadata** - The location where the idpMetadata.xml file can be found. This should be set to ```/mnt/customSecrets/saml-metadata/idpMetadata.xml```


Additional optional attributes:

**allowCreate** - Allow the IdP to create a new account if the requesting user does not have one. Default is false.

**allowCustomCacheKey** - Allow generating a custom cache key to access the authentication cache and get the subject.

**authFilterRef** - The id of the authFilter that defines the URL pattern that should be authenticated by SAML. If an authentication filter is not applied, all requests will be redirected to SAML for authentication.

**disableLtpaCookie** - The default setting is true, which disables LTPA and creates a session cookie scoped to the server instead. To create an LTPA cookie, set this to false. 

!!! note
    Additional steps are required to configure LTPA.

**mapToUserRegistry** - Valid values are:
- No : Do not map a SAML identity to a user or group in the registry
- User : Map a SAML identity to a user defined in the user registry
- Group : Map a SAML identity to a group defined in the user registry

!!! note
    If mapping SAML identity to a user in the user registry, the user registry login attribute must match what is returned from the SAML provider.

**spHostAndPort** - Specifies the hostname and port number by which the IdP addresses this SAML service provider. Use this attribute if the browser needs to be redirected to a router or proxy server instead of directly connecting to the service provider. The format for the value for this attribute is (scheme)://(proxyOrRouterHost):(proxyOrRouterPort). For example, https://myRouter.com:443.

If you require additional features to integrate with your SAML implementation, refer to the [Open Liberty SAML documentation](https://openliberty.io/docs/latest/reference/config/samlWebSso20.html) for other SAML-related properties.

### Simple SAML Configuration

```yaml
. . .
configuration:
  leap:
    . . .
    configOverrideFiles:
      . . .
      samlEnableOverride: |
         <server description="leapServer">
           <samlWebSso20
                 id="defaultSP"
                 enabled="true"
                 idpMetadata="/mnt/customSecrets/saml-metadata/idpMetadata.xml"
                 spHostAndPort="https://myserviceprovider:9443"
                 mapToUserRegistry="User">
           </samlWebSso20>
         </server>
. . .
```

### SAML Configuration with Authentication Filter

The ```authFilter``` can be used to define url patterns that should be authenticated using SAML.  If the ```authFilter``` is not specified then ALL url patterns are authenticated using SAML.

```yaml
. . .
configuration:
  leap:
    . . .
    configOverrideFiles:
      . . .
      samlEnableOverride: |
         <server description="leapServer">
           <samlWebSso20
                 id="defaultSP"
                 enabled="true"
                 idpMetadata="/mnt/customSecrets/saml-metadata/idpMetadata.xml"
                 spHostAndPort="https://myleapserver:9443"
                 authFilterRef="defaultAuthenticationFilter"
                 mapToUserRegistry="User">
           </samlWebSso20>
           <authFilter id="defaultAuthenticationFilter">
             <requestUrl urlPattern="/apps*" id="default"></requestUrl>
           </authFilter>
         </server>
. . .
```

**Parent topic:** [Open Liberty server customizations](helm_open_liberty_custom.md)

