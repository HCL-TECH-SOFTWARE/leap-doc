# Enabling basic authentication for HCL Domino Leap API requests

If form-based authentication is enabled, you will see an HTML form for authentication instead of a pop-up window. This topic provides instructions on how to disable HTML form-based authentication for the HCL Domino Leap server API URL paths and enable basic authentication.

## About this task

You must use Internet Site documents to disable form-based authentication and enable basic authentication.
To manually create the session override rule, complete the following steps:

### Procedure

1. On the server document **Basics** tab, enable **Load internet configurations from Server\Internet Sites documents** and save the server document.

    !!! note
        If you have an existing Internet Site Configuration, skip to step 3.

2. From **Configuration**, **Web**, **Internet Sites**, select **Add Internet Site**, **Web** and fill in the following fields:

- **Descriptive name for this site**: Enter any name you wish.
- **Organization**: The Domino organization.
- **Host names or addresses mapped to this site**: host name and/or IP address of your HCL Domino Leap server.
- **Domino servers that host this site**: The Domino server name of your HCL Domino Leap server.
- On the **Configuration** tab, change any desired configuration parameters.
- On the **Domino Web Engine** tab, enable **Session Authentication** with the same parameters as used in the Server Document.
- On the **Security** tab, make any additional security configuration changes including SSL settings.

Save and close the Internet Site document.

3. Open the Internet Site document created previously and select **Web Site** > **Create Rule**. Fill in the following fields:

- **Description**: Enter any description you wish.
- **Type of rule**: Override Session Authentication.
- **Incoming URL pattern**: ```/volt-api/*```.

4. Restart the Domino server.

5. Retry the previous HCL Domino Leap API URLs. All URLs should now generate a 401 pop-up challenge.

**Parent topic:** [Administering](administering_leap.md)