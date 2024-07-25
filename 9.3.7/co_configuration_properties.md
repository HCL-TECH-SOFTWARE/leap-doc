# Configuration properties 

This topic contains a list of properties in the Leap Leap_config.properties file or defined in the Kubernetes .yaml file. You can adjust the settings listed in the file, or add your own for a custom configuration.


## Properties {#section_config_properties .section}

### adminInfo {#section_admininfo .section}

Allows admin contact information to be shown within error messages.

If <i>adminInfo1</i> and <i>adminInfo2</i> are both provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at **adminInfo1**, or **adminInfo2**, and provide error reference: XXX.” <br>

If only <i>adminInfo1</i> is provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at **adminInfo1** and provide error reference: XXX.”<br>

If neither are provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator and provide error reference: XXX.”

**Examples:**
```
ibm.nitro.NitroConfig.adminInfo1 = admin@yourcompany.com 
ibm.nitro.NitroConfig.adminInfo2 = 1-800-GET-HELP
```



### anonBlockedMsg {#section_anonblockedmsg}

When a user attempts to access a Leap application anonymously, an error message is displayed. The default message is “Anonymous access blocked”. You can change the default message to provide additional information to the user.<br>

**Example:**
```
ibm.nitro.NitroConfig.anonBlockedMsg=Anonymous usage is not allowed
```



### appFiles {#appfiles .section}

List of allowed (whitelist), and not allowed (blackList) of mimetypes, and the number of maximum file sizes for Application File uploads.<br>

**appFilesWhiteList** – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – empty (everything is allowed)

**appFilesBlackList** – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – exe

**appFilesMaxSize** (size in kb) – A space separated list of:<br>

-   mimetypes – text/plain application/ /vnd.xfdl<br>
-   file extensions – GIF PDF XML or default as special type<br>
-   default value – 5000

**Examples:**
```
ibm.nitro.NitroConfig.appFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi 
ibm.nitro.NitroConfig.appFilesBlackList = exe 
ibm.nitro.NitroConfig.appFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.appFilesMaxSize.50000 = mov avi
```



### appStats {#section_appstats .section}

By default, the timer is enabled and the collection time is set to 3 AM daily local server timer.<br>

<strong>Note:</strong> Depending on the volume of applications, statistics collection may take 10+ minutes, adjust the timer and frequency to server quiet time.<br>

**appStats.timerEnabled** - Enable Application Statistics collection.<br>
To disable Application Statistics collection, set to false.<br>
Default value: true

**appStats.refreshHour** - Sets the hour of day to start Application Statistics collection.<br>
Value 0 to 23, indicating the hour of day to start the statistics collection process.<br>
Default value: 3

**appStats.refreshDays** - Sets the Application Statistics collection day. Use full names of day of the week, separated by a comma, semicolon, or space.<br>
Valid values: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday<br>
Default value: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday<br>

**Examples:**

``` {#codeblock_kqt_sy2_gzb}
ibm.nitro.NitroConfig.appStats.timerEnabled=true 
ibm.nitro.NitroConfig.appStats.refreshDays=Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday
ibm.nitro.NitroConfig.appStats.refreshHour=3
```




### attachmentFiles {#section_attachmentfiles .section}

List of allowed (whitelist), and not allowed (blackList) of mimetypes, and the number of maximum file sizes for the Attachment form item.<br>

**attachmentFilesWhiteList** – A space separated list of:<br>
<ul>
    <li>mimetypes – text/plain application/vnd.xfdl</li>
    <li>partial mimetypes – text/audio/ /plain</li>
    <li>file extensions – GIF PDF XML</li>
    <li>default value – empty (everything is allowed)</li>
</ul>

**attachmentFilesBlackList** – A space separated list of:
<ul>
    <li>mimetypes – text/plain application/vnd.xfdl</li>
    <li>partial mimetypes – text/audio/ /plain</li>
    <li>file extensions – GIF PDF XML</li>
    <li>default value – exe js html svg</li>
</ul>

**attachmentFilesMaxSize** (size in kb) – A space separated list of:
<ul>
    <li>mimetypes – text/plain application/ /vnd.xfdl</li>
    <li>file extensions – GIF PDF XML or default as special type</li>
    <li>default value – 5000</li>
</ul>

**Examples:**

``` {#codeblock_hvz_bcf_gzb}
ibm.nitro.NitroConfig.attachmentFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi
ibm.nitro.NitroConfig.attachmentFilesBlackList = exe 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.50000 = mov avi
```



### blockAnonAccess {#section_blockanonaccess .section}

Anonymous access is not allowed by default which means that to use a Leap application or survey, users must authenticate with a valid user ID and password.<br>
This setting determines anonymous access, where:<br>
<ul>
    <li>enabled - anonymous access is blocked</li>
    <li>disabled - anonymous access is allowed</li>
    <li>redirect - redirects the user to authenticate</li>
</ul>

Default value: redirect

**Example:**
```
ibm.nitro.NitroConfig.blockAnonAccess=redirect
```



### customThemes {#section_customthemes .section}

The **customThemes config** settings define a list of customer-provided themes that can be used in Leap applications.

For each theme, two parameters must be set:
<ul>
    <li>customThemes.[ID].displayName</li>
    <li>customThemes.[ID].location</li>
</ul>

**[ID]** - An identifier for the custom theme (e.g. "corpTheme1").
The id can contain the letters 'a' through 'z' and numbers, and must start with a letter.<br>

**displayName** - The theme name to be displayed in the Leap authoring UI.

**location** -The full URL of the theme's .css file.

For each theme, there are 2 optional parameters:
<ul>
    <li>customThemes.[ID].isDefault</li>
    <li>customThemes.[ID].nl.[LOCALE]</li>
</ul>

**isDefault** - If set to true, designates the theme as the default selection for new applications.

**nl.[LOCALE]** - For globalization support of the theme's display name. **[LOCALE]** is the locale code that identifies the language (e.g.,"en", "fr", "fr_CA", "zh").

After modifying these settings, restart the Leap server to see the changes in the authoring environment. If the location property of a theme is modified, any deployed applications using that custom theme need to be redeployed for changes to take affect.

**Examples:**
``` {#codeblock_wgh_s51_hzb}
customThemes.corpTheme1.displayName = Corporate Theme 1
customThemes.corpTheme1.nl.fr = Thème d'entreprise 1
customThemes.corpTheme1.nl.zh = 企业主题1
customThemes.corpTheme1.isDefault = true
customThemes.corpTheme1.location =https://mycompany.com/theme1.css
```



### detectBrowser {#section_detectbrowser .section}

If Leap detects an unsupported browser, a warning message is displayed to the user. The user can still see the form after the warning message is closed.Where:

<ul>
<li>warn - The user is warned that the browser is unsupported. A list of supported browsers is displayed in the warning message. When the user closes the warning message, the form is displayed.</li>
<li>ignore - The user is not warned that the browser is unsupported, and the form is displayed.</li>
</ul>

Default value: warn

**Example:**

``` 
ibm.nitro.NitroConfig.detectBrowser=ignore
```



### disableUseTab {#section_disableusetab .section}

Hides the "Use" tab, and prevents fetching the list of deployed and usable applications, where:

<ul>
    <li>true - "Use" tab is hidden</li>
    <li>false - "Use" tab is displayed</li>
</ul>

Default value: false

**Example:**

``` 
ibm.nitro.NitroConfig.disableUseTab=true
```



### enableAdminConfigUI {#section_enableAdminConfigUI .section}

Enables the admin configuration page. Valid values are true or false.  For more information, refer to [Admin Configuration Page](admin_config_ui.md).

Default value: false

**Example:**

```
ibm.nitro.NitroConfig.enableAdminConfigUI=true
```


### embedDomainWhitelist {#section_embedDomainWhitelist .section}

The domains where Leap may be embedded. If the whitelist is enabled and the domain is not listed then Leap applications will not be allowed to be presented as part of that content.

This property contains 2 parts:
<ul>
    <li>embedDomainWhitelist.enabled</li>
    <li>embedDomainWhitelist.[N].domain</li>
</ul>

**enabled** - Enables/Disables the whitelist.  If the whitelist is disabled, Leap will allow itself to be embedded into any domain.

Default value: true

**[N].domain** - '[N]' is an incrementing number starting with '1'. Provide the domain where embedding Leap applications should be allowed.

**Example:**

```
ibm.nitro.NitroConfig.embedDomainWhitelist.enabled = true
ibm.nitro.NitroConfig.embedDomainWhitelist.1.domain = https://embedder1.example.com
ibm.nitro.NitroConfig.embedDomainWhitelist.2.domain = https://embedder2.example.com
ibm.nitro.NitroConfig.embedDomainWhitelist.3.domain = 'self'
```



### EventHandler {#section_eventhandler .section}

Leap contains an event handling implementation that enables printing out all or specific events in the system log or in a separate file based on properties setting, by default this feature is not enabled. Change properties, in the Leap_config.properties file, to monitor events that you are interested in, and where you want to output the event information.

The following will output Events information in Application Server's system log at info or debug level:
<ul>
    <li>EventHandler.infoLevelEvents</li>
    <li>EventHandler.debugLevelEvents</li>
</ul>

**EventHandler.auditLevelEvents** will output to a file. The default file location on Windows is C:\febEvents.log and AIX/Linux is /febEvents.log, with maximum file size 5MB, back up to 5 files.

The content of the event output is in CSV format, the description of the data: Event topic, Event time stamp, User id, User email, Application uid, Application title, Form id, Record uid, Result

The following is the list of event topics that Leap sends out:

<ul>
    <li>builder/app/delete – Application is deleted</li>
    <li>builder/app/deploy – Application is deployed for the first time</li>
    <li>builder/app/redeploy – A deployed application is deployed again</li>
    <li>builder/app/stop – A deployed application is stopped</li>
    <li>builder/app/import – Application is imported</li>
    <li>builder/app/importAndDeploy – Application is imported and deployed</li>
    <li>builder/app/importAndDeployWithData – Application is imported and deployed with data</li>
    <li>builder/app/export – Application is exported</li>
    <li>builder/app/exportWithData – Application is exported with data</li>
    <li>builder/app/upgrade – Application is upgraded</li>
    <li>builder/app/upgradeWithDataReplaced – Application is upgraded and the data replaced</li>
    <li>builder/app/result/export – Application data is exported from View Data (or REST API)</li>
    <li>builder/app/retrieve/source – Application source is retrieved</li>
    <li>builder/app/query/deployed – Application deployment state is queried</li>
    <li>builder/record/submit – A record is submitted by normal app usage</li>
    <li>builder/record/update – A record is updated by normal app usage</li>
    <li>builder/record/delete – A record is deleted by normal app usage</li>
    <li>builder/data/insert/user – A record is created as a result of a direct user action</li>
    <li>builder/data/insert/code – A record is created indirectly</li>
    <li>builder/data/update/user – A record is updated as a result of a direct user action</li>
    <li>builder/data/update/code – A record is updated indirectly</li>
    <li>builder/data/delete/user – A record is deleted as a result of a direct user action</li>
    <li>builder/data/delete/code – A record is deleted indirectly</li>
</ul>

To capture failed events, use "builder/error/[EVENT_TOPIC]"

**Example:**

``` 
 ibm.nitro.EventHandler.infoLevelEvents=builder/record/submit,builder/error/builder/record/submit
```



### exportDataWithEmails {#section_exportdatawithemails .section}

By default when you export data from applications, emails are also exported. You can exclude emails from the export by changing the property value to false.

Where:
<ul>
    <li>true - emails are exported with application data</li>
    <li>false - emails are not exported with application data</li>
</ul>

Default value: true

**Example:**

``` 
ibm.nitro.NitroConfig.exportDataWithEmails=true
```

### hclMXFoundryApps {#section_mxfoundry .section}

The **hclMXFoundryApps** property defines the settings for connecting Leap to HCL Volt MX Foundry integration services.

This property contains the following parts:
<ul>
    <li>hclMXFoundryApps.enabled</li>
    <li>hclMXFoundryApps.[N].appName</li>
    <li>hclMXFoundryApps.[N].serviceUrl</li>
    <li>hclMXFoundryApps.[N].credentialAlias</li>
</ul>

**Example:**

```
ibm.nitro.NitroConfig.hclMXFoundryApps.enabled = true
ibm.nitro.NitroConfig.hclMXFoundryApps.1.appName = Foundry App 1
ibm.nitro.NitroConfig.hclMXFoundryApps.1.serviceUrl = http://myFoundryServer/authService/100000002/appconfig
ibm.nitro.NitroConfig.hclMXFoundryApps.1.credentialAlias = 'FOUNDRY_APP1'
ibm.nitro.NitroConfig.hclMXFoundryApps.2.appName = Foundry App 2
ibm.nitro.NitroConfig.hclMXFoundryApps.2.serviceUrl = https://100002720.myFoundryCloudServer/appconfig
ibm.nitro.NitroConfig.hclMXFoundryApps.2.credentialAlias = 'FOUNDRY_APP2'
```

### hclMXFoundryAppsCacheRefreshMins {#section_mxfoundrycache .section}

The **hclMXFoundryAppsCacheRefreshMins** property defines the amount of time in minutes that MX Foundry service descriptions are held in memory.  The default value is 60.

**Example:**

```
ibm.nitro.NitroConfig.hclMXFoundryAppsCacheRefreshMins=60
```

### imageDomainWhitelist {#section_imagedomain .section}

The **imageDomainWhitelist** config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.

In addition to setting the following:

**imageDomainWhitelist.enabled=true** for each domain an additional parameters must be set.

**imageDomainWhitelist.[N].domain =** where "[N]" is an integer number identifying that service.

domain - The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.

**Examples:**

``` 
ibm.nitro.NitroConfig.imageDomainWhitelist.enabled=true
ibm.nitro.NitroConfig.imageDomainWhitelist.[1].domain=http://acme.com
ibm.nitro.NitroConfig.imageDomainWhitelist.[2].domain=http://acme2.com
```



### InfoEntryPoint.dailyInfo {#section_infoentrypoint .section}

Provides HTML content that is shown in the login screen. Can be used for status messages, or help.

``` 
ibm.nitro.InfoEntryPoint.dailyInfo = Welcome to **HCL Leap**
```



### LogoutServlet.postLogoutRedirectURL {#section_logout .section}

The value of this parameter tells Leap where to redirect user after log off. If the parameter is not configured or left blank, the user is redirected to the login page.

**Example:**

``` 
ibm.nitro.LogoutServlet.postLogoutRedirectURL=http://example_url.com/signout
```



### maximumRecordsToRetrieve {#section_maximumrecords .section}

Maximum number of records that are permitted for export from the View Data page at one time. If the number of records to be exported exceeds the number set by this property, the export is stopped, and an error message is shown.

**Note:** The default value of 20,000 is supported for base systems. Setting the value higher could result in poor performance, depending on result set size and server hardware.

**Example:**

``` 
ibm.nitro.NitroConfig.maximumRecordsToRetrieve=25000
```



### MemberManager {#section_membermanager .section}

<ul>
<li>MemberManager.userProps.loginName</li>
<li>MemberManager.userProps.id</li>
<li>MemberManager.groupProps.id</li>
<li>MemberManager.userProps.email</li>
<li>MemberManager.userProps.displayName<li>
</ul>

**MemberManager.adminAlias** setting is mandatory. For WebSphere Application Server only, configure the VMM login.

By default, Leap uses J2C alias **vmmAdmin** to authenticate with VMM. You must configure it here if you want to change the J2C alias name.

You must have WebSphere Application Server administrative user credentials to run Leap.

If you use LDAP within WebSphere Application Server, there are a number of properties that look up user and group information. If your LDAP uses different property keys than the ones set by default, update the property keys here so that user and group look up function correctly.

If you are using LDAP within WebSphere Application Server, refer to the following settings:

**MemberManager.userProps.loginName**: 
Describes the LDAP property used as the login ID. Each loginName must be unique.
Default setting: uid

**MemberManager.userProps.id**
Represents a unique key for the user. This key must be identical to the loginName.
Default setting: uid

**MemberManager.groupProps.id**
Represents a unique key for the group. The value is the LDAP property that is used. For example, cn, represents Common Name.
Default setting: cn

**MemberManager.userProps.email**
The email address of the user. Leap uses this email address to send notifications and other emails to the user.
Default setting: mail

**MemberManager.userProps.displayName**
Used to display the name of the user, instead of the login id.
Default setting: cn

**Examples:**

``` 
ibm.was.MemberManager.userProps.loginName = mail 
ibm.was.MemberManager.userProps.id = mail
ibm.was.MemberManager.groupProps.id = name
ibm.was.MemberManager.userProps.email = mail
ibm.was.MemberManager.userProps.displayName = cn
```



### purgeOrphanFilesHours {#section_purgefileshours .section}

In some circumstances, files attached to either application designs or user-submitted records can become orphaned if the primary design or record element is removed outside the normal process. File records which are older than this number of hours and are no longer associated with an existing primary record are removed.

Default value: 48

**Example:**

``` 
ibm.nitro.NitroConfig.purgeOrphanFilesHours=36
```

### reauthInNewWindow {#section_reauthInNewWindow .section}

Helps with seamless re-authentication when Leap is using an external IdP (in SAML or OIDC configurations), so that Leap users do not lose their work.  When set to `true`, the authentication flow is presented in a pop-up window, which is typically adequate for most external IdPs. It is recommended to use this setting in conjunction with `ibm.nitro.NitroConfig.reauthOnFailedRequest`.

Default value: false

**Example:**

``` 
ibm.nitro.NitroConfig.reauthInNewWindow=true
```

### reauthOnFailedRequest {#section_reauthOnFailedRequest .section}

Helps with seamless re-authentication when Leap is using an external IdP (in SAML or OIDC configurations) so that Leap users do not lose their work.  When set to `true`, a failed XHR request triggers the authentication flow. A failed request is the typical result when an SAML or OIDC session has timed-out. It is recommended to use this setting in conjunction with `ibm.nitro.NitroConfig.reauthInNewWindow`. 

**Known Limitations**: There is no mechanism in the browser for the Leap code to distinguish a session time-out failure from other types of failures, such as a loss of internet connectivity. Enabling this setting means that *any* XHR request failure will trigger an authentication flow, even if it is not appropriate. However, for the majority of cases this setting will help Leap users to not lose their work, therefore it is recommended.

Default value: false

**Example:**

``` 
ibm.nitro.NitroConfig.reauthOnFailedRequest=true
```


### rootAdminId {#section_rootAdminId .section}

The **rootAdminId** setting defines the login id of a user that will always have access to the Admin Configuration page.

**Example**

```
ibm.nitro.NitroConfig.rootAdminId=adminUser
```



### runtimeCSP {#section_runtimecsp .section}

The **runtimeCSP** setting defines the <code>Content-Security-Policy</code> (CSP) header that will be applied to running Forms.

**Note:** This setting only applies to Forms. It does not currently apply to App Pages, Summary Charts, or the View Data page.

For more information on CSP, see <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP" target="_blank">Content Security Policy (CSP)</a> in the Mozilla documentation.

For more information on <i>Strict</i> CSP, see <a href="leap_strict_csp.html">Strict CSP</a>

**Example:**

``` 
ibm.nitro.NitroConfig.runtimeCSP=default-src 'self' *.example.com; img-src *
```



### runtimeResources.[N] {#section_runtimeresources .section}

Additional web resources to load into the Leap UI for leveraging the <a href="customwidgetapi_landing.html">Custom Widget API</a>. The values from these settings will be injected into the <code>&lt;head&gt;</code> section of Leap's HTML pages.

**Example:**

``` 
ibm.nitro.NitroConfig.runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css'>
ibm.nitro.NitroConfig.runtimeResources.2 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
ibm.nitro.NitroConfig.runtimeResources.3 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
```



### secureJS {#section_securejs .section}

Enables or disables JavaScript restrictions in run time forms. When a form designer adds custom JavaScript to an application, this flag restricts the scope of that custom JavaScript. This flag applies to the entire Leap server for all users.

**Note:** Setting this parameter to <code>false</code> might expose users to malicious JavaScript. Only set to <code>false</code> in a secured environment where Leap applications are created by trusted users.

For more information, see <a href="ref_javascript_api.html">JavaScript API</a> for Leap.

Default value: true

**Example:**

``` 
ibm.nitro.ApplicationCompilerService.secureJS = false
```



### serviceAuthorization {#section_serviceauthorization .section}

Access to a service description may be given to a specific user, group, or special assignment. The access control is made up of two parts:

<ul>
    <li>Who may "discover" and work with the service while designing an application.</li>
    <li>Who may "invoke" the service.</li>
</ul>

Users or Groups provided must be defined using the attributes defined by <code>ibm.was.MemberManager.userProps.id = mail</code> and <code>ibm.was.MemberManager.groupProps.id = name</code> respectively.

Special assignment valid values are:
<ul>
    <li>all-authenticated: for app author "discover" privilege only</li>
    <li>anonymous: for app authors and end-user "discover" and "invoke" privileges</li>
    <li>all-authors: for end-user "invoke" privilege only</li>
</ul>

To enable service authorizations, set <code>ibm.nitro.NitroConfig.serviceAuthorization.enabled=true</code>. Multiple services may be defined. To define a service authorization, add <code>ibm.nitro.NitroConfig.serviceAuthorization.serviceIdN</code> where **serviceIdN** is the 'id' of the service description. The value must be a valid JSON string, see provided samples.

<strong>Note:</strong> A backslash (\) at the end of a line can be used to present a value over multiple lines. The backslash must be the very last character on the line.

**Examples:**

```
ibm.nitro.NitroConfig.serviceAuthorization.enabled = true
ibm.nitro.NitroConfig.serviceAuthorization.serviceId1 = { \
   "comment": "Auth for Service 1", \
   "discover": { "users": ["user1"], "groups": ["group1"], "special": [] }, \
   "invoke": { "users": [], "groups": [], "special": ["all-authenticated"]" } \
}
```



### serverURI {#section_serveruri .section}

Indicates the base URI used for critical functions, including editing applications, and email. Must include everything necessary to connect to the Leap context, for example, /apps.

With this entry, all emailed links, and absolute links visible during Leap design time start with the following base URI regardless of what the user enters in the address bar.

Example:
``` 
ibm.nitro.NitroConfig.serverURI = https://leap.example.com/apps
```



### servicesWhitelist {#section_servicewhitelist .section}

The **servicesWhitelist** config settings define a white list of domains and HTTP actions that app authors are allowed to call directly from their applications using URL based services.

In addition to setting <code>servicesWhitelist.enabled=true</code>, for each service two additional parameters must be set:
<ul>
<li>servicesWhitelist.[N].domain =</li>
<li>servicesWhitelist.[N].actions =</li>
</ul>

The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.
The https or http protocol included in the domain property is respected. For example, a domain property of https://api.example.com only allows calls to secure SSL https://api.example.com/anything and not to non-secure http://api.example.com/anything.
The actions property is a comma-separated list of the HTTP actions allowed for a particular domain. Valid values are GET, PUT, POST, DELETE, HEAD, and PATCH. If the actions value is missing, no actions are allowed.

Where **[N]** is an integer number identifying that service.

Default value: true

**Examples:**

``` 
ibm.nitro.NitroConfig.servicesWhitelist.enabled = true
ibm.nitro.NitroConfig.servicesWhitelist.1.domain = example.com
ibm.nitro.NitroConfig.servicesWhitelist.1.actions = GET
ibm.nitro.NitroConfig.servicesWhitelist.2.domain = https://securehost.com
ibm.nitro.NitroConfig.servicesWhitelist.2.actions = GET, POST,PUT
```

**Note:** This white-list has no effect on service descriptions and custom service transports that were installed on the server by the administrator.



### SetupAll.setupStatus {#section_setupall .section}

After deploying Leap for the first time or upgrading to a newer version, there is a setup screen that is presented upon accessing the manage page. This setup screen shows the status of detecting and updating the database tables, checks that security is properly enabled, and a mail session is configured. This page requires the admin to click a button to fully progress through the setup.

To disable this setup page and required admin interaction add the property: 

``` 
ibm.nitro.SetupAll.setupStatus = start
```



### viewResponsesMaximumCount {#section_viewresponsecount .section}

For DB2® or Oracle. The maximum number of records that are <i>counted</i> when returning record sets in pages. If the total number of records exceeds viewResponsesMaximumCount, then paging indicators will no longer accurately lists the total number of pages. Setting this value higher can have performance consequences for the server if there are many users viewing forms with large response lists.

Default value: 1000

**Example:**

```
ibm.nitro.NitroConfig.viewResponsesMaximumCount=2000
```



### <strike>xFrameOptions</strike> {#section_xframeoption .section}

Deprecated. Use [embedDomainWhitelist](#embedDomainWhitelist).



**Parent topic:** [Configuring the properties file](co_configuring_the_properties_file.md)

