# Post-installation tasks

After you install Domino Leap, complete the following tasks:

!!! note
    The file paths and file names listed in the following tasks are case-sensitive.

## Restart Domino and verify Domino Leap installation

1. Restart the Domino server, and then run the following console command:

    ```
    tell http osgi ss dleap
    ```

2. Ensure that the output includes the following content:

    ```
    ACTIVE    dleap_[version]
    ```

    !!! note
        If output if does not include this line, do not proceed. Recheck all preceding configuration steps.

When Domino Leap starts for the first time, it automatically creates three databases in the volt folder of your Domino data directory:

- volt/VoltBuilder.nsf
- volt/VoltAppHistory.nsf
- volt/VoltConfig.nsf

The following sections include important steps for completing the configuration of these three databases.


## Modify VoltBuilder.nsf

The HCL Domino Volt Builder database is used to store Domino Leap application designs and for other processing. The default ACL entry for VoltBuilder.nsf allows **all authenticated users** to create Domino Leap applications. We recommend that you modify the ACL to restrict access to a group of trusted Domino Leap authors.

1. From the Notes Client, open the Volt Builder database on the server (volt/VoltBuilder.nsf).

2. Modify the database ACL.

### Suggested ACLs for VoltBuilder.nsf

- Domino Leap Authors should have **Editor** access with delete privileges. Use the group you name created in Configuring the server.
- Default access should be **Reader**.
- Anonymous should have **No Access** and **Read public documents** should be checked.
- **Optional**: Assign [VoltAppsManager] role to at least one administrator. Users in this role will be able to view and edit all Domino Leap applications.
- **Optional**: Assign [LeapAdmin] role to at least one administrator. Users in this role will be able to view and edit all Domino Leap applications. For more information, see [Admin Application Dashboard](admin_application_dashboard.md).

For more information on verifying the VoltBuilder.nsf, see [Controlling who creates HCL Domino Leap applications](dleap_control_creating_applications.md).


## Modify VoltAppHistory.nsf

The application history database is used to record the changes to each Domino Leap application. The ACL entries for VoltAppHistory.nsf should match the entries for VoltBuilder.nsf.

1. From the Notes Client, open the application history database on the server (volt/VoltAppHistory.nsf).

2. Modify the database ACL.

### Suggested ACLs for VoltAppHistory.nsf

- Domino Leap Authors should have Editor access with delete privileges. Use the group you name created in Configuring the server.
- Default access should be Reader.
- Anonymous should have **No Access**.


## Modify VoltConfig.nsf

The HCL Domino Leap Configuration database is used to manage configuration information specific for your environment. Domino Leap is capable of operating absent of any enabled settings except the Server URI.

1. From the Notes Client, open the Domino Leap Config database on the server (volt/VoltConfig.nsf)

2. From the All Settings view, select and edit the setting **serverURI**.

3. Set the Setting Value to match the appropriate URI for your HCL Domino Leap server. An example value is https://volt.example.com/volt-apps. Be sure to specify http if you don’t have SSL configured (not recommended).

4. Ensure the setting is Enabled.

5. Save and close the Setting document.

6. Verify the database ACL.

### Suggested ACLs for VoltConfig.nsf

- Default access should be **No Access**.
- Anonymous should be **No Access**.

!!! note
    This file name is CASE SENSITIVE on Linux.


## Log in to Domino Leap

Once you have finished modifying the Domino Leap system databases, issue a ```restart task http``` command at the server console, and then launch a browser and visit the Domino Leap Manager page. The absolute URL depends on your server host name and whether you have enabled https on your server. The relative URL is **/volt-apps/secure/org/ide/manager.html**.

Full URL example: https://volt.example.com/volt-apps/secure/org/ide/manager.html.

Login as a user in the Domino Leap Authors group, or as a user with equivalent privileges.

## Next steps...

After completing the previous tasks, an author should be able to create a new Domino Leap application and share it with other users. This may be sufficient for a test environment. However, a production deployment of Domino Leap may require additional configuration steps. For more configuration topics to consider see [Core Domino server configuration](dleap_core_domino_config.md).

**Parent topic:** [Installing Domino Leap](dleap_install_overview.md)