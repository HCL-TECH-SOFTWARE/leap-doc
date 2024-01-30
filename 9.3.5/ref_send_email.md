# Send Email service 

This topic provides reference information on the Send Email service in HCL Leap.

## Purpose {#section_jkm_qck_d1c .section}

The Send Email service provides a mechanism to send an email from a Leap application. The service enables an application author to bind fields from their form to the parameters of the service and it can be executed at any time, which is what distinguishes it from the submit activity email functionality \(which can only be sent as part of a submit event\).

This feature is disabled by default and must be enabled by the administrator. To enable this service, add \(or modify\) the following property in the Leap\_config.properties:

``` {#codeblock_und_tck_d1c}
ibm.nitro.NitroConfig.enableEmailService=true
```

Leap does not need to be restarted, but it may take a few minutes for the service to appear in the authoring environment.

## Service parameters {#section_qgm_tck_d1c .section}

|**Parameter**|**Definition**|
|-------|--------|
|To| One or more addresses to be used as the primary email target.|
|CC|One or more addresses to which the email will be sent as cc.|
|BCC|One or more addresses to which the email will be sent as bcc.|
|Reply To|The email address to be shown as the reply to address.|
|Subject|The text to be used for the email subject.|
|Text Content|Plain text content to be used for the email body.|
|HTML Content|HTML content to be used for the email body.|
|  | **Note:** Both the plain text and html content are sent as part of the email if specified. It is up to the rendering email client to decide how and when to use the content provided.|


## Advanced service parameters {#section_hwm_zck_d1c .section}

To access the advanced service parameters, select **Advanced** from the drop-down labelled **View** on the **Inputs** tab.

|**Parameter**|**Definition**|
|-------|--------|
|To List|This is a list parameter that can be connected to a list form item, like a table, to enable multiple addresses to be assigned to the email ‘To’ field.|
|CC List|This is a list parameter that can be connected to a list form item, like a table, to enable multiple addresses to be assigned to the email ‘CC’ field.|
|BCC List|This is a list parameter that can be connected to a list form item, like a table, to enable multiple addresses to be assigned to the email ‘BCC’ field.|

## How to use {#section_zvw_cdk_d1c .section}

To use this service, complete the following steps while editing an application:

1.  Select **Settings**.
2.  Create a service configuration.
3.  Select the **General** service catalog.
4.  From the list of services, select **Send Email**.
5.  Map form items to the email service parameters
6.  On the **Details** tab, define a meaningful service id..
7.  Click **OK**.

The service is then listed on the services page for that form. This service can be connected to a button click event or triggered from any item’s javaScript event. You can also setup an ‘onCallFinished’ handler to run custom javaScript code after the service completes.

## Possible response values {#section_gx3_ndk_d1c .section}

The service does not return any parameters. The service could throw the following errors:

|**Error message**|****Definition****|
|-------|--------|
|CLFNI1803E: Email must define at least one address \('to', 'cc' or 'bcc'\).|If the to, cc and bcc are empty|
|CLFNI1804E: Email body may not be empty.|If the text content and the html content are empty|
|CLFNI1805E: Failed to send email.|If an error is received from the mail server configured with Leap.|

**Parent topic:**[Services](ref_services_toc.md)

