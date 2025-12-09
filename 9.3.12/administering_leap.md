# Administering {{shortProductName}} { #administering_leap .concept }

The following topics contain information on administering {{shortProductName}}.

{% if isLeap %}
-   **[Backing up and restoring the DB2 database](ad_managing_db2_database.md)**  
Data for {{fullProductName}} applications is stored within a database. Ensure that you have a backup and restore strategy in place to protect your data.
-   **[Admin Configuration Page](admin_config_ui.md)**
The Admin configuration page can be used to modify some configuration properties and is available to members of the Admin group.
{% endif %}
{% if isDominoLeap %}
-   **[Controlling who creates HCL Domino Leap applications](dleap_control_creating_applications.md)**
To configure who can create and delete applications, you need to modify the Access Control List (ACL) for VoltBuilder.nsf.
-   **[Domino Leap configuration settings](dleap_control_creating_applications.md)**
Domino Leap configuration settings are in **VoltConfig.nsf** in the volt folder of your Domino data directory (volt/VoltConfig.nsf). Use the Notes client or the Domino Administrator client to modify a configuration setting.
-   **[Core Domino server configuration](dleap_control_creating_applications.md)**
HCL Domino Leap is an add-on to the core HCL Domino server. Domino Leap runs in the context of the Domino web server (HTTP process). Therefore, Domino Leap is affected by the underlying Domino server configuration. This topic covers some of the core configuration settings that may affect Domino Leap.
-   **[Upgrading from prior releases](dleap_upgrading_prior_releases.md)**
All Domino Leap NSF files set the database property **Don't Maintain Unread Marks** as default, which should improve performance. NSF files created in prior versions of Domino Leap are not changed.
-   **[Domino Leap Cleanup process](dleap_cleanup_agent.md)**
Domino Leap Cleanup primarily purges orphaned Builder attachments, orphaned application attachments, and old Preview databases. Prior to release 1.0.3, this process was done by the Domino Leap Cleanup Agent.
-   **[Enabling basic authentication for HCL Domino Leap API requests](dleap_control_creating_applications.md)**
If form-based authentication is enabled, you will see an HTML form for authentication instead of a pop-up window. This topic provides instructions on how to disable HTML form-based authentication for the HCL Domino Leap server API URL paths and enable basic authentication.
-   **[Securing your Domino Leap deployment](dleap_control_creating_applications.md)**
{% endif %}
-   **[Strict CSP](leap_strict_csp.md)**  
{{fullProductName}} has a limited capability to restrict the rendering of Leap Forms using a “Strict CSP” policy.
-   **[Admin Application Dashboard](admin_application_dashboard.md)**  
The Admin Application Dashboard is a page that is available to members of the Admin or SuperAdmin groups.
-   **[Integrating with HCL Volt MX Foundry](foundry_integration.md)**
Use integration services defined in HCL Volt MX Foundry and track leap users.

