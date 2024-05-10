# Troubleshooting HCL Leap 

The following table contains information to help you troubleshoot your Leap product or applications. The table contains limitations, best practices, and known issues.

Table 1. Known limitations of Leap

|Limitations|Resolution|
|-----------|----------|
|HCL Connections Community Surveys are not available in Leap 8.6.0 and later versions. |To add Surveys to your Connections application, you must use Leap 8.5 with Connections 4.5, or Leap 8.5.1 with Connections 5.0.|
|Form item size limitations.| When building a Leap application, you must not exceed the following size limits|
| | You cannot have more than 1000 data items in your form|
| | You cannot have more than 200 data items in your form|
| | DB2® has a page size limit for tables of 32kb.|
| | Each data item in a Leap application has a size limit. For example:| 
| | - Single Line – 200 bytes and Multiple line|
| | - Leap uses a CLOB data type to store the value of each multiple line entry data item. The limit to the number of characters stored in a CLOB is dependent on language and character set. The English limit is approximately 1 million characters.If the content of any given multiple line field exceeds the database allowance, you see a “500 Internal Server Error” message, and form submission fails. The full message is stored in the system log files.|
| | -   Currency/Number – 8 bytes|
| | -   Attachment – 108 bytes|
| | -   Select One and Survey – size is based on the number of choices and questions|
| | If you receive the error *The row length of the table exceeded a limit of “32677” bytes. \(Table space “”.\). SQLCODE=-670*, your form exceeds the maximum size. You must remove items from the form, or break the application into multiple forms.
| | It is important to note that items create database columns, and contribute to the limit even when they are hidden on the form.|
| | **Note:** This is no longer applicable as of DB2 10.5 and newer, due to extended row size.|
|Limit on the number of embedded sections. |When designing a form in Leap, you can embed sections within sections to achieve the wanted layout. Do not embed more than 5 sections within one another.|
| | When using more than five embedded sections, it becomes difficult to select the action icons for a specific section. Exceeding 5 sections also results in forms not rendering properly.|
|Printing Leap content | Leap provides a print button. If there is no print button in the contents of your form, the web browser print function does not work well. To print out the contents shown in your browser, uses a screen capture. For more information, see [Taking a screen capture in Windows™](http://windows.microsoft.com/en-US/windows-vista/Take-a-screen-capture-print-screen).|
|Adding Groups to Leap applications. |Leap cannot resolve users if they are members of nested groups.|
| | For example, your company LDAP contains a super group called “Managers”. This super group consists of several smaller groups, such as “Supervisors”, and “Shift Leaders”. In the **Access** tab of Leap, you must add the “Supervisors”, and “Shift Leaders” as groups individually, rather than using the “Managers” super group.|

Table 2. Leap Best Practices

|Issue|Resolution|
|-----|----------|
|Canonical URLs versus short URL in the ibm.nitro.NitroConfig.serverURI property of the Leap\_config.properties file |When accessing Leap, the ibm.nitro.NitroConfig.serverURI entry setting is different from the browser address base URI. If you are using a short URL format to design your application, you must set ibm.nitro.NitroConfig.serverURI entry with the canonical URL. For example, if your short URL is http://localhost:9080/apps, the canonical URL for the user is http://hostname:9080/apps. Using two different URLs means users must sign on twice, as the short URL is replaced by the canonical URL. It is a best practice to use the canonical URL whenever possible.|
|**Web Link** and **Website** form items.|When using the **Web Link** or **Website** form items in your application, ensure that you enter the correct URL to get the runtime result. If the link goes to an external site, you must enter the URL with a URL protocol. For example, enter the URL as http://www.ibm.com, rather than www.ibm.com.|
| | -   If you enter the URL with no protocol, then the URL is considered relative the current location. The prefix for the relative URL is attached, which might result in errors.|
| | -   If you enter the URL with a single slash '/', it resolves to a URL relative to the root of the host.|
| | When using the **Website** item in a Leap the URLs entered must begin with: http://, https://, ftp://, or ftps://|
|Leap users and groups |When using WebSphere® Application Server to directly maintain users and groups, it is important to maintain integrity between the WebSphere Application Server users and Leap. If you change a user definition in WebSphere Application Server, and that user is used in Leap, the relationship might be corrupted. The user would no longer be able to access Leap.|
|Uploading files in Leap|If an application requires supplemental files, it is a best practice to use reference URLs, rather than uploading the files directly into the application. The option to include reference URLs is available in the Upload dialog from the **Settings** tab.|
|Leap Preview mode|To use the Leap Preview feature, you must ensure that your browser is configured to allow all pop-up windows. If your browser does not allow pop-up windows, users cannot see the preview window.|
|Browser cookies must be enabled. | To successfully log in Leap, you must have browser cookie enabled. If you have deployed Leap with WebSphere Application Server Community Edition as your application server, you must ensure that you have only one Leap window or tab running in your browser at any time. Attempting to log in to multiple Leap windows or tabs results in login errors.|

Table 3. Troubleshooting Leap errors

|Problem|Resolution|
|-------|----------|
|Building Leap applications in Safari with bidirectional languages |Designing Leap applications with the Safari locale set to a bidirectional language results in extraneous horizontal scroll bars shown in each form cell. These scroll bars do not affect the rendering of the completed form at run time.|
|Allowing non-ASCII administrative login characters |If the Leap administrative user name or password contains non-ASCII characters, you must complete an additional configuration task.|
| | In WebSphere Application Server:|
| | 1.  Log in to WebSphere Application Server administrative console, and select the server.|
| | 2.  On the settings page for the selected application server, go to **Server Infrastructure** \> **Java and Process Management**.|
| | 3.  Go to **Process Definition** \> **Java Virtual Machine**, and specify -Dclient.encoding.override=UTF-8 for Generic JVM Arguments.|
| | 4.  Click **OK**, then **Save**|
| | 5.  Restart the application server|

Table 4. General Leap information

|Topic|Additional Information|
|-----|----------------------|
|Using the **Upgrade** link on the **Manage** tab.| You can upgrade an application with a new application definition using theLeap **Upgrade** feature. Upgrading replaces all access rules, business rules, formulas, interface options, Stages definitions, JavaScript™, images, and service mappings with those in the new version. It then updates the data base definition to the model described by the new application, and merges existing data into that model.|
| | If data elements were removed in the new version, or their unique identifiers changed, the data associated with those elements is not migrated to the new application. Data elements that did not exist in the previous version, but were added in the new version, are added as columns to existing data records with a NULL value.|

**Parent topic: **[Troubleshooting](tr_troubleshooting_toc.md)

