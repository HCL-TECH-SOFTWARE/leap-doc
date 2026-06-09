# Troubleshooting {{fullProductName}} 

The following page contains limitations, best practices, and known issues to help you troubleshoot your {{shortProductName}} product or applications.

## Known limitations of {{shortProductName}}

{% if isDominoLeap %}
### Error message: WARNING CLFAD0251W: Requesting user authentication

When you log in to {{shortProductName}}, you may see the following message in the server console:

```
WARNING CLFAD0251W: Requesting user authentication.
```

This message is logged by core Domino code. It is not logged by {{shortProductName}} itself.

Add the following line to /{domino-data}/domino/workspace/.config/rcpinstall.properties:

```
com.ibm.domino.xsp.bridge.http.manager.level=SEVERE
```

After you save the change, restart the HTTP process.

### Domino installers remove {{shortProductName}}.

Domino installers remove {{shortProductName}}. For example, if you upgrade to Domino 11.0.1 from 11.0.0, the Domino installer removes {{shortProductName}} bundles from /{domino-program}/osgi/volt.

Reinstall {{shortProductName}} after you upgrade Domino. Be sure to stop the Domino server before you reinstall {{shortProductName}}. You may leave the /{domino-data}/volt directory in place for the upgrade.
{% endif %}

### Apps are forward compatible only

Apps are forward compatible only; apps created on newer {{shortProductName}} releases cannot be deployed in previous {{shortProductName}} releases.

### Limit on the number of embedded sections

When designing a form in {{shortProductName}}, you can embed sections within sections to achieve the wanted layout. Do not embed more than 5 sections within one another.

When using more than five embedded sections, it becomes difficult to select the action icons for a specific section. Exceeding 5 sections also results in forms not rendering properly.

### Printing {{shortProductName}} content

{{shortProductName}} provides a print button. If there is no print button in the contents of your form, the web browser print function does not work well. To print out the contents shown in your browser, uses a screen capture. For more information, see [Taking a screen capture in Windows™](http://windows.microsoft.com/en-US/windows-vista/Take-a-screen-capture-print-screen).

### Adding Groups to {{shortProductName}} applications

{{shortProductName}} cannot resolve users if they are members of nested groups.

For example, your company LDAP contains a super group called “Managers”. This super group consists of several smaller groups, such as “Supervisors”, and “Shift Leaders”. In the **Access** tab of {{shortProductName}}, you must add the “Supervisors”, and “Shift Leaders” as groups individually, rather than using the “Managers” super group.

## {{shortProductName}} Best Practices

### Canonical URLs versus short URL in the serverURI property

When accessing {{shortProductName}}, the {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serverURI entry setting differs from the browser address base URI. If you are using a short URL format to design your application, you must set {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}serverURI entry with the canonical URL. For example, if your short URL is http://localhost:9080/{{context}}, the canonical URL for the user is http://hostname:9080/{{context}}. Using two different URLs means that users must sign on twice, as the short URL is replaced by the canonical URL. It is a best practice to use the canonical URL whenever possible.

### **Web Link** and **Website** form items

When using the **Web Link** or **Website** form items in your application, ensure that you enter the correct URL to get the runtime result. If the link goes to an external site, you must enter the URL with a URL protocol. For example, enter the URL as http://www.hcl.com, rather than www.hcl.com.

- If you enter the URL with no protocol, then the URL is considered relative the current location. The prefix for the relative URL is attached, which might result in errors.
- If you enter the URL with a single slash '/', it resolves to a URL relative to the root of the host.
- When using the **Website** item in a {{shortProductName}} the URLs entered must begin with: http://, https://, ftp://, {% if isDominoLeap %} notes://,{% endif %} or ftps://

{% if isLeap %}
### Leap users and groups

When using WebSphere® Application Server to directly maintain users and groups, it is important to maintain integrity between the WebSphere Application Server users and Leap. If you change a user definition in WebSphere Application Server, and that user is used in Leap, the relationship might be corrupted. The user would no longer be able to access Leap.
{% endif %}

### Uploading files in {{shortProductName}}

If an application requires supplemental files, it is a best practice to use reference URLs, rather than uploading the files directly into the application. The option to include reference URLs is available in the Upload dialog from the **Settings** tab.

### {{shortProductName}} Preview mode

To use the {{shortProductName}} Preview feature, you must ensure that your browser is configured to allow all pop-up windows. If your browser does not allow pop-up windows, users cannot see the preview window.

### Browser cookies must be enabled.

To successfully log in {{shortProductName}}, you must have browser cookies enabled. 

{% if isLeap %}
If you have deployed Leap with WebSphere Application Server Community Edition as your application server, you must ensure that you have only one Leap window or tab running in your browser at any time. Attempting to log in to multiple Leap windows or tabs results in login errors.
{% endif %}

## Troubleshooting {{shortProductName}} errors

### Building {{shortProductName}} applications in Safari with bidirectional languages

Designing {{shortProductName}} applications with the Safari locale set to a bidirectional language results in extraneous horizontal scroll bars shown in each form cell. These scroll bars do not affect the rendering of the completed form at run time.

{% if isLeap %}
### Allowing non-ASCII administrative login characters

If the Leap administrative user name or password contains non-ASCII characters, you must complete an additional configuration task.

In WebSphere Application Server:

1.  Log in to WebSphere Application Server administrative console, and select the server.

2.  On the settings page for the selected application server, go to **Server Infrastructure** \> **Java and Process Management**.

3.  Go to **Process Definition** \> **Java Virtual Machine**, and specify -Dclient.encoding.override=UTF-8 for Generic JVM Arguments.

4.  Click **OK**, then **Save**

5.  Restart the application server
{% endif %}

## General {{shortProductName}} information

### Using the **Upgrade** link on the **Manage** tab.

You can upgrade an application with a new application definition using the {{shortProductName}} **Upgrade** feature. Upgrading replaces all access rules, business rules, formulas, interface options, Stages definitions, JavaScript™, images, and service mappings with those in the new version. It then updates the data base definition to the model described by the new application, and merges existing data into that model.|

If data elements were removed in the new version, or their unique identifiers changed, the data associated with those elements is not migrated to the new application. Data elements that did not exist in the previous version, but were added in the new version, are added to existing data records with a NULL value.

**Parent topic:** [Troubleshooting](tr_troubleshooting_toc.md)

