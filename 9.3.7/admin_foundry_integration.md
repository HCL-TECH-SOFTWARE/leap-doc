# Integrating with HCL Volt MX Foundry

HCL Leap can now use the integration services defined in [HCL Volt MX Foundry](https://opensource.hcltechsw.com/volt-mx-docs/docs/documentation/tutorials/voltmxFoundryOverview.html).

Leap can be connected to more than one Foundry application and can even be located on different Foundry cloud or on-premise servers.  This integration does not require any identity services because all requests will be made using the app key and the app secret of the application.

Once configured, Leap will connect with Foundry to determine the services and operations that need to appear in Leap.  Each service in the Foundry application will be represented as a Service Catalog in Leap.  Each operation in the Foundry service will appear as a service in the Leap catalog.  Leap will periodically reach out to Foundry to insure that its service catalogs and services are kept in sync.

Before configuring the integration you will need to have a published Foundry application that includes at least 1 integration service and operation.

## How to create your first Foundry Integration Service

1. Login to the **HCL Volt MX Foundry** console.
2. Click **Add new**.
3. Enter a name for the application.
4. Click **Integration**.
5. Click **Configure New**.
  - Give the service a meaningful name (it may not contain spaces and only allows special characters '-' and '_'.
  - Set the service type.
  - Define the base url of the service.
  - If required, configure the authentication for connecting to the service.
6. Click **Save & Add Operation**.
7. Define the operation:
  - Give the operation a meaningful name (it may not contain spaces).
  - Define the target URL. 
  **Note:** If the URL is meant to take dynamic parameters, create an input parameter and then reference it in the URL with a dollar sign (for example,  ```$inputParam```).
  - Define the target method.
8. Click **Save and Fetch Response**.
9. In the **Backend Response** section, hover over the elements that you want to be returned and click **Create Response**.  This will add the appropriate outputs to the operation response.
10. Click **Save Operation**.
11. Click on the **Publish** tab.
12. Click on the **Publish** button. Once the app is published, you are ready to move on to the next step of setting up the Leap configuration!  You will need the service URL, the primary app key, and the primary app secret.  If you did not copy them from the publish dialog you can access them by clicking on the Key button (on the upper right corner of the application card) on the **Publish** tab.

For more detailed information on the HCL Volt MX Foundry integration services refer to the [product documentation](https://opensource.hcltechsw.com/volt-mx-docs/docs/documentation/Foundry/vmf_integrationservice_admin_console_userguide/Content/Integration_Services.html).

## Enabling and configuring the MX Foundry Integration

In this section we will configure Leap so that it can communicate with MX Foundry and its integration services.

The process for enabling and configuring the integration depends on your Leap environment. 

If you have the Admin Configuration page enabled you will use it, otherwise the settings are defined as [Leap properties](co_configuration_properties.md).

There are 3 things that are required for each Foundry application:

1. the application name (appName) - This can be any name that you like, but it is intended to help you easily correlate the settings with the application in Foundry. It is recommended that you set this to the same name used in Foundry.

2. the service url (serviceUrl) - This is the url for the integration service.  It can be copied from the Foundry "publish" dialog.

3. the credential alias (credentialAlias) - This is the name of the credential object that contains the app key and app secret which is used to communicate with MX Foundry.  The credential setup depends on where Leap is deployed.


### How to create credential for accessing MX Foundry

The process for creating the credential object is based on the deployment environment: WebSphere, Kubernetes, or Domino.


#### Create credential for Leap on WebSphere

The credential object for Leap running on WebSphere is a J2c Alias.

1. Login to the **WebSphere Administration** console.
2. Create a new J2C Alias.
3. Provide a name for the alias.  This is the value that will be given to the ```credentialAlias``` in the Leap configuration.
4. Copy the app key from the MX Foundry publish dialog into the username field.
5. Copy the app secret from the MX Foundry publish dialog into the password field.
6. Save the alias.
7. Restart WebSphere.


#### Create credential for Leap on Kubernetes

The credential object for Leap running on WebSphere is a Kubernetes Secret. The value you supply is the same as the one you have used in creating the kubernetes secret.

First, create a kubernetes secret using the command below:

```
"kubectl create secret generic <secretName> --from-literal=<credentialAlias>_key=<appKey> --from-literal=<credentialAlias>_secret=<appSecret> -n dxns"
```

- The ```<secretName>``` will be how the object is identified within Kubernetes.

- The ```<credentialAlias>``` is the value provided to the 'credentialAlias' property. This is how Leap will locate/use this object.

- The ```<appKey>``` is the app key for the Foundry application.

- The ```<appSecret>``` is the app secret for the Foundry application.

An example secret would look something like:

```
"kubectl -n dxns create secret generic foundry-app1-credentials --from-literal=FOUNDRY_APP1_key=6e230187797c9ddb28b77d5d11306d55 --from-literal=FOUNDRY_APP1_secret=1f8527fd8d981e31a4861291ce632942"
```
The value specified for the ```credentialAlias``` would be "FOUNDRY_APP1".

After creating, you need to refer to the secret in the ```deploy-values.yaml``` as shown in the following example:

```yaml
configuration:
  leap:
    . . .
    customSecrets:
      foundry-app1: foundry-app1-credentials
    . . .
```


#### Create credential for Domino Leap not included in the 9.3.7 docs

The credential object for Domino Leap is a service credential which can be defined in the Leap Config DB (.nsf).

1. Open the **Leap Configuration** database in **HCL Domino Designer** or **HCL Notes**.
2. Create a new service credential.
3. Provide a name for the credential, this is the value that is given to the ```credentialAlias``` in the Leap configuration.
4. Copy the app key from the MX Foundry publish dialog into the username field.
5. Copy the app secret from the MX Foundry publish dialog into the password field.
6. Save the service credential.


## Using a service from MX Foundry in your Leap application

The MX Foundry services will appear in the service configuration dialog.  The Foundry service will be the name of the service catalog.  After selecting the catalog, the Foundry operations will be listed as the Leap services.

Select the service and continue through the dialog to map inputs and outputs as you would for any other service.

## Troubleshooting the HCL Volt MX Integration

If your Foundry Integration services are not appearing with in Leap, try the following procedures:

- Verify that your Leap server can reach the Foundry server.
- Verify that you have enabled the integration.
- Verify that you have defined all three config settings for the Foundry application (app name, service url, and credential alias).
- Verify that the username and password in the credential alias is using the correct app key (should be used as the username) and app secret (used as the password).
- Verify that your Foundry application is published.  If it was published recently, then you may need to wait at least 5 minutes before the change will appear in Leap.  Restarting Leap will also force Leap to pull fresh content from Foundry.
- Leap caches (default is 60 minutes) the artifacts that define the foundry services, if your changes are not appearing in Leap then you may need to restart Leap.
- You may need to install the trusted root certificate for the SSL certificate that was used to secure the MX Foundry server.
- Increase the log level by adding the trace string "com.ibm.form.nitro.service.*=finest".
- If the catalogs and services are still not appearing, contact [Support](https://support.hcltechsw.com/csm?id=csm_index).

**Parent topic:** [Administering Leap](administering_leap.md)