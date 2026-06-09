# Importing and exporting applications { #importingandexportinganapplication .task }

This topic provides an overview of importing and exporting applications in {{fullProductName}}.  You can import or export applications from the **Manage** page to migrate an application between environments.

## Importing an application

The following steps are a general overview of how to **import** an application.

1.  On the **Manage** page, click the **Import an app** button.

2.  The **Create a new app** window opens. By default, ***Remove previously defined users and groups from this application?*** is selected.

    !!! note
        To import the application with existing users and roles, uncheck ***Remove previously defined users and groups from this application?***.

3.  Click **Create**. Ensure that **Assigned Users** is not be empty when you open the application.


## Exporting an application

The following steps provide a general overview of how to **export** an application.

1.  On the **Manage** page, under the [Application Name], click **More** and then **Export**.

2.  The **Export Application** window opens. Export the application definition, including security settings and any uploaded files or images. 

    !!! note
        To export the application with data, select **Include submission data?** in **Existing data options**.  

3.  Click **OK**. The `.leap` file is downloaded to the local machine and can be imported into another {{fullProductName}} environment.  

    
**Parent topic:** [Application Management](cr_application_operations_toc.md)

