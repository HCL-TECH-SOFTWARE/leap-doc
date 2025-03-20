# Admin Application Dashboard { #admin_application_dashboard .concept }

The Admin Application Dashboard is a page that is available to members of the Admin or SuperAdmin groups.

An **Admin** tab will appear in the top banner for users with permission. The page provides information about all the applications on the {{shortProductName}} server. To manage the load on the server, the details are gathered using a timer task that runs at a regular configurable interval \(see Application Statistics collection timer in [Configuration properties](co_configuration_properties.md)\).

The dashboard shows the following:

-   The total number of applications.
-   A breakdown of the applications by status \(i.e. running, undeployed\).
-   The total number of application records across all applications.
-   A filterable table of all the applications. Clicking on a row in the table reveals additional details about the selected application.

The data may be updated by clicking **Refresh**. The data may be exported to a spreadsheet by clicking **Export to spreadsheet**.

For more information, see [Application statistics REST API](app_stats_restapi.md).

**Parent topic: **[Administering {{shortProductName}}](administering_leap.md)

