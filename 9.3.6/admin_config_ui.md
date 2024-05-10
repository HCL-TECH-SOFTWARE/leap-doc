# Admin Configuration Page

The Admin Configuration page is available to members of the 'AdministrativeUsers' security role.  The admin can modify settings like: the HTTP services whitelist, service catalogs and descriptions, the domains that Leap can be embedded into, the javaScript sandbox setting, image domain whitelist, users and roles, admin contact information, and enabling anonymous access.

The page must be enabled by setting the Leap property "ibm.nitro.NitroConfig.enableAdminConfigUI=true" in the leap-config.properties or the Helm script for a Kubernetes deployment.

To access the admin configuration page visit http://myLeapServer/apps-admin/secure/org/admin/config/index.html.

When you access the admin configuration page the first time, all config settings (the javaScript sandbox, services whitelist, service descriptions, image domain whitelist, admin info and anonymous settings) will be loaded from the current configuration.  Custom extensions are not currently supported through the admin configuration page, they will need to be deployed directly to the extensions directory.  Any services defined in a custom extension will not appear in the services section.

After the feature is enabled, and the admin clicks 'save', the supported config properties are stored and read from the database.
 
Changes made in the admin configuration page will take effect automatically within a few moments, the server/pod does not need to be restarted, but may need a browser refresh to take effect.

Settings that are not supported in the Admin configuration page will continute to be configured using the leap_config.properties or the Helm chart properties.


## HTTP Services whitelist {#section_adm_srv_whitelist .section}

The Leap admin can define a list of domains and operations that app authors are allowed to include in their applications.  The whitelist defaults to 'off, which means that app authors can use REST/JSON services from any domain'.  The admin can enable the feature and then click the "Add URL to whitelist" button, which will provide a dialog to define a URL and operations (get, post, put, patch, delete, and head) to allow.


## Service catalogs and descriptions {#section_adm_srv_catalog .section}

Admins have always been able to add custom service descriptions to Leap (by placing them in the '.../ServiceCatalog/1' directory on the server).  Within the admin configuration page, admins will be able to upload existing XML service descriptions or create new service descriptions with the REST/JSON wizard.

For the first time, Leap admins will be able to define additional service catalogs and populate those catalogs with services.

The configured service descriptions are grouped by catalog.  App authors will see any configured catalogs and services to which they have access in the service description authoring dialog.  This dialog can be accessed from Settings…Services…Add Service Configuration panel, or through other venues like events or buttons within the authoring environment.

The section will also show product-level service descriptions, enabling the admin to adjust which users and groups have access to them.

### Service Security

Access to a service description may be given to all authenticated users or a specific user or group.  The access control is made up of two parts:
- App Authors (those who may discover and work with the service while designing an application)
  - Can be set to all app authors
  - Can be set to specific users or groups
- End user access (those who may run the service)
  - Can be set to all authenticated users
  - Can be set to include anonymous users
  - Can be set to specific users or groups

The Leap admin must manually enter the users and groups to which they want to assign access for a service description.  

The user values provided must match the configured user identification attribute (userIdMap):

 For a **Kubernetes Deployment**, this is defined in the ldap override section of your Helm chart, which is currently limited to "mail". The group values must match the configured group identification attribute (groupIdMap), defined in the ldap override section of your Helm chart, which defaults to its common name (cn). 

 For a **traditional WebSphere deployment**, this is defined in your federated repository configuration, which defaults to 'uid'.  The group values must match the configured group identification attribute, defined in the federated repository configuration, which defaults to its common name (cn).
 
### Creating a service description

To add a service, click the "Create service description" button, where you will have two options: Build REST/JSON or Upload service description XML.
 
#### Build REST/JSON

For this feature we have provided the same wizard that is provided to application authors for building a REST/JSON service description.  This enables the admin to build a service description for a HTTP endpoint that accepts and returns JSON.

##### URL

Select the desired action and URL for the endpoint.

##### Segments and parameters

This section separates the segments and parameters of the specified URL.  The purpose of this is so that you can define which components need to remain hard-coded or can be assignable from within the Leap application that uses the service.

If assignable, you can customize the name of the parameter as it will appear for the app author.

##### Request

In this section you can define any request headers that are required to communicate with the specified URL.  Any header defined can be hard-coded or marked as assignable.

##### Response

In this section you can define a sample response body.  We will attempt to access the URL and retrieve a sample response.  If a sample response cannot be retrieved, then you may need to supply one.  The content in this section will determine how the output of the service is constructed.  If there is no response then the service will have a single response output parameter.

You may also add any response headers.

##### Security

In this section you can define who can access this service.  The access is defined as:
- Application authors (who can discover and use the service in their applications)
- End users (who are allowed to access the data from the service while running in an application)

You can also define what kind of authentication is required to call the service:
- no authentication required
- username/password
- cookie-based authentication

##### Service Details

In this section you can define the service name, description, and assign it to a category.  If you want to create a new category, enter in the category name and then click the "Add ..." option that appears.
 
#### Upload service description XML

This feature is for configuring any custom service description files that have been deployed to your Leap environment.  We recommend that you remove the files from your ServiceCatalog/1 directory and then upload them using this feature of the admin configuration page.

**Note:** The previous mechanism of placing files in the ServiceCatalog/1 directory will still work, but any files added that way cannot be assigned to a category and will appear in "General".

1. Select "Upload service description XML"
2. Click Next.
3. Click "Upload File", locate and select the desired service description XML file.  Note that only XML files that follow our schema definition for service descriptions may be used.
4. The content of the file will be parsed and displayed.  This version of the tech-preview will not allow editing of the content, if you need to make changes to the service configuration you must edit outside the admin UI and then re-upload the file.
5. Assign the service to a catalog.  Select an existing catalog from the list, or type in the name of a new catalog and click the "Add ... " option that appears in the list.
**Note:** the catalog will not be added if you do not click the list item that appears.
6. Click Next to move on to security.
7. Select the desired security option and if applicable enter the users or groups separated by commas.


## Embedding into iFrame {#section_adm_ebd_iframe .section}

You can toggle the option to "Allow embedding from any domain" or you can add the specific domains that are allowed.

Define which domains users can embed Leap forms into.

To add a domain, click the "Add new domain" button and enter the HTTP address for the domain into the field that appears.  If you want to allow Leap apps to embed other Leap apps add a value of 'self' (including single quotes).


## JavaScript Setting {#section_adm_js .section}

By default, any custom JavaScript and custom HTML in Leap applications runs in a restricted sandbox.

With this setting enabled, Leap applications can utilize unrestricted JavaScript and HTML.

This section is related to the existing "secureJS" property.


## Image domain whitelist {#section_adm_img_whitelist .section}

The Image Domain Whitelist config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.

You can toggle the option to "Allow images from any domain" or you can add the specific domains that are allowed.

To add a domain, click the "Add new domain" button and enter the HTTP address for the domain in the field that appears.
This section is related to the existing "imageDomainWhitelist" property.


## Users and Roles {#section_adm_usr_role .section}

This section allows the Leap admin to change the definition of the administrator, application author and application end user roles.  You can use this to change the users and groups assigned to the roles, which previously would have required you to define them in the WebSphere admin console or modify the helm chart in a kubernetes deployment.  When using the admin configuration page, Leap becomes the custodian of the access permissions related to application security.  You must assign the special subject of 'All Authenticated Users' to each of these roles within the WebSphere admin console 'security role to user/group mapping' or the helm charts 'roleMapping' property.

**Note:** The user values provided must match the attributes used to login, for a Kubernetes deployment this is limited to the users email property. The group values must match the configured attribute, which defaults to cn.  The user and group values should be comma separated.

### Administrator Role

Users or groups in the Administrator role can modify the Leap configuration, view application statistics, and, view and edit all applications.  Add users or groups to the designated fields to assign them to the role.

### Application Manager Role

Users or groups in this role can view application statistics and view and edit all applications.  Add users or groups to the designated fields to assign them to the role.

### Application Author Role

A role that defines who has the ability to create an application.  You can select "all authenticated" or define a specific set of users or groups.

### Application end user role

A role that defines who can access the runtime version of an application.  You can select "all authenticated" or define a specific set of users or groups.  You can also toggle the option to allow anonymous access to use applications.


## Admin Contact Info

This section is for setting the "adminInfo" from our existing configuration properties.  It allows the Leap admin to provide the user more contact information when an error message is shown.  The section renders the message, including the admin-supplied info, that will be displayed to end users.


**Parent topic: **[Administering Leap](administering_leap.md)