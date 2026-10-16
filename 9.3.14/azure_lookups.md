# Enabling user/group searching using {{msEntraName}}

Several Leap features that require the ability to verify the existence of a user or group. These features include:

- When deploying or saving an application as the Leap author
- When adding users or groups to a role on the Access or Permissions tabs
- When using a name picker field to search for a user or group
- When dynamically assigning a user or group to a role using the “Assign User/Group”  submit activity
- When submitting a form

Leap can be configured to interact with {{msEntraName}}, formerly known as Azure Active Directory, for verifying the existence of users or groups.

!!!note
    This feature is not responsible for user authentication against {{msEntraName}}, refer to [configure authentication against {{msEntraName}}](helm_oidc_config.md#sample_entra_config).  If integrating with {{msEntraName}}, we recommend that you configure both the authentication and user/group search.

To complete this configuration you must:

- enable the feature
- configure the {{msEntraName}} tenant
- configure the credential alias

!!!note
    Leap must be restarted for these changes to take effect.

## Enable {{msEntraName}} User/Group Search

To enable Leap to search for users and groups in {{msEntraName}} you must add the ```ibm.nitro.NitroConfig.memberManagerType``` parameter to your Leap configuration.  The only valid value is **ms-azure-ad**.

```
ibm.nitro.NitroConfig.memberManagerType=ms-azure-ad
```

## Configure {{msEntraName}} Tenant

You must provide the tenant id for your {{msEntraName}} instance.  The ```ibm.nitro.NitroConfig.GraphApiMemberManager.tenantId``` property must be added to your Leap configuration.

```
ibm.nitro.NitroConfig.GraphApiMemberManager.tenantId=11111111-1111-1111-1111-111111111111
```

!!!note
    If Leap is running on WebSphere Application Server, refer to [Leap properties](helm_leap_properties.md) for more details on configuring properties.

    If Leap is running on Kubernetes, refer to [Configuring the properties file](co_configuring_the_properties_file.md) for more details on configuring properties.

## Configure the credential alias for communicating with {{msEntraName}} { #entra_credential_alias .section }

An OAuth token is required for communicating with {{msEntraName}}.  The ```ibm.nitro.NitroConfig.GraphApiMemberManager.credentialAlias``` specifies the alias containing the key and secret that will be used to retrieve the OAuth token.

The process for creating the credential object, referenced by the **credentialAlias** is based on the deployment environment, either WebSphere or Kubernetes.

### WebSphere Application Server: Create credential for Leap

The credential object for Leap running on WebSphere is a J2C Alias. 

For details on creating a J2C alias in IBM WebSphere, refer to [Managing Java 2 Connector Architecture authentication data entries for JAAS](https://www.ibm.com/docs/en/was-nd/9.0.5?topic=cplj-managing-java-2-connector-architecture-authentication-data-entries-jaas) in the IBM WebSphere documentation.

Take note of the following points in creating J2C alias in the IBM WebSphere Application Server:

The **alias name** will be used for the [GraphApiMemberManager.credentialAlias](azure_lookups.md#entra_credential_alias).

The **secret id** should be entered as the J2C alias **user id**.

The **secret value** should be entered as the J2C alias **password**.


### Kubernetes: Create credential for Leap

The credential object for Leap running on Kubernetes is a Kubernetes Secret.  The value provided should match the one used when creating the Kubernetes Secret.

Perform the following steps to create a Kubernetes secret using the client secret id and client secret value from the app registration in {{msEntraName}}.

```
"kubectl create secret generic <secretName> --from-literal=<credentialAlias>_key=<clientId> --from-literal=<credentialAlias>_secret=<clientSecret> -n myNamespace"
```

- The ```<secretName>``` will be how the object is identified within Kubernetes.

- The ```<credentialAlias>``` is the value provided to the 'credentialAlias' property. This is how Leap will locate/use this object.

- The ```<clientId>``` is the client id from the application that you created in the {{msEntraName}} admin center under "Enterprise application".

- The ```<clientSecret>``` is the client secret from the application that you created in the {{msEntraName}} admin center under "Enterprise application".

An example secret would look something like:

```
"kubectl -n myNamespace create secret generic azure-credentials --from-literal=azureAlias_key=11111 --from-literal=azureAlias_secret=22222"
```
The value specified for the ```credentialAlias``` would be "azureAlias".

After creating, you need to refer to the secret in the ```deploy-values.yaml``` as shown in the following example:

```yaml
configuration:
  leap:
    . . .
    customSecrets:
      azure-credentials: azure-credentials
    . . .
```

**Parent topic:** [Integrating with {{msEntraName}}](azure_toc.md)