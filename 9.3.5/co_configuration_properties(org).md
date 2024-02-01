# Configuration properties 
The following table contains a list of properties in the HCL Leap Leap\_config.properties file. You can adjust the settings listed in the file, or add your own for a custom configuration.

Table 1. List of properties in the Leap_config.properties configuration file

|Setting|Description|
|:------|:----------|
|adminInfo |You can provide the user more contact information when the following error message is shown. If the message is “We are unable to process your request. If this error persists, report the problem to your administrator at **adminInfo1**, or **adminInfo2**, and provide error reference: XXX.” You provide **adminInfo1** and **adminInfo2**. If you provide only **adminInfo1**, then the message is shortened.|
| | **Examples:**  |
| | ``` {#codeblock_pr5_gcf_gzb} 
ibm.nitro.NitroConfig.adminInfo1 = admin@yourcompany.com 
ibm.nitro.NitroConfig.adminInfo2 = 1-800-GET-HELP
```|
|anonBlockedMsg=Anonymous access blocked|When a user attempts to access a Leap application anonymously, an error message is displayed. The default message is “Anonymous access blocked”. You can change the default message to provide additional information to the user.

 **Example:**

``` {#codeblock_cwf_tdf_gzb}
ibm.nitro.NitroConfig.anonBlockedMsg=Anonymous access blocked
```

|
|appFilesWhiteList

 appFilesBlackList

 appFilesMaxSize

|List of allowed \(WhiteList\), and not allowed \(BlackList\) of mimetypes, and the number of maximum file sizes for Application File uploads.

 **appFilesWhiteList** – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – empty \(everything is allowed\)

 **appFilesBlackList** – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – exe

 **appFilesMaxSize** \(size in kb\) – A space separated list of:

-   mimetypes – text/plain application/ /vnd.xfdl
-   file extensions – GIF PDF XML or default as special type
-   default value – 5000

 **Examples:**

``` {#codeblock_kwd_wbf_gzb}
ibm.nitro.NitroConfig.appFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi 
ibm.nitro.NitroConfig.appFilesBlackList =exe 
ibm.nitro.NitroConfig.appFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.appFilesMaxSize.50000 = mov avi
```

|
|appStats.timerEnabled

 appStats.refreshHour

 appStats.refreshDays

|By default, the timer is enabled and the collection time is set to 3am daily local server timer.**Note:** Depending on the volume of applications, statistics collection may take 10+ minutes, adjust the timer and frequency to server quiet time.

 **appStats.timerEnabled**Enable Application Statistics collection.

To disable Application Statistics collection, set to false.

Default value: true

**appStats.refreshHour**Sets the hour of day to start Application Statistics collection.

Value 0 to 23, indicating the hour of day to start the statistics collection process.

Default value: 3

**appStats.refreshDays**Sets the Application Statistics collection day. Use full names of day of the week, separated by a comma, semicolon, or space.

Valid values: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday

Default value: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday

**Examples:**

``` {#codeblock_kqt_sy2_gzb}
ibm.nitro.NitroConfig.appStats.timerEnabled=true 
ibm.nitro.NitroConfig.appStats.refreshDays=Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday
ibm.nitro.NitroConfig.appStats.refreshHour=3
```

|
|attachmentFilesWhiteList

 attachmentFilesBlackList

 attachmentFilesMaxSize

|List of allowed \(WhiteList\), and not allowed \(BlackList\) of mimetypes, and the number of maximum file sizes for the Attachment form item.

 **attachmentFilesWhiteList** – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – empty \(everything is allowed\)

 **attachmentFilesBlackList** – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – exe js html svg

 **attachmentFilesMaxSize** \(size in kb\) – A space separated list of:

-   mimetypes – text/plain application/ /vnd.xfdl
-   file extensions – GIF PDF XML or default as special type
-   default value – 5000

 **Examples:**

``` {#codeblock_hvz_bcf_gzb}
ibm.nitro.NitroConfig.attachmentFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi
ibm.nitro.NitroConfig.attachmentFilesBlackList =exe 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.50000 = mov avi
```

|
|blockAnonAccess|As of Leap 8.5.1 anonymous access is no longer allowed by default. To complete a Leap application or survey, users must authenticate with a valid user ID and password. Where:

-   enabled - anonymous access is blocked
-   disabled - anonymous access is allowed
-   redirect - redirects the user to authenticate

**Note:** Redirection is not available for Leap with WebSphere® Portal.


Default value: redirect

**Example:**

``` {#codeblock_ksj_ldf_gzb}
ibm.nitro.NitroConfig.blockAnonAccess=redirect
```

|
|customThemes.\[ID\].displayName

 customThemes.\[ID\].location

 customThemes.\[ID\].isDefault

 customThemes.\[ID\].nl.\[LOCALE\]

|The **customThemes config** settings define a list of customer-provided themes that can be used in Leap applications.

 For each theme, two parameters must be set:

-   **customThemes.\[ID\].displayName**
-   **customThemes.\[ID\].location**

 **\[ID\]** - An identifier for the custom theme \(e.g. "corpTheme1"\).

 The id can contain the letters 'a' through 'z' and numbers, and must start with a letter.

 **displayName** - The theme name to be displayed in the Leap authoring UI.

 **location** -The full URL of the theme's .css file.

 For each theme, there are 2 optional parameters:

-   **customThemes.\[ID\].isDefault**
-   **customThemes.\[ID\].nl.\[LOCALE\]**

 **isDefault** - If set to true, designates the theme as the default selection for new applications.

 **nl.\[LOCALE\]** - For globalization support of the theme's display name. **\[LOCALE\]** is the locale code that identifies the language \(e.g.,"en", "fr", "fr\_CA", "zh"\).

 After modifying these settings, restart the http task to see the changes in the authoring environment. If the location property of a theme is modified, any deployed applications using that custom theme need to be redeployed for changes to take affect.

 **Examples:**

 ``` {#codeblock_wgh_s51_hzb}
customThemes.corpTheme1.displayName = Corporate Theme 1
customThemes.corpTheme1.nl.fr = Thème d'entreprise 1
customThemes.corpTheme1.nl.zh = 企业主题1
customThemes.corpTheme1.isDefault = true
customThemes.corpTheme1.location =https://mycompany.com/theme1.css
```

|
|detectBrowser|If Leap detects an unsupported browser, a warning message is displayed to the user. The user can still see the form after the warning message is closed.Where:

-   warn - The user is warned that the browser is unsupported. A list of supported browsers is displayed in the warning message. When the user closes the warning message, the form is displayed.
-   ignore - The user is not warned that the browser is unsupported, and the form is displayed.

Default value: warn

**Example:**

``` {#codeblock_iqt_j2f_gzb}
ibm.nitro.NitroConfig.detectBrowser=warn
```

|
|disableUseTab|Hides the "Use" tab, and prevents fetching the list of deployed and usable applications.Where:

-   true - "Use" tab is hidden
-   false - "Use" tab is displayed

Default value: false

**Example:**

``` {#codeblock_dcl_mcf_gzb}
ibm.nitro.NitroConfig.disableUseTab=true
```

|
|EventHandler.infoLevelEvents

 EventHandler.debugLevelEvents

 EventHandler.auditLevelEvents

|Leap contains an event handling implementation that enables printing out all or specific events in the system log or in a separate file based on properties setting, by default this feature is not enabled. Change properties, in the Leap\_config.properties file, to monitor events that you are interested in, and where you want to output the event information.The following will output Events information in Application Server's system log at info or debug level:

-   **EventHandler.infoLevelEvents**
-   **EventHandler.debugLevelEvents**

**auditLevelEvents** will output to a file. The default file location on Windows is c:\\febEvents.log and AIX/Linux is /febEvents.log, with maximum file size 5MB, back up to 5 files.

The content of the event output is in CSV format, the description of the data: Event topic, event issued time stamp, user id, user email, Leap application id, Leap application name, Leap application Form short name, Record Id, result

The following is the list of event topics that Leap sends out:

-   "builder/app/delete" – Application is deleted
-   "builder/app/deploy" – Application is deployed for the first time
-   "builder/app/redeploy" – A deployed application is deployed again
-   "builder/app/stop" – A deployed application is stopped
-   "builder/app/import" – Application is imported
-   "builder/app/importAndDeploy" – Application is imported and deployed
-   "builder/app/importAndDeployWithData" – Application is imported and deployed with data
-   "builder/app/export" – Application is exported
-   "builder/app/exportWithData" – Application is exported with data
-   "builder/app/upgrade" – Application is upgraded
-   "builder/app/upgradeWithDataReplaced" – Application is upgraded and the data replaced
-   "builder/app/result/export" – Application data is exported from View Data \(or REST API\)
-   "builder/app/retrieve/source"
-   "builder/app/query/deployed"
-   "builder/record/submit" – A form is submitted
-   "builder/record/update" – A specific form record is updated
-   "builder/record/delete" – A specific form record is deleted
-   "builder/data/insert/user"
-   "builder/data/insert/code"
-   "builder/data/update/user"
-   "builder/data/update/code"
-   "builder/data/delete/user"
-   "builder/data/delete/code"

To capture failed events, use "builder/error" + mainEventCode

**Example:**

``` {#codeblock_ekf_cv1_hzb}
 ibm.nitro.EventHandler.infoLevelEvents=builder/record/submit,builder/error/submit
```

|
|exportDataWithEmails|By default when you export data from applications, emails are also exported. You can exclude emails from the export by changing the property value to false.

 Where:

-   true - emails are exported with application data
-   false - emails are not exported with application data

Default value: true

 **Example:**

``` {#codeblock_qgd_zdf_gzb}
ibm.nitro.NitroConfig.exportDataWithEmails=true
```

|
|imageDomainWhitelist.enabled=true

 imageDomainWhitelist.\[N\].domain

|The **imageDomainWhitelist** config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.

 In addition to setting the following:

 **imageDomainWhitelist.enabled=true** for each domain an additional parameters must be set.

 **imageDomainWhitelist.\[N\].domain =** where "\[N\]" is an integer number identifying that service.

 domain - The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything,http://api.example.com/anything , or https://example.com/anything.

 **Examples:**

``` {#codeblock_msm_fv1_hzb}
ibm.nitro.imageDomainWhitelist.enabled=true
ibm.nitro.imageDomainWhitelist.[1].domain=http://acme.com
ibm.nitro.imageDomainWhitelist.[2].domain=http://acme2.com
```

|
|InfoEntryPoint.dailyInfo|Provides HTML content that is shown at the end of the login screen. Can be used for status messages, or help.**Example:**

``` {#codeblock_igw_mbf_gzb}
ibm.nitro.InfoEntryPoint.dailyInfo = Welcome to **HCL Leap**
```

|
|LogoutServlet.postLogoutRedirectURL|The value of this parameter tells Leap where to redirect user after log off. If the parameter is not configured or left blank, the user is redirected to the login page.

 **Example:**

 ``` {#codeblock_zxm_42f_gzb}
ibm.nitro.LogoutServlet.postLogoutRedirectURL=http://example_url.com/signout
```

|
|maximumRecordsToRetrieve|Maximum number of records that are permitted for export from the View Data page at one time. If the number of records to be exported exceeds the number set by this property, the export is stopped, and an error message is shown.

 **Note:** The default value of 20,000 is supported for base systems. Setting the value higher results in poor performance, depending on result set size and server hardware.

 **Example:**

``` {#codeblock_qy1_1df_gzb}
ibm.nitro.NitroConfig.maximumRecordsToRetrieve=25000
```

|
|MemberManager.adminAlias

 MemberManager.userProps.loginName

 MemberManager.userProps.id

 MemberManager.groupProps.id

 MemberManager.userProps.email

 MemberManager.userProps.displayName

|**MemberManager.adminAlias** setting is mandatory. For WebSphere Application Server only, configure the VMM login.

By default, Leap uses J2C alias **vmmAdmin** to authenticate with VMM. You must configure it here if you want to change the J2C alias name.

You must have WebSphere Application Server administrative user credentials to run Leap

If you use LDAP within WebSphere Application Server, there are a number of properties that look up user and group information. If your LDAP uses different property keys than the ones set by default, update the property keys here so that user and group look up function correctly.

If you are using LDAP within WebSphere Application Server, refer to the following settings:

**MemberManager.userProps.loginName**

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

``` {#codeblock_ufc_cbf_gzb}
ibm.was.MemberManager.userProps.loginName = mail 
ibm.was.MemberManager.userProps.id = mail
ibm.was.MemberManager.groupProps.id = name
ibm.was.MemberManager.userProps.email = mail
ibm.was.MemberManager.userProps.displayName = cn
```

|
|purgeOrphanFilesHours|In some circumstances, files attached to either application designs or user-submitted records can become orphaned if the primary design or record element is removed outside the normal process. File records which are older than this number of hours and are no longer associated with an existing primary record are removed by a clean-up agent in VoltBuilder.nsf.

 Default value: 48

 **Example:**

``` {#codeblock_n4r_3v1_hzb}
ibm.nitro.purgeOrphanFilesHours=36
```

|
|runtimeCSP|The **runtimeCSP** setting defines the `Content-Security-Policy` header that will be applied to running Forms.

 **Note:** This setting only applies to Forms. It does not currently apply to App Pages, Summarry Charts, or the View Data page.

 For more information, see [https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP](https://apc01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FHTTP%2FCSP&data=05%7C01%7Cnatalie.mezzina%40hcl.com%7C8a7d42f352b44ca3836e08dacdb6b55a%7C189de737c93a4f5a8b686f4ca9941912%7C0%7C0%7C638048482179359357%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=EaK4MB589PFSRNjwx%2BZebUAajhhBcSLoGfPuyha2eY8%3D&reserved=0)

 For more information on Strict CSP, see [Strict CSP](leap_strict_csp.md).

 **Example:**

``` {#codeblock_jhw_cz2_gzb}
ibm.nitro.NitroConfig.runtimeCSP=default-src 'self' *.example.com; img-src *
```

|
|runtimeResources.\[N\]|Additional web resources to load into the Domino Leap UI for leveraging the [Custom Widget API](customwidgetapi_landing.md). The values from these settings will be injected into the *<head\>* section of Domino Leap's HTML pages.**Example:**

``` {#codeblock_o4c_kv1_hzb}
ibm.nitro.NitroConfig.runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css'>
ibm.nitro.NitroConfig.runtimeResources.2 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
ibm.nitro.NitroConfig.runtimeResources.3 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
```

|
|secureJS|Enables or disables JavaScript security in run time forms. When a form designer adds custom JavaScript to an application, this flag applies security settings to the custom JavaScript. This flag applies to the entire Leap server for all users.

**Note:** Setting this parameter to `FALSE` might expose users to malicious JavaScript. Only set to `FALSE` in a secured environment where Leap applications are created by trusted users.

 For more information, see [JavaScript API](ref_javascript_api.md) for Leap.

 Default value: true

 **Example:**

``` {#codeblock_rch_njf_gzb}
ibm.nitro.ApplicationCompilerService.secureJS = true
```

|
|serviceAuthorization.enabled

 serviceAuthorization.jxpath-sample

|Access to a service description may be given to a specific user, group, or special assignment. The access control is made up of two parts:-   Who may discover and work with the service while designing an application.
-   Who may run the service.

 Users or Groups provided must be defined using the attributes defined by `ibm.was.MemberManager.userProps.id = mail` and `ibm.was.MemberManager.groupProps.id = name` respectively.Special assignment valid values are:-   all-authenticated: for app author "discover" privilege only
-   anonymous: for app authors and end-user "discover" and "invoke" privileges
-   all-authors: for end-user "invoke" privilege only

To enable service authorizations, set `ibm.nitro.NitroConfig.serviceAuthorization.enabled=true`.Multiple services may be defined. To define a service authorization, add `ibm.nitro.NitroConfig.serviceAuthorization.serviceIdN` where **serviceIdN** is the 'id' of the service description. The value must be a valid JSON string, see provided samples.**Note:** A backslash \(\\\) at the very end of a line can be used to present a value over multiple lines. The backslashmust be the very last character on the line.

**Examples:**

``` {#codeblock_lpq_w3f_gzb}
ibm.nitro.NitroConfig.serviceAuthorization.enabled = true
ibm.nitro.NitroConfig.serviceAuthorization.jxpath-sample = {{"comment": 
"Sample 1","discover": { "users": [ "user1" ], "groups": [],"special": [] }, "invoke": 
{ "users": [ "user1"], "groups": [], "special": [] } }
```

|
|serverURI|Indicates the base URI used for critical functions, including editing applications, and email. Must include everything necessary to connect to the Leap context, for example, /apps.

With this entry, all emailed links, and absolute links visible during Leap design time start with the following base URI regardless of what the user enters in the address bar.**Example:**

``` {#codeblock_ggl_gdf_gzb}
ibm.nitro.NitroConfig.serverURI = http://host:9080/apps
```

|
|servicesWhitelist.enabled

 servicesWhitelist.\[N\].actions

 servicesWhitelist.\[N\].domain

|The **servicesWhitelist** config settings define a white list of domains and HTTP actions that app authors are allowed to call directly from their applications using URL based services.

 In addition to setting `servicesWhitelist.enabled=true`, for each service two additional parameters must be set:

-   **servicesWhitelist.\[N\].domain =**
-   **servicesWhitelist.\[N\].actions =**

 The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything,http://api.example.com/anything , or https://example.com/anything.

 The https or http protocol included in the domain property is respected. For example, a domain property of https://api.example.com only allows calls to secure SSL https://api.example.com/anything and not to non-secure http://api.example.com/anything.

 The actions property is a comma-separated list of the HTTP actions allowed for a particular domain. Valid values are GET, PUT, POST, and DELETE. If the actions value is missing, no actions are allowed.

 Where **\[N\]** is an integer number identifying that service. For more information, see the servicesWhitelist documents in VoltConfig.nsf.

 Default value: true

 **Examples:**

 ``` {#codeblock_qdk_2ff_gzb}
ibm.nitro.NitroConfig.servicesWhitelist.enabled = true
ibm.nitro.NitroConfig.servicesWhitelist.1.domain = example.com
ibm.nitro.NitroConfig.servicesWhitelist.1.actions = GET
ibm.nitro.NitroConfig.servicesWhitelist.2.domain = https://securehost.com
ibm.nitro.NitroConfig.servicesWhitelist.2.actions = GET, POST,PUT
```

 **Note:** This white-list has no effect on service descriptions and custom service transports that were installed on the server by the administrator.

|
|SetupAll.setupStatus|After deploying Leap for the first time or upgrading to a newer version, there is a setup screen that is presented upon accessing the manage page. This setup screen shows the status of detecting and updating the database tables, checks that security is properly enabled, and a mail session is configured. This page requires the admin to click a button to fully progress through the setup. To disable this setup page and required admin interaction add the property `ibm.nitro.SetupAll.setupStatus = start`.

 **Example**:

``` {#codeblock_twt_qs5_jzb}
ibm.nitro.SetupAll.setupStatus = start
```

|
|viewResponsesMaximumCount|For WebSphere Application Server with DB2®, or Oracle. The maximum number of records that View Response counts up to when returning large record sets. Larger values are still returned, but the paging no longer accurately lists the total number of pages. Setting this value higher can have performance consequences for the server if there are many users viewing forms with large response lists. **Example:**

``` {#codeblock_icw_vcf_gzb}
ibm.nitro.NitroConfig.viewResponsesMaximumCount=2000
```

|
|wchApiUrl|IBM Watson Content Hub API URL. This setting is optional. When set in the config, all Leap users will use the same Watson Content Hub tenant for selecting assets. When it's not set, Leap design users can set their own Watson Content Hub API URL at the time of use.ibm.nitro.NitroConfig.wchEnabled=true is required for this setting to work.

**Example:**

``` {#codeblock_vpt_zff_gzb}
ibm.nitro.NitroConfig.wchApiUrl=https://my1.digitalexperience.ibm.com/api/<guid>
```

|
|wchEnabled|Enables integration with [IBM Watson Content Hub](https://www.digitalexperience.ibm.com/). This allows Leap applications to select assets from IBM Watson Content Hub.Where:

-   true - enables a choice in the design experience that allows a design user to select assets from IBM Watson Content Hub \(a Watson Content Hub subscription is required\)
-   false - feature remains disabled

Default value: false

**Example:**

``` {#codeblock_nwj_tff_gzb}
ibm.nitro.NitroConfig.wchEnabled=false
```

|
|xFrameOptions|Use this setting to control the X-Frame-Options response header for Leap pages.

 **Example:**

``` {#codeblock_ld5_nff_gzb}
ibm.nitro.NitroConfig.xFrameOptions = SAMEORIGIN
```

|

**Parent topic:**[Configuring the properties file](co_configuring_the_properties_file.md)

