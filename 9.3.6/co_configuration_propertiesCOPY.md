# Configuration properties 

The following table contains a list of properties in the HCL Leap Leap_config.properties file. You can adjust the settings listed in the file, or add your own for a custom configuration.

Table 1. List of properties in the Leap_config.properties configuration file

<table class="table-wrap">
<tr>
<td width="300"> <b>Setting</b> </td><td> <b>Description</b> </td>
</tr>
<tr>
<td> adminInfo </td>
<td> Allows admin contact information to be shown within error messages.<br>
<br>
If <i>adminInfo1</i> and <i>adminInfo2</i> are both provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at <b>adminInfo1</b>, or <b>adminInfo2</b>, and provide error reference: XXX.” <br>
<br>
If only <i>adminInfo1</i> is provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator at <b>adminInfo1</b> and provide error reference: XXX.”<br>
<br> 
If neither are provided, the error message will be “We are unable to process your request. If this error persists, report the problem to your administrator and provide error reference: XXX.”
<br>
<br>
<b>Examples:</b>
```
ibm.nitro.NitroConfig.adminInfo1 = admin@yourcompany.com 
ibm.nitro.NitroConfig.adminInfo2 = 1-800-GET-HELP
```
</td>
</tr>
<tr>
<td> anonBlockedMsg=[MESSAGE] </td>
<td>

When a user attempts to access a Leap application anonymously, an error message is displayed. The default message is “Anonymous access blocked”. You can change the default message to provide additional information to the user.<br>
<br>

<b>Example:</b>
```
ibm.nitro.NitroConfig.anonBlockedMsg=Anonymous usage is not allowed
```
</td>
</tr>
<tr> 
<td> appFilesWhiteList<br>appFilesBlackList<br>appFilesMaxSize </td>
<td>

List of allowed (whitelist), and not allowed (blackList) of mimetypes, and the number of maximum file sizes for Application File uploads.<br>
<br>

<b>appFilesWhiteList</b> – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – empty (everything is allowed)
<br>
<br>
<b>appFilesBlackList</b> – A space separated list of:<br>

-   mimetypes – text/plain application/vnd.xfdl<br>
-   partial mimetypes – text/audio/ /plain<br>
-   file extensions – GIF PDF XML<br>
-   default value – exe
<br>
<br>
<b>appFilesMaxSize</b> (size in kb) – A space separated list of:<br>

-   mimetypes – text/plain application/ /vnd.xfdl<br>
-   file extensions – GIF PDF XML or default as special type<br>
-   default value – 5000<br>
<br>

<b>Examples:</b>
```
ibm.nitro.NitroConfig.appFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi 
ibm.nitro.NitroConfig.appFilesBlackList = exe 
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
By default, the timer is enabled and the collection time is set to 3 AM daily local server timer.<br>
<br>
<strong>Note:</strong> Depending on the volume of applications, statistics collection may take 10+ minutes, adjust the timer and frequency to server quiet time.<br>
<br>
<b>appStats.timerEnabled</b> - Enable Application Statistics collection.<br>
<br>
To disable Application Statistics collection, set to false.<br>
<br>
Default value: true<br>
<br>
<b>appStats.refreshHour</b> - Sets the hour of day to start Application Statistics collection.<br>
<br>
Value 0 to 23, indicating the hour of day to start the statistics collection process.<br>
<br>
Default value: 3<br>
<br>
<b>appStats.refreshDays</b> - Sets the Application Statistics collection day. Use full names of day of the week, separated by a comma, semicolon, or space.<br>
<br>
Valid values: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday<br>
<br>
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
List of allowed (whitelist), and not allowed (blackList) of mimetypes, and the number of maximum file sizes for the Attachment form item.<br>
<br>
<b>attachmentFilesWhiteList</b> – A space separated list of:<br>
<ul>
    <li>mimetypes – text/plain application/vnd.xfdl</li>
    <li>partial mimetypes – text/audio/ /plain</li>
    <li>file extensions – GIF PDF XML</li>
    <li>default value – empty (everything is allowed)</li>
</ul>
<b>attachmentFilesBlackList</b> – A space separated list of:
<ul>
    <li>mimetypes – text/plain application/vnd.xfdl</li>
    <li>partial mimetypes – text/audio/ /plain</li>
    <li>file extensions – GIF PDF XML</li>
    <li>default value – exe js html svg</li>
</ul>
<b>attachmentFilesMaxSize</b> (size in kb) – A space separated list of:
<ul>
    <li>mimetypes – text/plain application/ /vnd.xfdl</li>
    <li>file extensions – GIF PDF XML or default as special type</li>
    <li>default value – 5000</li>
<ul>
<br>

<b>Examples:</b>

``` {#codeblock_hvz_bcf_gzb}
ibm.nitro.NitroConfig.attachmentFilesWhiteList = css js html exe text/plain application/vnd.xfdl mov avi
ibm.nitro.NitroConfig.attachmentFilesBlackList = exe 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.10000 = default 
ibm.nitro.NitroConfig.attachmentFilesMaxSize.50000 = mov avi
```
</td>
</tr>
<tr>
<td> blockAnonAccess </td>
<td>
Anonymous access is not allowed by default which means that to use a Leap application or survey, users must authenticate with a valid user ID and password.<br>
This setting determines anonymous access, where:<br>
<ul>
    <li>enabled - anonymous access is blocked</li>
    <li>disabled - anonymous access is allowed</li>
    <li>redirect - redirects the user to authenticate</li>
</ul>

Default value: redirect<br>
<br>

<b>Example:</b>
```
ibm.nitro.NitroConfig.blockAnonAccess=redirect
```

</td>
</tr>
<tr>
<td> customThemes.[ID].displayName<br>customThemes.[ID].location<br>customThemes.[ID].isDefault<br>customThemes.[ID].nl.[LOCALE] </td>
<td>
The <b>customThemes config</b> settings define a list of customer-provided themes that can be used in Leap applications.<br>
<br>

For each theme, two parameters must be set:
<ul>
    <li><b>customThemes.[ID].displayName</b></li>
    <li><b>customThemes.[ID].location</b></li>
</ul>
<b>[ID]</b> - An identifier for the custom theme (e.g. "corpTheme1").<br>
<br>
The id can contain the letters 'a' through 'z' and numbers, and must start with a letter.<br>
<br>
<b>displayName</b> - The theme name to be displayed in the Leap authoring UI.<br>
<br>
<b>location</b> -The full URL of the theme's .css file.<br>
<br>
For each theme, there are 2 optional parameters:<br>
<ul>
    <li><b>customThemes.[ID].isDefault</b></li>
    <li><b>customThemes.[ID].nl.[LOCALE]</b></li>
</ul>
<b>isDefault</b> - If set to true, designates the theme as the default selection for new applications.<br>
<br>
<b>nl.[LOCALE]</b> - For globalization support of the theme's display name. <b>[LOCALE]</b> is the locale code that identifies the language (e.g.,"en", "fr", "fr_CA", "zh").<br>
<br>
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
<ul>
<li>warn - The user is warned that the browser is unsupported. A list of supported browsers is displayed in the warning message. When the user closes the warning message, the form is displayed.</li>
<li>ignore - The user is not warned that the browser is unsupported, and the form is displayed.</li>
</ul>
<br>
Default value: warn<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.NitroConfig.detectBrowser=ignore
```
</td>
</tr>
<tr>
<td style="width:5%">disableUseTab</td>
<td>
Hides the "Use" tab, and prevents fetching the list of deployed and usable applications, where:
<ul>
    <li>true - "Use" tab is hidden</li>
    <li>false - "Use" tab is displayed</li>
</ul>
Default value: false<br>
<br>

<b>Example:</b>

``` 
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
Leap contains an event handling implementation that enables printing out all or specific events in the system log or in a separate file based on properties setting, by default this feature is not enabled. Change properties, in the Leap_config.properties file, to monitor events that you are interested in, and where you want to output the event information.<br>
<br>
The following will output Events information in Application Server's system log at info or debug level:<br>
<ul>
    <li><b>EventHandler.infoLevelEvents</b></li>
    <li><b>EventHandler.debugLevelEvents</b></li>
</ul>
<b>auditLevelEvents</b> will output to a file. The default file location on Windows is C:\febEvents.log and AIX/Linux is /febEvents.log, with maximum file size 5MB, back up to 5 files.<br>
<br>
The content of the event output is in CSV format, the description of the data: Event topic, Event time stamp, User id, User email, Application uid, Application title, Form id, Record uid, Result<br>
<br>
The following is the list of event topics that Leap sends out:
<ul>
    <li>builder/app/delete – Application is deleted</li><li>builder
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
To capture failed events, use "builder/error/[EVENT_TOPIC]"<br>
<br>

<b>Example:</b>

``` 
 ibm.nitro.EventHandler.infoLevelEvents=builder/record/submit,builder/error/builder/record/submit
```
</td>
</tr>
<tr>
<td>exportDataWithEmails</td>
<td>
By default when you export data from applications, emails are also exported. You can exclude emails from the export by changing the property value to false.

Where:
<ul>
    <li>true - emails are exported with application data</li>
    <li>false - emails are not exported with application data</li>
</ul>
Default value: true<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.NitroConfig.exportDataWithEmails=true
```
</td>
</tr>
<tr>
<td>
imageDomainWhitelist.enabled=true

imageDomainWhitelist.[N].domain
</td>
<td>
The <b>imageDomainWhitelist</b> config settings define a white-list of domains from where images can be uploaded to a Rich Text Entry field.<br>
<br>
In addition to setting the following:<br>
<br>
<b>imageDomainWhitelist.enabled=true</b> for each domain an additional parameters must be set.<br>
<br>
<b>imageDomainWhitelist.[N].domain =</b> where "[N]" is an integer number identifying that service.<br>
<br>
domain - The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.<br>
<br>

<b>Examples:</b>

``` 
ibm.nitro.imageDomainWhitelist.enabled=true
ibm.nitro.imageDomainWhitelist.[1].domain=http://acme.com
ibm.nitro.imageDomainWhitelist.[2].domain=http://acme2.com
```
</td>
</tr>
<tr>
<td>InfoEntryPoint.dailyInfo</td>
<td>
Provides HTML content that is shown in the login screen. Can be used for status messages, or help.

``` 
ibm.nitro.InfoEntryPoint.dailyInfo = Welcome to <b>HCL Leap</b>
```
</td>
</tr>
<tr>
<td>LogoutServlet.postLogoutRedirectURL</td>
<td>
The value of this parameter tells Leap where to redirect user after log off. If the parameter is not configured or left blank, the user is redirected to the login page.<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.LogoutServlet.postLogoutRedirectURL=http://example_url.com/signout
```
</td>
</tr>
<tr>
<td> maximumRecordsToRetrieve</td>
<td>
Maximum number of records that are permitted for export from the View Data page at one time. If the number of records to be exported exceeds the number set by this property, the export is stopped, and an error message is shown.<br>
<br>

<b>Note:</b> The default value of 20,000 is supported for base systems. Setting the value higher could result in poor performance, depending on result set size and server hardware.<br>
<br>

<b>Example:</b>

``` 
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
<b>MemberManager.adminAlias</b> setting is mandatory. For WebSphere Application Server only, configure the VMM login.<br>
<br>
By default, Leap uses J2C alias <b>vmmAdmin</b> to authenticate with VMM. You must configure it here if you want to change the J2C alias name.<br>
<br>
You must have WebSphere Application Server administrative user credentials to run Leap<br>
<br>
If you use LDAP within WebSphere Application Server, there are a number of properties that look up user and group information. If your LDAP uses different property keys than the ones set by default, update the property keys here so that user and group look up function correctly.<br>
<br>
If you are using LDAP within WebSphere Application Server, refer to the following settings:<br>
<br>
<b>MemberManager.userProps.loginName</b><br>
<br>
Describes the LDAP property used as the login ID. Each loginName must be unique.<br>
<br>
Default setting: uid<br>
<br>
<b>MemberManager.userProps.id</b><br>
<br>
Represents a unique key for the user. This key must be identical to the loginName.<br>
<br>
Default setting: uid<br>
<br>
<b>MemberManager.groupProps.id</b><br>
<br>
Represents a unique key for the group. The value is the LDAP property that is used. For example, cn, represents Common Name.<br>
<br>
Default setting: cn<br>
<br>
<b>MemberManager.userProps.email</b><br>
<br>
The email address of the user. Leap uses this email address to send notifications and other emails to the user.<br>
<br>
Default setting: mail<br>
<br>
<b>MemberManager.userProps.displayName</b><br>
<br>
Used to display the name of the user, instead of the login id.<br>
<br>
Default setting: cn<br>
<br>

<b>Examples:</b>

``` 
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
In some circumstances, files attached to either application designs or user-submitted records can become orphaned if the primary design or record element is removed outside the normal process. File records which are older than this number of hours and are no longer associated with an existing primary record are removed.<br>
<br>
Default value: 48<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.purgeOrphanFilesHours=36
```
</td>
</tr>
<tr>
<td>runtimeCSP</td>
<td>
The <b>runtimeCSP</b> setting defines the <code>Content-Security-Policy</code> (CSP) header that will be applied to running Forms.<br>
<br>

<b>Note:</b> This setting only applies to Forms. It does not currently apply to App Pages, Summary Charts, or the View Data page.<br>
<br>
For more information on CSP, see <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP" target="_blank">https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP</a><br>
<br>
For more information on <i>Strict</i> CSP, see <a href="leap_strict_csp.html">Strict CSP</a><br>
<br>
<b>Example:</b>

``` 
ibm.nitro.NitroConfig.runtimeCSP=default-src 'self' *.example.com; img-src *
```
</td>
</tr>
<tr>
<td>runtimeResources.[N]</td>
<td>
Additional web resources to load into the Leap UI for leveraging the <a href="customwidgetapi_landing.html">Custom Widget API</a>. The values from these settings will be injected into the <code>&lt;head&gt;</code> section of Leap's HTML pages.<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.NitroConfig.runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css'>
ibm.nitro.NitroConfig.runtimeResources.2 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
ibm.nitro.NitroConfig.runtimeResources.3 = <script type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
```
</td>
</tr>
<tr>
<td>secureJS</td>
<td>
Enables or disables JavaScript restrictions in run time forms. When a form designer adds custom JavaScript to an application, this flag restricts the scope of that custom JavaScript. This flag applies to the entire Leap server for all users.<br>
<br>
<b>Note:</b> Setting this parameter to <code>false</code> might expose users to malicious JavaScript. Only set to <code>false</code> in a secured environment where Leap applications are created by trusted users.<br>
<br>
For more information, see <a href="ref_javascript_api.html">JavaScript API</a> for Leap.
<br>
Default value: true<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.ApplicationCompilerService.secureJS = false
```
</td>
</tr>
<tr>
<td>
serviceAuthorization.enabled

serviceAuthorization.[SERVICE_ID]
</td>
<td>
Access to a service description may be given to a specific user, group, or special assignment. The access control is made up of two parts:
<ul>
    <li>Who may "discover" and work with the service while designing an application.</li>
    <li>Who may "invoke" the service.</li>
</ul>
 Users or Groups provided must be defined using the attributes defined by <code>ibm.was.MemberManager.userProps.id = mail</code> and <code>ibm.was.MemberManager.groupProps.id = name</code> respectively.<br>
 <br>
 Special assignment valid values are:
 <ul>
    <li>all-authenticated: for app author "discover" privilege only</li>
    <li>anonymous: for app authors and end-user "discover" and "invoke" privileges</li>
    <li>all-authors: for end-user "invoke" privilege only</li>
</ul>

To enable service authorizations, set <code>ibm.nitro.NitroConfig.serviceAuthorization.enabled=true</code>. Multiple services may be defined. To define a service authorization, add <code>ibm.nitro.NitroConfig.serviceAuthorization.serviceIdN</code> where <b>serviceIdN</b> is the 'id' of the service description. The value must be a valid JSON string, see provided samples.<br>
<br>
Note: A backslash (\) at the end of a line can be used to present a value over multiple lines. The backslash must be the very last character on the line.<br>
<br>

<b>Examples:</b>

```
ibm.nitro.NitroConfig.serviceAuthorization.enabled = true
ibm.nitro.NitroConfig.serviceAuthorization.serviceId1 = { \
   "comment": "Auth for Service 1", \
   "discover": { "users": ["user1"], "groups": ["group1"], "special": [] }, \
   "invoke": { "users": [], "groups": [], "special": ["all-authenticated"]" } \
}
```
</td>
</tr>
<tr>
<td>serverURI</td>
<td>
Indicates the base URI used for critical functions, including editing applications, and email. Must include everything necessary to connect to the Leap context, for example, /apps.<br>
<br>
With this entry, all emailed links, and absolute links visible during Leap design time start with the following base URI regardless of what the user enters in the address bar.<br>
<br>
Example:
``` 
ibm.nitro.NitroConfig.serverURI = https://leap.example.com/apps
```
</td>
</tr>
<tr>
<td>
servicesWhitelist.enabled

servicesWhitelist.[N].actions

servicesWhitelist.[N].domain
</td>
<td>
The <b>servicesWhitelist</b> config settings define a white list of domains and HTTP actions that app authors are allowed to call directly from their applications using URL based services.<br>
<br>
In addition to setting <code>servicesWhitelist.enabled=true</code>, for each service two additional parameters must be set:
<ul>
<li><b>servicesWhitelist.[N].domain =</b></li>
<li><b>servicesWhitelist.[N].actions =</b></li>
</ul>
The domain property implicitly allows sub-domains. For example, a domain property of example.com allows URLs such as https://www.example.com/anything, http://api.example.com/anything, or https://example.com/anything.<br>
<br>
The https or http protocol included in the domain property is respected. For example, a domain property of https://api.example.com only allows calls to secure SSL https://api.example.com/anything and not to non-secure http://api.example.com/anything.<br>
<br>
The actions property is a comma-separated list of the HTTP actions allowed for a particular domain. Valid values are GET, PUT, POST, DELETE, HEAD, and PATCH. If the actions value is missing, no actions are allowed.<br>
<br>
Where <b>[N]</b> is an integer number identifying that service.<br>
<br>
Default value: true<br>
<br>

<b>Examples:</b>

``` 
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
After deploying Leap for the first time or upgrading to a newer version, there is a setup screen that is presented upon accessing the manage page. This setup screen shows the status of detecting and updating the database tables, checks that security is properly enabled, and a mail session is configured. This page requires the admin to click a button to fully progress through the setup.<br>
<br>
To disable this setup page and required admin interaction add the property: 
``` 
ibm.nitro.SetupAll.setupStatus = start
```
</td>
</tr>
<tr>
<td>viewResponsesMaximumCount</td>
<td>
For DB2® or Oracle. The maximum number of records that are <i>counted</i> when returning record sets in pages. If the total number of records exceeds viewResponsesMaximumCount, then paging indicators will no longer accurately lists the total number of pages. Setting this value higher can have performance consequences for the server if there are many users viewing forms with large response lists.<br>
<br>
Default value: 1000<br>
<br>

<b>Example:</b>

```
ibm.nitro.NitroConfig.viewResponsesMaximumCount=2000
```
</td>
</tr>
<tr>
<td>xFrameOptions</td>
<td>
Use this setting to control the <code>X-Frame-Options</code> response header for Leap pages, which determines if Leap can be embedded into other web pages.<br>
<br>

<b>Example:</b>

``` 
ibm.nitro.NitroConfig.xFrameOptions = SAMEORIGIN
```
</td>
</tr>
</table>

<b>Parent topic:</b> [Configuring the properties file](co_configuring_the_properties_file.md)

