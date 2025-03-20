# Configuration properties 

This topic contains a list of properties in the {{shortProductName}} {% if isLeap %}Leap_config.properties file or defined in the Kubernetes .yaml file{% endif %}{% if isDominoLeap %}VoltConfig.nsf{% endif %}. You can adjust the settings listed in the file, or add your own for a custom configuration.


## Properties { #section_config_properties .section }

### adminInfo { #section_admininfo .section }

Allows admin contact information to be shown within error messages.

If <i>adminInfo1</i> and <i>adminInfo2</i> are both provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at **adminInfo1**, or **adminInfo2**, and provide error reference: XXX.” <br>

If only <i>adminInfo1</i> is provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at **adminInfo1** and provide error reference: XXX.”<br>

If neither are provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator and provide error reference: XXX.”

**Examples:**
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}adminInfo1 = admin@yourcompany.com 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}adminInfo2 = 1-800-GET-HELP
```



### anonBlockedMsg { #section_anonblockedmsg }

When a user attempts to access a {{shortProductName}} application anonymously, an error message is displayed. The default message is “Anonymous access blocked”. You can change the default message to provide additional information to the user.<br>

**Example:**
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}anonBlockedMsg=Anonymous usage is not allowed
```



### appFiles { #appfiles .section }

List of allowed (whitelist) and not allowed (blackList) file types, and the maximum file sizes for Application File uploads.  
A whiteList is strongly recommended for best security.

File types can be specified as:  

- mimetypes - text/plain application/json
- partial mimetypes - text/ image/ /javascript
- file extensions - GIF PDF XML  (case insensitive)

**appFilesWhiteList** (*Recommended*) - A space-separated list of allowed files types  

- default value - `css js svg png gif bmp jpg webp txt pdf ttf otf woff woff2`

**appFilesBlackList** (*Deprecated*) - A space-separated list of disallowed file types:  

- default value - (empty)

**appFilesMaxSize.\[size_in_KB\]** - Max file size for the given separated list of values, in kilobytes.  

- value can be:  
    - the word "default" to indicate the default max size for all file types
    - a space-separated list of mime-types or file extensions, for max size of specific file types
- the default max file size is 5000 KB

**Example:**
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appFilesWhiteList = css js text/plain image/ mp3 mp4
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appFilesMaxSize.10000 = default
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appFilesMaxSize.50000 = mp3 mp4
```



### appStats { #section_appstats .section }

By default, the timer is enabled and the collection time is set to 3 AM daily local server timer.<br>

!!! note
    Depending on the volume of applications, statistics collection may take 10+ minutes, adjust the timer and frequency to server quiet time.<br>

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

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appStats.timerEnabled=true 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appStats.refreshDays=Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}appStats.refreshHour=3
```


### attachmentFiles { #section_attachmentfiles .section }

List of allowed (whiteList) and disallowed (blackList) file types, and the maximum file sizes for file uploads via Attachment and Rich Text Entry widgets.  
A whiteList is strongly recommended for best security.

File types can be specified as:  

- mimetypes - text/plain application/json
- partial mimetypes - text/ image/ /plain
- file extensions - GIF PDF XML  (case insensitive)

**attachmentFilesWhiteList** (*Recommended*) - A space-separated list of allowed files types  

- default value - `png gif bmp jpg webp txt pdf odt ods odp doc docx ppt pptx xls xlsx csv tsv log`

**attachmentFilesBlackList** (*Deprecated*) - A space-separated list of disallowed file types:  

- default value - (empty)

**attachmentFilesMaxSize.\[size_in_KB\]** - Max file size for the given separated list of values, in kilobytes.  

- value can be:  
    - the word "default" to indicate the default max size for all file types
    - a space-separated list of mimetypes or file extensions, for max size of specific file types
- the default max file size is 5000 KB

**Example:**
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}attachmentFilesWhiteList = png gif jpg text/plain pdf docx xlsx csv mp3 mp4
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}attachmentFilesMaxSize.10000 = default
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}attachmentFilesMaxSize.50000 = mp3 mp4
```



### blockAnonAccess { #section_blockanonaccess .section }

Anonymous access is not allowed by default which means that to use a {{shortProductName}} application or survey, users must authenticate with a valid user ID and password.<br>
This setting determines anonymous access, where:<br>

- enabled - anonymous access is blocked
- disabled - anonymous access is allowed
- redirect - redirects the user to authenticate


Default value: redirect

**Example:**
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}blockAnonAccess=redirect
```



### customThemes { #section_customthemes .section }

The **customThemes config** settings define a list of customer-provided themes that can be used in {{shortProductName}} applications.

For each theme, two parameters must be set:

- customThemes.[ID].displayName
- customThemes.[ID].location


**[ID]** - An identifier for the custom theme (e.g. "corpTheme1").
The id can contain the letters 'a' through 'z' and numbers, and must start with a letter.<br>

**displayName** - The theme name to be displayed in the {{shortProductName}} authoring UI.

**location** -The full URL of the theme's .css file.

For each theme, there are 2 optional parameters:

- customThemes.[ID].isDefault
- customThemes.[ID].nl.[LOCALE]


**isDefault** - If set to true, designates the theme as the default selection for new applications.

**nl.[LOCALE]** - For globalization support of the theme's display name. **[LOCALE]** is the locale code that identifies the language (e.g.,"en", "fr", "fr_CA", "zh").

After modifying these settings, restart the {{shortProductName}} server to see the changes in the authoring environment. If the location property of a theme is modified, any deployed applications using that custom theme need to be redeployed for changes to take affect.

**Examples:**
```
customThemes.corpTheme1.displayName = Corporate Theme 1
customThemes.corpTheme1.nl.fr = Thème d'entreprise 1
customThemes.corpTheme1.nl.zh = 企业主题1
customThemes.corpTheme1.isDefault = true
customThemes.corpTheme1.location =https://mycompany.com/theme1.css
```



### detectBrowser { #section_detectbrowser .section }

If Leap detects an unsupported browser, a warning message is displayed to the user. The user can still see the form after the warning message is closed.Where:

- warn - The user is warned that the browser is unsupported. A list of supported browsers is displayed in the warning message. When the user closes the warning message, the form is displayed.
- ignore - The user is not warned that the browser is unsupported, and the form is displayed.

Default value: warn

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}detectBrowser=ignore
```


{% if isLeap %}
### disableUseTab { #section_disableusetab .section }

Hides the "Use" tab, and prevents fetching the list of deployed and usable applications, where:

- true - "Use" tab is hidden
- false - "Use" tab is displayed


Default value: false

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}disableUseTab=true
```


### enableAdminConfigUI { #section_enableAdminConfigUI .section }

Enables the admin configuration page. Valid values are true or false.  For more information, refer to [Admin Configuration Page](admin_config_ui.md).

Default value: false

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}enableAdminConfigUI=true
```
{% endif %}

### embedDomainWhitelist { #embedDomainWhitelist .section }

The domains where {{shortProductName}} may be embedded. If the whitelist is enabled and the domain is not listed then {{shortProductName}} applications will not be allowed to be presented as part of that content.

This property contains 2 parts:

- embedDomainWhitelist.enabled
- embedDomainWhitelist.[N].domain


**enabled** - Enables/Disables the whitelist.  If the whitelist is disabled, {{shortProductName}} will allow itself to be embedded into any domain.

Default value: true

**[N].domain** - '[N]' is an incrementing number starting with '1'. Provide the domain where embedding {{shortProductName}} applications should be allowed.

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}embedDomainWhitelist.enabled = true
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}embedDomainWhitelist.1.domain = https://embedder1.example.com
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}embedDomainWhitelist.2.domain = https://embedder2.example.com
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}embedDomainWhitelist.3.domain = 'self'
```


{% if isLeap %}
### EventHandler { #section_eventhandler .section }

Leap contains an event handling implementation that enables printing out all or specific events in the system log or in a separate file based on properties setting, by default this feature is not enabled. Change properties, in the Leap_config.properties file, to monitor events that you are interested in, and where you want to output the event information.

The following will output Events information in Application Server's system log at info or debug level:

- EventHandler.infoLevelEvents
- EventHandler.debugLevelEvents

**EventHandler.auditLevelEvents** will output to a file. The default file location on Windows is C:\febEvents.log and AIX/Linux is /febEvents.log, with maximum file size 5MB, back up to 5 files.

The content of the event output is in CSV format, the description of the data: Event topic, Event time stamp, User id, User email, Application uid, Application title, Form id, Record uid, Result

The following is the list of event topics that Leap sends out:

- builder/app/delete – Application is deleted
- builder/app/deploy – Application is deployed for the first time
- builder/app/redeploy – A deployed application is deployed again
- builder/app/stop – A deployed application is stopped
- builder/app/import – Application is imported
- builder/app/importAndDeploy – Application is imported and deployed
- builder/app/importAndDeployWithData – Application is imported and deployed with data
- builder/app/export – Application is exported
- builder/app/exportWithData – Application is exported with data
- builder/app/upgrade – Application is upgraded
- builder/app/upgradeWithDataReplaced – Application is upgraded and the data replaced
- builder/app/result/export – Application data is exported from View Data (or REST API)
- builder/app/retrieve/source – Application source is retrieved
- builder/app/query/deployed – Application deployment state is queried
- builder/record/submit – A record is submitted by normal app usage
- builder/record/update – A record is updated by normal app usage
- builder/record/delete – A record is deleted by normal app usage
- builder/data/insert/user – A record is created as a result of a direct user action
- builder/data/insert/code – A record is created indirectly
- builder/data/update/user – A record is updated as a result of a direct user action
- builder/data/update/code – A record is updated indirectly
- builder/data/delete/user – A record is deleted as a result of a direct user action
- builder/data/delete/code – A record is deleted indirectly

To capture failed events, use "builder/error/[EVENT_TOPIC]"

**Example:**

``` 
 ibm.nitro.EventHandler.infoLevelEvents=builder/record/submit,builder/error/builder/record/submit
```
{% endif %}


### exportDataWithEmails { #section_exportdatawithemails .section }

By default when you export data from applications, emails are also exported. You can exclude emails from the export by changing the property value to false.

Where:
- true; emails are exported with application data
- false; emails are not exported with application data

Default value: true

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}exportDataWithEmails=true
```

{% if isLeap %}
### GraphApiMemberManager.credentialAlias ###

The name of a credential alias that contains the id and secret for retrieving an OAuth token from {{msEntraName}} (Azure AD).  Refer to [Configure the credential alias for communicating with {{msEntraName}}](azure_lookups.md#entra_credential_alias) for more details.

**Example:**

```
ibm.nitro.NitroConfig.GraphApiMemberManager.credentialAlias=azureAlias
```

!!!note
    To enable Leap to search for users or groups in {{msEntraName}}, you must also configure the [tenantId](#graphapimembermanagertenantid), and the [member manager type](#membermanagertype).


### GraphApiMemberManager.tenantId ###

The tenant id of the {{msEntraName}} (Azure AD) instance.

**Example:**
```
ibm.nitro.NitroConfig.GraphApiMemberManager.tenantId=11111111-1111-1111-1111-111111111111
```

!!!note
    To enable Leap to search for users or groups in {{msEntraName}}, you must also configure a [credential alias](#graphapimembermanagercredentialalias) and the [member manager type](#membermanagertype).
{% endif %}

### hclMXFoundryApps { #section_mxfoundry .section }

The **hclMXFoundryApps** property defines the settings for connecting {{shortProductName}} to HCL Volt MX Foundry integration services.

This property contains the following parts:

- hclMXFoundryApps.enabled
- hclMXFoundryApps.[N].appName
- hclMXFoundryApps.[N].serviceUrl
- hclMXFoundryApps.[N].credentialAlias
{% if isLeap %}
- hclMXFoundryApps.[N].userTracking
{% endif %}

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.enabled = true
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.1.appName = Foundry App 1
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.1.serviceUrl = http://myFoundryServer/authService/100000002/appconfig
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.1.credentialAlias = FOUNDRY_APP1
{% if isLeap %}ibm.nitro.NitroConfig.hclMXFoundryApps.1.userTracking = true{% endif %}
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.2.appName = Foundry App 2
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.2.serviceUrl = https://100002720.myFoundryCloudServer/appconfig
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryApps.2.credentialAlias = FOUNDRY_APP2
{% if isLeap %}ibm.nitro.NitroConfig.hclMXFoundryApps.2.userTracking = false{% endif %}
```
{% if isLeap %}
!!! note
    Only one Foundry app can be used for user tracking, meaning that only one app can have userTracking=true
{% endif %}

### hclMXFoundryAppsCacheRefreshMins { #section_mxfoundrycache .section }

The **hclMXFoundryAppsCacheRefreshMins** property defines the amount of time in minutes that MX Foundry service descriptions are held in memory.  The default value is 60.

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}hclMXFoundryAppsCacheRefreshMins=60
```

### imageDomainWhitelist { #section_imagedomain .section }

The **imageDomainWhitelist** config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.

In addition to setting the following:

**imageDomainWhitelist.enabled=true** for each domain an additional parameters must be set.

**imageDomainWhitelist.[N].domain =** where "[N]" is an integer number identifying that service.

domain - The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.

**Examples:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}imageDomainWhitelist.enabled=true
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}imageDomainWhitelist.[1].domain=http://acme.com
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}imageDomainWhitelist.[2].domain=http://acme2.com
```



### InfoEntryPoint.dailyInfo { #section_infoentrypoint .section }

Provides HTML content that is shown in the login screen. Can be used for status messages, or help.

``` 
{% if isLeap %}ibm.nitro.{% endif %}InfoEntryPoint.dailyInfo = Welcome to **HCL {{shortProductName}}**
```


{% if isLeap %}
### LogoutServlet.postLogoutRedirectURL { #section_logout .section }

The value of this parameter tells {{shortProductName}} where to redirect user after log off. If the parameter is not configured or left blank, the user is redirected to the login page.

**Example:**

``` 
ibm.nitro.LogoutServlet.postLogoutRedirectURL=http://example_url.com/signout
```
{% endif %}


### maximumRecordsToRetrieve { #section_maximumrecords .section }

Maximum number of records that are permitted for export from the View Data page at one time. If the number of records to be exported exceeds the number set by this property, the export is stopped, and an error message is shown.

!!! note
    The default value of 20,000 is supported for base systems. Setting the value higher could result in poor performance, depending on result set size and server hardware.

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}maximumRecordsToRetrieve=25000
```


{% if isLeap %}
### MemberManager { #section_membermanager .section }

For WebSphere Application Server only, to configure the Leap to use the WebSphere VMM.

- MemberManager.adminAlias
- MemberManager.userProps.loginName
- MemberManager.userProps.id
- MemberManager.groupProps.id
- MemberManager.userProps.email
- MemberManager.userProps.displayName


The **MemberManager.adminAlias** default is a J2C alias named **vmmAdmin** to authenticate with VMM. You must configure it here if you want to change the J2C alias name.

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
ibm.was.MemberManager.adminAlias = vmmAdmin
ibm.was.MemberManager.userProps.loginName = mail 
ibm.was.MemberManager.userProps.id = mail
ibm.was.MemberManager.groupProps.id = name
ibm.was.MemberManager.userProps.email = mail
ibm.was.MemberManager.userProps.displayName = cn
```

### MemberManagerType ###

Used to configure Leap to perform user/group lookups against a configured {{msEntraName}} (Azure Active Directory).  The only valid value is **ms-azure-ad**.

!!!note
    To enable Leap to search for users or groups in {{msEntraName}}, you must also configure the [GraphApiMemberManager.credentialAlias](#graphapimembermanagercredentialalias) and [GraphApiMemberManager.tenantId](#graphapimembermanagertenantid).

**Example:**

```
ibm.nitro.NitroConfig.memberManagerType=ms-azure-ad
```
{% endif %}


### protectSensitiveActions

Records cannot be deleted using the REST API by default. Set to **false**, to enable delete actions.

Default value: true

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}protectSensitiveActions=false
```


### purgeOrphanFilesHours { #section_purgefileshours .section }

In some circumstances, files attached to either application designs or user-submitted records can become orphaned if the primary design or record element is removed outside the normal process. File records which are older than this number of hours and are no longer associated with an existing primary record are removed.

Default value: 48

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}purgeOrphanFilesHours=36
```

### reauthInNewWindow { #section_reauthInNewWindow .section }

Helps with seamless re-authentication when {{shortProductName}} is using an external IdP (in SAML or OIDC configurations), so that {{shortProductName}} users do not lose their work.  When set to `true`, the authentication flow is presented in a pop-up window, which is typically adequate for most external IdPs. It is recommended to use this setting in conjunction with `{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}reauthOnFailedRequest`.

Default value: false

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}reauthInNewWindow=true
```

### reauthOnFailedRequest { #section_reauthOnFailedRequest .section }

Helps with seamless re-authentication when {{shortProductName}} is using an external IdP (in SAML or OIDC configurations) so that {{shortProductName}} users do not lose their work.  When set to `true`, a failed XHR request triggers the authentication flow. A failed request is the typical result when an SAML or OIDC session has timed-out. It is recommended to use this setting in conjunction with `{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}reauthInNewWindow`. 

**Known Limitations**: There is no mechanism in the browser for the {{shortProductName}} code to distinguish a session time-out failure from other types of failures, such as a loss of internet connectivity. Enabling this setting means that *any* XHR request failure will trigger an authentication flow, even if it is not appropriate. However, for the majority of cases this setting will help {{shortProductName}} users to not lose their work, therefore it is recommended.

Default value: false

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}reauthOnFailedRequest=true
```

{% if isLeap %}
### rootAdminId { #section_rootAdminId .section }

The **rootAdminId** setting defines the login id of a user that will always have access to the Admin Configuration page.

**Example**

```
ibm.nitro.NitroConfig.rootAdminId=adminUser
```
{% endif %}


### runtimeCSP { #section_runtimecsp .section }

The **runtimeCSP** setting defines the `Content-Security-Policy` (CSP) header that will be applied to running Forms.

!!! note
    This setting only applies to Forms. It does not currently apply to App Pages, Summary Charts, or the View Data page.

For more information on CSP, see [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) in the Mozilla documentation.

For more information on <i>Strict</i> CSP, see [Strict CSP](leap_strict_csp.md)

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeCSP=default-src 'self' *.example.com; img-src *
```



### runtimeResources.[N] { #section_runtimeresources .section }

Additional web resources to load into the {{shortProductName}} UI for leveraging the [Custom Widget API](customwidgetapi_landing.md). The values from these settings will be injected into the `&lt;head&gt;` section of {{shortProductName}}'s HTML pages.

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css'>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.2 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.3 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
```



### secureJS { #section_securejs .section }

Enables or disables JavaScript restrictions in run time forms. When a form designer adds custom JavaScript to an application, this flag restricts the scope of that custom JavaScript. This flag applies to the entire {{shortProductName}} server for all users.

!!! note
    Setting this parameter to `false` might expose users to malicious JavaScript. Only set to `false` in a secured environment where {{shortProductName}} applications are created by trusted users.

For more information, see <a href="ref_javascript_api.html">JavaScript API</a> for {{shortProductName}}.

Default value: true

**Example:**

``` 
{% if isLeap %}ibm.nitro.ApplicationCompilerService.{% endif %}secureJS = false
```



### serviceAuthorization { #section_serviceauthorization .section }

Access to a service description may be given to a specific user, group, or special assignment. The access control is made up of two parts:

- Who may "discover" and work with the service while designing an application.
- Who may "invoke" the service.

{% if isLeap %}
Users or Groups provided must be defined using the attributes defined by `ibm.was.MemberManager.userProps.id = mail` and `ibm.was.MemberManager.groupProps.id = name` respectively.
{% else %}
Users or Groups provided must be defined using the fully qualified common name, i.e. CN=Frank Ford/Acme or CN=IT Users/Acme
{% endif %}

Special assignment valid values are:

- all-authenticated: for app author "discover" privilege only
- anonymous: for app authors and end-user "discover" and "invoke" privileges
- all-authors: for end-user "invoke" privilege only

To enable service authorizations, set `{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serviceAuthorization.enabled=true`. Multiple services may be defined. To define a service authorization, add `{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serviceAuthorization.serviceIdN` where **serviceIdN** is the 'id' of the service description. The value must be a valid JSON string, see provided samples.

!!! note
    A backslash (\) at the end of a line can be used to present a value over multiple lines. The backslash must be the very last character on the line.

**Examples:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serviceAuthorization.enabled = true
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serviceAuthorization.serviceId1 = { \
   "comment": "Auth for Service 1", \
   "discover": { "users": ["user1"], "groups": ["group1"], "special": [] }, \
   "invoke": { "users": [], "groups": [], "special": ["all-authenticated"]" } \
}
```



### serverURI { #section_serveruri .section }

Indicates the base URI used for critical functions, including editing applications, and email. Must include everything necessary to connect to the {{shortProductName}} context, for example, /apps.

With this entry, all emailed links, and absolute links visible during {{shortProductName}} design time start with the following base URI regardless of what the user enters in the address bar.

**Example:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serverURI = https://leap.example.com/apps
```



### servicesWhitelist { #section_servicewhitelist .section }

The **servicesWhitelist** config settings define a white list of domains and HTTP actions that app authors are allowed to call directly from their applications using URL based services.

In addition to setting `servicesWhitelist.enabled=true`, for each service two additional parameters must be set:

- servicesWhitelist.[N].domain =
- servicesWhitelist.[N].actions =


The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.
The https or http protocol included in the domain property is respected. For example, a domain property of https://api.example.com only allows calls to secure SSL https://api.example.com/anything and not to non-secure http://api.example.com/anything.
The actions property is a comma-separated list of the HTTP actions allowed for a particular domain. Valid values are GET, PUT, POST, DELETE, HEAD, and PATCH. If the actions value is missing, no actions are allowed.

Where **[N]** is an integer number identifying that service.

Default value: true

**Examples:**

``` 
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}servicesWhitelist.enabled = true
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}servicesWhitelist.1.domain = example.com
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}servicesWhitelist.1.actions = GET
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}servicesWhitelist.2.domain = https://securehost.com
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}servicesWhitelist.2.actions = GET, POST,PUT
```

!!! note
    This white-list has no effect on service descriptions and custom service transports that were installed on the server by the administrator.


{% if isLeap %}
### SetupAll.setupStatus { #section_setupall .section }

After deploying {{shortProductName}} for the first time or upgrading to a newer version, there is a setup screen that is presented upon accessing the manage page. This setup screen shows the status of detecting and updating the database tables, checks that security is properly enabled, and a mail session is configured. This page requires the admin to click a button to fully progress through the setup.

To disable this setup page and required admin interaction add the property: 

**Example:**
``` 
ibm.nitro.SetupAll.setupStatus = start
```
{% endif %}


{% if isLeap %}
### userGroups ###

It is set to **false** if group information is not available and to **true** if ID token contains group information. If **true**, ensure OIDC  groupIdentifier attribute matches correct claim in the ID token, for more details refer to [Configuring Leap with OIDC](helm_oidc_config.md).

**Example:**

```
ibm.nitro.NitroConfig.userGroups=false
```
### userLookup ###

It is set to **false** if LDAP directory is not available and to **true** if an LDAP is available and configured an OIDC client with mapIdentityToRegistryUser="true".  For more details refer to [Configuring Leap with OIDC](helm_oidc_config.md).

**Example:**

```
ibm.nitro.NitroConfig.userLookup=false
```

### userLookupGroups ###

It is set to **false** if LDAP directory is not available or if it does not support searching for groups.  And it is set to **true** if directory has group information and the OIDC groupIdentifier matches the attribute that identifies groups in the directory.  For more details refer to [Configuring Leap with OIDC](helm_oidc_config.md).

**Example:**

```
ibm.nitro.NitroConfig.userLookupGroups=false
```
{% endif %}

### viewResponsesMaximumCount { #section_viewresponsecount .section }

For DB2® or Oracle. The maximum number of records that are <i>counted</i> when returning record sets in pages. If the total number of records exceeds viewResponsesMaximumCount, then paging indicators will no longer accurately lists the total number of pages. Setting this value higher can have performance consequences for the server if there are many users viewing forms with large response lists.

Default value: 1000

**Example:**

```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}viewResponsesMaximumCount=2000
```


### <strike>xFrameOptions</strike> { #section_xframeoption .section }

Deprecated. Use [embedDomainWhitelist](#embedDomainWhitelist).



**Parent topic:** {% if isLeap %}[Configuring the properties file](co_configuring_the_properties_file.md){% else %}[Configuring](co_config_toc.md){% endif %}

