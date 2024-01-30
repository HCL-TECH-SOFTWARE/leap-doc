# Importing data in View Data {#concept_gxl_bf2_gy .concept}

Application Owners can use an Import Data operation on the **View Data** page to import spreadsheet data into their application. This can provide a quick start method for adding many records/rows of data into an application from an existing spreadsheet.

The import operation is available for application Owners to use as an alternative to keying each row of data into the Launch experience of their Leap application and as an alternative to using the Data Access Rest API to programmatically add the data.

Each row of data in the spreadsheet is imported into the Start stage of your Leap application as a new submitted record. Supported spreadsheet formats are Microsoft Excel 97 workbook and Microsoft Excel workbook \(.xls and .xlsx\).

**Note:** Microsoft Excel 5.0/95 workbooks are not supported.

-   When using other spreadsheet tools, save the spreadsheet file into one to the supported formats before attempting to import your data.
-   Only spreadsheet data on the active sheet can be imported.

To indicate where in your application each column of spreadsheet data should be imported, the first row of your spreadsheet must be modified to provide data mapping instructions.

-   Each column header must include the **ID** of the item within your application where the data is mapped.
-   An item's ID can be found on the Advanced tab of the Properties Dialog when editing the application.

The **Import Data** button on the **View Data** page is available only to an application's Owners/Administrators and only active when the following is true:

-   Imports respect the access settings that are configured within the application, so the application owner must be included in the list of people in the **Initiator** role.
-   The application must not be configured to **Limit to single submission per Authenticated User**.
-   The application must be deployed and not stopped.

Validation and enforcement of your applications data types, required elements, and rules are performed on import.

-   Custom JavaScript added to the applications UI is not run during data import.
-   Some data elements, including dates and times, need to be in a specific format to import successfully. To identify the correct input format, it can be helpful to add a record of data using the application Launch UI, and then exporting the row from **View Data** and review the output format.

**Table** data and **Attachments** can not be imported.

**Surveys** and **Select Many** items can contain values that are lists of multiple selected choices.

-   Use commas to separate the selected choices.
-   In cases where one of the selected choices contains a comma, the following sequence can be used as an alternative separator: \_\_\#\_\_

The data import operation stops when it encounters blank columns or rows in the spreadsheet.

The data import operation supports a maximum of 1000 rows of data.

To import data that has been exported from a HCL Leap application:

-   You must replace the column header label with the item IDs required for mapping.
-   The metadata can not be imported and must be removed from the spreadsheet or mapped to a form item.

Stage transition emails configured in your application will be sent, so depending on the nature of the emails and the number of records being imported, application owners may want to disable the stage action email associated with the **Start** stage prior to running the import operation.

Import operations can not be undone and bulk deletion of records is not available. Using some of the following recommendations can help ensure the desired outcome when using the bulk data import.

-   Select one or two rows or spreadsheet data to import as an initial test to help ensure the mapping is set up as expected and the data types are compatible. Review the imported data in **View Data** after the import to see that it imported as expected.
-   To quickly remove all data from an application, on the **Manage** page, choose to **Export** your application without including submitted data and then choose to **Upgrade** your application and select the option to **Replace submitted data**.
-   Prior to performing a large bulk data import into an application that already has submitted data, creating a backup of the application and all existing records is recommended. On the **Manage** page, select the **Export** operation for your application and be sure to select the option to **Include submitted data**. This will provide an archive of the application and data in the state it was in just prior to the import.

**Parent topic:**[Deploying applications and viewing data responses](cr_deploy_and_launch_toc.md)

