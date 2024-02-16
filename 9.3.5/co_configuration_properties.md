# Configuration properties 

The following table contains a list of properties in the HCL Leap Leap\_config.properties file. You can adjust the settings listed in the file, or add your own for a custom configuration.

Table 1. List of properties in the Leap_config.properties configuration file

<table class="table-wrap">
<tr>
<td> <b>Setting</b> </td><td> <b>Description</b> </td>
</tr>
<tr>
<td> adminInfo </td>
<td> You can provide the user more contact information when the following error message is shown. If the message is “We are unable to process your request. If this error persists, report the problem to your administrator at <b>adminInfo1</b>, or <b>adminInfo2</b>, and provide error reference: XXX.” You provide <b>adminInfo1</b> and <b>adminInfo2</b>. If you provide only <b>adminInfo1</b>, then the message is shortened.<br> 
<br>

<b>Examples:</b>
```
ibm.nitro.NitroConfig.adminInfo1 = admin@yourcompany.com 
ibm.nitro.NitroConfig.adminInfo2 = 1-800-GET-HELP
```
</td>
</tr>
<tr>
<td> anonBlockedMsg=Anonymous access blocked </td>
<td>

When a user attempts to access a Leap application anonymously, an error message is displayed. The default message is “Anonymous access blocked”. You can change the default message to provide additional information to the user.<br>
<br>

<b>Example:</b>
```
ibm.nitro.NitroConfig.anonBlockedMsg=Anonymous access blocked
```
</td>
</tr>
<tr> 
<td> appFilesWhiteList<br>appFilesBlackList<br>appFilesMaxSize </td>
<td>

List of allowed \(WhiteList\), and not allowed \(BlackList\) of mimetypes, and the number of maximum file sizes for Application File uploads.<br>
<br>

<b>appFilesWhiteList</b> – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – empty (everything is allowed)
<br>

<b>appFilesBlackList</b> – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – exe
<br>

<b>appFilesMaxSize</b> (size in kb) – A space separated list of:<br>

-   mimetypes – text/plain application/ /vnd.xfdl<br>
-   file extensions – GIF PDF XML or default as special type<br>
-   default value – 5000<br>
<br>

<b>Examples:</b>
```
ibm.nitro.NitroConfig.appFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi 
ibm.nitro.NitroConfig.appFilesBlackList =exe 
ibm.nitro.NitroConfig.appFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.appFilesMaxSize.50000 = mov avi
```
</td>
</tr>
<tr>
<td>
appStats.timerEnabled

appStats.refreshHour

appStats.refreshDays
</td>
<td>
By default, the timer is enabled and the collection time is set to 3am daily local server timer.**Note:** Depending on the volume of applications, statistics collection may take 10+ minutes, adjust the timer and frequency to server quiet time.

<b>appStats.timerEnabled</b> Enable Application Statistics collection.

To disable Application Statistics collection, set to false.

Default value: true

<b>appStats.refreshHour</b> sets the hour of day to start Application Statistics collection.

Value 0 to 23, indicating the hour of day to start the statistics collection process.

Default value: 3

<b>appStats.refreshDays</b> Sets the Application Statistics collection day. Use full names of day of the week, separated by a comma, semicolon, or space.

Valid values: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday

Default value: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday<br>
<br>

<b>Examples:</b>

``` {#codeblock_kqt_sy2_gzb}
ibm.nitro.NitroConfig.appStats.timerEnabled=true 
ibm.nitro.NitroConfig.appStats.refreshDays=Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday
ibm.nitro.NitroConfig.appStats.refreshHour=3
```
</td>
</tr>
<tr>
<td>
attachmentFilesWhiteList

attachmentFilesBlackList

attachmentFilesMaxSize
</td>
<td>
List of allowed \(WhiteList\), and not allowed \(BlackList\) of mimetypes, and the number of maximum file sizes for the Attachment form item.

<b>attachmentFilesWhiteList</b> – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – empty \(everything is allowed\)

<b>attachmentFilesBlackList</b> – A space separated list of:

-   mimetypes – text/plain application/vnd.xfdl
-   partial mimetypes – text/audio/ /plain
-   file extensions – GIF PDF XML
-   default value – exe js html svg

<b>attachmentFilesMaxSize</b> (size in kb) – A space separated list of:

-   mimetypes – text/plain application/ /vnd.xfdl
-   file extensions – GIF PDF XML or default as special type
-   default value – 5000<br>
<br>

<b>Examples:</b>

``` {#codeblock_hvz_bcf_gzb}
ibm.nitro.NitroConfig.attachmentFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi
ibm.nitro.NitroConfig.attachmentFilesBlackList =exe 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.50000 = mov avi
```
</td>
</tr>
<tr>
<td> blockAnonAccess </td>
<td>
As of Leap 8.5.1 anonymous access is no longer allowed by default. To complete a Leap application or survey, users must authenticate with a valid user ID and password. Where:<br>

-   enabled - anonymous access is blocked<br>
-   disabled - anonymous access is allowed<br>
-   redirect - redirects the user to authenticate<br>

<b>Note:</b> Redirection is not available for Leap with WebSphere® Portal.<br>

Default value: redirect<br>
<br>

<b>Example:</b>
```
ibm.nitro.NitroConfig.blockAnonAccess=redirect
```

</td>
</tr>
<tr>
<td> customThemes.\[ID\].displayName<br>customThemes.\[ID\].location<br>customThemes.\[ID\].isDefault<br>customThemes.\[ID\].nl.\[LOCALE\] </td>
<td>
The <b>customThemes config</b> settings define a list of customer-provided themes that can be used in Leap applications.<br>
<br>

For each theme, two parameters must be set:<br>

-   <b>customThemes.\[ID\].displayName</b><br>
-   <b>customThemes.\[ID\].location</b><br>

<b>[ID]</b> - An identifier for the custom theme (e.g. "corpTheme1").<br>

The id can contain the letters 'a' through 'z' and numbers, and must start with a letter.<br>

<b>displayName</b> - The theme name to be displayed in the Leap authoring UI.<br>

<b>location</b> -The full URL of the theme's .css file.<br>

For each theme, there are 2 optional parameters:<br>

-   <b>customThemes.\[ID\].isDefault</b><br>
-   <b>customThemes.\[ID\].nl.\[LOCALE\]</b><br>

<b>isDefault</b> - If set to true, designates the theme as the default selection for new applications.<br>

<b>nl.\[LOCALE\]</b> - For globalization support of the theme's display name. <b>\[LOCALE\]</b> is the locale code that identifies the language (e.g.,"en", "fr", "fr_CA", "zh").<br>

After modifying these settings, restart the Leap server to see the changes in the authoring environment. If the location property of a theme is modified, any deployed applications using that custom theme need to be redeployed for changes to take affect.<br>
<br>

<b>Examples:</b><br>
 
``` {#codeblock_wgh_s51_hzb}
customThemes.corpTheme1.displayName = Corporate Theme 1
customThemes.corpTheme1.nl.fr = Thème d'entreprise 1
customThemes.corpTheme1.nl.zh = 企业主题1
customThemes.corpTheme1.isDefault = true
customThemes.corpTheme1.location =https://mycompany.com/theme1.css
```
</td>
</tr>
<tr>
<td> detectBrowser </td>
<td>
If Leap detects an unsupported browser, a warning message is displayed to the user. The user can still see the form after the warning message is closed.Where:<br>

-   warn - The user is warned that the browser is unsupported. A list of supported browsers is displayed in the warning message. When the user closes the warning message, the form is displayed.
-   ignore - The user is not warned that the browser is unsupported, and the form is displayed.

Default value: warn<br>
<br>

<b>Example:</b>

``` {#codeblock_iqt_j2f_gzb}
ibm.nitro.NitroConfig.detectBrowser=warn
```
</td>
</tr>
<tr>
<td style="width:5%">disableUseTab</td>
<td>
Hides the "Use" tab, and prevents fetching the list of deployed and usable applications.Where:

-   true - "Use" tab is hidden
-   false - "Use" tab is displayed

Default value: false<br>
<br>

<b>Example:</b>

``` {#codeblock_dcl_mcf_gzb}
ibm.nitro.NitroConfig.disableUseTab=true
```
</td>
</tr>
<tr>
<td>
EventHandler.infoLevelEvents

EventHandler.debugLevelEvents

EventHandler.auditLevelEvents
</td>
<td>
Leap contains an event handling implementation that enables printing out all or specific events in the system log or in a separate file based on properties setting, by default this feature is not enabled. Change properties, in the Leap\_config.properties file, to monitor events that you are interested in, and where you want to output the event information.The following will output Events information in Application Server's system log at info or debug level:

-   <b>EventHandler.infoLevelEvents</b>
-   <b>EventHandler.debugLevelEvents</b>

<b>auditLevelEvents</b> will output to a file. The default file location on Windows is c:\\febEvents.log and AIX/Linux is /febEvents.log, with maximum file size 5MB, back up to 5 files.

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

To capture failed events, use "builder/error" + mainEventCode<br>
<br>

<b>Example:</b>

``` {#codeblock_ekf_cv1_hzb}
 ibm.nitro.EventHandler.infoLevelEvents=builder/record/submit,builder/error/submit
```
</td>
</tr>
<tr>
<td>exportDataWithEmails</td>
<td>
By default when you export data from applications, emails are also exported. You can exclude emails from the export by changing the property value to false.

Where:

-   true - emails are exported with application data
-   false - emails are not exported with application data

Default value: true<br>
<br>

<b>Example:</b>

``` {#codeblock_qgd_zdf_gzb}
ibm.nitro.NitroConfig.exportDataWithEmails=true
```
</td>
</tr>
<tr>
<td>
imageDomainWhitelist.enabled=true

imageDomainWhitelist.\[N\].domain
</td>
<td>
The <b>imageDomainWhitelist</b> config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.

In addition to setting the following:

<b>imageDomainWhitelist.enabled=true</b> for each domain an additional parameters must be set.

<b>imageDomainWhitelist.\[N\].domain =</b> where "\[N\]" is an integer number identifying that service.

domain - The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything,http://api.example.com/anything , or https://example.com/anything.<br>
<br>

<b>Examples:</b>

``` {#codeblock_msm_fv1_hzb}
ibm.nitro.imageDomainWhitelist.enabled=true
ibm.nitro.imageDomainWhitelist.[1].domain=http://acme.com
ibm.nitro.imageDomainWhitelist.[2].domain=http://acme2.com
```
</td>
</tr>
<tr>
<td>InfoEntryPoint.dailyInfo</td>
<td>
Provides HTML content that is shown at the end of the login screen. Can be used for status messages, or help.**Example:**

``` {#codeblock_igw_mbf_gzb}
ibm.nitro.InfoEntryPoint.dailyInfo = Welcome to **HCL Leap**
```
</td>
</tr>
<tr>
<td>LogoutServlet.postLogoutRedirectURL</td>
<td>
The value of this parameter tells Leap where to redirect user after log off. If the parameter is not configured or left blank, the user is redirected to the login page.<br>
<br>

<b>Example:</b>

``` {#codeblock_zxm_42f_gzb}
ibm.nitro.LogoutServlet.postLogoutRedirectURL=http://example_url.com/signout
```
</td>
</tr>
<tr>
<td> maximumRecordsToRetrieve</td>
<td>
Maximum number of records that are permitted for export from the View Data page at one time. If the number of records to be exported exceeds the number set by this property, the export is stopped, and an error message is shown.<br>
<br>

<b>Note:</b> The default value of 20,000 is supported for base systems. Setting the value higher results in poor performance, depending on result set size and server hardware.<br>
<br>

<b>Example:</b>

``` {#codeblock_qy1_1df_gzb}
ibm.nitro.NitroConfig.maximumRecordsToRetrieve=25000
```
</td>
</tr>
<tr>
<td>
MemberManager.adminAlias

MemberManager.userProps.loginName

MemberManager.userProps.id

MemberManager.groupProps.id

MemberManager.userProps.email

MemberManager.userProps.displayName
</td>
<td>
<b>MemberManager.adminAlias</b> setting is mandatory. For WebSphere Application Server only, configure the VMM login.

By default, Leap uses J2C alias **vmmAdmin** to authenticate with VMM. You must configure it here if you want to change the J2C alias name.

You must have WebSphere Application Server administrative user credentials to run Leap

If you use LDAP within WebSphere Application Server, there are a number of properties that look up user and group information. If your LDAP uses different property keys than the ones set by default, update the property keys here so that user and group look up function correctly.

If you are using LDAP within WebSphere Application Server, refer to the following settings:

<b>MemberManager.userProps.loginName</b>

Describes the LDAP property used as the login ID. Each loginName must be unique.

Default setting: uid

<b>MemberManager.userProps.id</b>

Represents a unique key for the user. This key must be identical to the loginName.

Default setting: uid

<b>MemberManager.groupProps.id</b>

Represents a unique key for the group. The value is the LDAP property that is used. For example, cn, represents Common Name.

Default setting: cn

<b>MemberManager.userProps.email</b>

The email address of the user. Leap uses this email address to send notifications and other emails to the user.

Default setting: mail

<b>MemberManager.userProps.displayName</b>

Used to display the name of the user, instead of the login id.

Default setting: cn<br>
<br>

<b>Examples:</b>

``` {#codeblock_ufc_cbf_gzb}
ibm.was.MemberManager.userProps.loginName = mail 
ibm.was.MemberManager.userProps.id = mail
ibm.was.MemberManager.groupProps.id = name
ibm.was.MemberManager.userProps.email = mail
ibm.was.MemberManager.userProps.displayName = cn
```
</td>
</tr>
<tr>
<td>purgeOrphanFilesHours</td>
<td>
In some circumstances, files attached to either application designs or user-submitted records can become orphaned if the primary design or record element is removed outside the normal process. File records which are older than this number of hours and are no longer associated with an existing primary record are removed by a clean-up agent in VoltBuilder.nsf.

Default value: 48<br>
<br>

<b>Example:</b>

``` {#codeblock_n4r_3v1_hzb}
ibm.nitro.purgeOrphanFilesHours=36
```
</td>
</tr>
<tr>
<td>runtimeCSP</td>
<td>
The <b>runtimeCSP</b> setting defines the `Content-Security-Policy` header that will be applied to running Forms.<br>
<br>

<b>Note:</b> This setting only applies to Forms. It does not currently apply to App Pages, Summarry Charts, or the View Data page.

For more information, see [https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP](https://apc01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FHTTP%2FCSP&data=05%7C01%7Cnatalie.mezzina%40hcl.com%7C8a7d42f352b44ca3836e08dacdb6b55a%7C189de737c93a4f5a8b686f4ca9941912%7C0%7C0%7C638048482179359357%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=EaK4MB589PFSRNjwx%2BZebUAajhhBcSLoGfPuyha2eY8%3D&reserved=0)

For more information on Strict CSP, see [Strict CSP](leap_strict_csp.md).<br>
<br>

<b>Example:</b>

``` {#codeblock_jhw_cz2_gzb}
ibm.nitro.NitroConfig.runtimeCSP=default-src 'self' *.example.com; img-src *
```
</td>
</tr>
<tr>
<td>runtimeResources.\[N\]</td>
<td>
Additional web resources to load into the Domino Leap UI for leveraging the [Custom Widget API](customwidgetapi_landing.md). The values from these settings will be injected into the <b><head></b> section of Domino Leap's HTML pages.<br>
<br>

<b>Example:</b>

``` {#codeblock_o4c_kv1_hzb}
ibm.nitro.NitroConfig.runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css'>
ibm.nitro.NitroConfig.runtimeResources.2 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
ibm.nitro.NitroConfig.runtimeResources.3 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
```
</td>
</tr>
<tr>
<td>secureJS</td>
<td>
Enables or disables JavaScript security in run time forms. When a form designer adds custom JavaScript to an application, this flag applies security settings to the custom JavaScript. This flag applies to the entire Leap server for all users.

<b>Note:</b> Setting this parameter to `FALSE` might expose users to malicious JavaScript. Only set to `FALSE` in a secured environment where Leap applications are created by trusted users.

For more information, see [JavaScript API](ref_javascript_api.md) for Leap.

Default value: true<br>
<br>

<b>Example:</b>

``` {#codeblock_rch_njf_gzb}
ibm.nitro.ApplicationCompilerService.secureJS = true
```
</td>
</tr>
<tr>
<td>
serviceAuthorization.enabled

serviceAuthorization.jxpath-sample
</td>
<td>
Access to a service description may be given to a specific user, group, or special assignment. The access control is made up of two parts:-   Who may discover and work with the service while designing an application.

-   Who may run the service.

 Users or Groups provided must be defined using the attributes defined by `ibm.was.MemberManager.userProps.id = mail` and `ibm.was.MemberManager.groupProps.id = name` respectively.Special assignment valid values are:-   all-authenticated: for app author "discover" privilege only
-   anonymous: for app authors and end-user "discover" and "invoke" privileges
-   all-authors: for end-user "invoke" privilege only

To enable service authorizations, set `ibm.nitro.NitroConfig.serviceAuthorization.enabled=true`.Multiple services may be defined. To define a service authorization, add `ibm.nitro.NitroConfig.serviceAuthorization.serviceIdN` where <b>serviceIdN</b> is the 'id' of the service description. The value must be a valid JSON string, see provided samples.**Note:** A backslash \(\\\) at the very end of a line can be used to present a value over multiple lines. The backslashmust be the very last character on the line.<br>
<br>

<b>Examples:</b>

``` {#codeblock_lpq_w3f_gzb}
ibm.nitro.NitroConfig.serviceAuthorization.enabled = true
ibm.nitro.NitroConfig.serviceAuthorization.jxpath-sample = {{"comment": 
"Sample 1","discover": { "users": [ "user1" ], "groups": [],"special": [] }, "invoke": 
{ "users": [ "user1"], "groups": [], "special": [] } }
```
</td>
</tr>
<tr>
<td>serverURI</td>
<td>
Indicates the base URI used for critical functions, including editing applications, and email. Must include everything necessary to connect to the Leap context, for example, /apps.

With this entry, all emailed links, and absolute links visible during Leap design time start with the following base URI regardless of what the user enters in the address bar.**Example:**

``` {#codeblock_ggl_gdf_gzb}
ibm.nitro.NitroConfig.serverURI = http://host:9080/apps
```
</td>
</tr>
<tr>
<td>
servicesWhitelist.enabled

servicesWhitelist.\[N\].actions

servicesWhitelist.\[N\].domain
</td>
<td>
The <b>servicesWhitelist</b> config settings define a white list of domains and HTTP actions that app authors are allowed to call directly from their applications using URL based services.

In addition to setting `servicesWhitelist.enabled=true`, for each service two additional parameters must be set:

-   <b>servicesWhitelist.\[N\].domain =</b>
-   <b>servicesWhitelist.\[N\].actions =</b>

The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything,http://api.example.com/anything , or https://example.com/anything.

The https or http protocol included in the domain property is respected. For example, a domain property of https://api.example.com only allows calls to secure SSL https://api.example.com/anything and not to non-secure http://api.example.com/anything.

The actions property is a comma-separated list of the HTTP actions allowed for a particular domain. Valid values are GET, PUT, POST, and DELETE. If the actions value is missing, no actions are allowed.

Where <b>[N]<</b> is an integer number identifying that service. For more information, see the servicesWhitelist documents in VoltConfig.nsf.

Default value: true<br>
<br>

<b>Examples:</b>

``` {#codeblock_qdk_2ff_gzb}
ibm.nitro.NitroConfig.servicesWhitelist.enabled = true
ibm.nitro.NitroConfig.servicesWhitelist.1.domain = example.com
ibm.nitro.NitroConfig.servicesWhitelist.1.actions = GET
ibm.nitro.NitroConfig.servicesWhitelist.2.domain = https://securehost.com
ibm.nitro.NitroConfig.servicesWhitelist.2.actions = GET, POST,PUT
```

<br>
<b>Note:</b> This white-list has no effect on service descriptions and custom service transports that were installed on the server by the administrator.
</td>
</tr>
<tr>
<td>SetupAll.setupStatus</td>
<td>
After deploying Leap for the first time or upgrading to a newer version, there is a setup screen that is presented upon accessing the manage page. This setup screen shows the status of detecting and updating the database tables, checks that security is properly enabled, and a mail session is configured. This page requires the admin to click a button to fully progress through the setup. To disable this setup page and required admin interaction add the property `ibm.nitro.SetupAll.setupStatus = start`.<br>
<br>

<b>Example:</b>

``` {#codeblock_twt_qs5_jzb}
ibm.nitro.SetupAll.setupStatus = start
```
</td>
</tr>
<tr>
<td>viewResponsesMaximumCount</td>
<td>
For WebSphere Application Server with DB2®, or Oracle. The maximum number of records that View Response counts up to when returning large record sets. Larger values are still returned, but the paging no longer accurately lists the total number of pages. Setting this value higher can have performance consequences for the server if there are many users viewing forms with large response lists.<br>
<br>

<b>Example:</b>

``` {#codeblock_icw_vcf_gzb}
ibm.nitro.NitroConfig.viewResponsesMaximumCount=2000
```
</td>
</tr>
<tr>
<td>wchApiUrl</td>
<td>
IBM Watson Content Hub API URL. This setting is optional. When set in the config, all Leap users will use the same Watson Content Hub tenant for selecting assets. When it's not set, Leap design users can set their own Watson Content Hub API URL at the time of use.ibm.nitro.NitroConfig.wchEnabled=true is required for this setting to work.<br>
<br>

<b>Example:</b>

``` {#codeblock_vpt_zff_gzb}
ibm.nitro.NitroConfig.wchApiUrl=https://my1.digitalexperience.ibm.com/api/<guid>
```
</td>
</tr>
<tr>
<td>wchEnabled</td>
<td>
Enables integration with [IBM Watson Content Hub](https://www.digitalexperience.ibm.com/). This allows Leap applications to select assets from IBM Watson Content Hub.Where:

-   true - enables a choice in the design experience that allows a design user to select assets from IBM Watson Content Hub \(a Watson Content Hub subscription is required\)
-   false - feature remains disabled

Default value: false<br>
<br>

<b>Example:</b>

``` {#codeblock_nwj_tff_gzb}
ibm.nitro.NitroConfig.wchEnabled=false
```
</td>
</tr>
<tr>
<td>xFrameOptions</td>
<td>
Use this setting to control the X-Frame-Options response header for Leap pages.<br>
<br>

<b>Example:</b>

``` {#codeblock_ld5_nff_gzb}
ibm.nitro.NitroConfig.xFrameOptions = SAMEORIGIN
```
</td>
</tr>
</table>

<b>Parent topic:</b> [Configuring the properties file](co_configuring_the_properties_file.md)

