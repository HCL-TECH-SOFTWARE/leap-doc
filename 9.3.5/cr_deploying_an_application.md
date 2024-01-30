# Deploying an application {#deployinganapplication .task}

Deploying an HCL Leap application makes it available for users. When you click **Deploy**, the application is loaded onto a server. You can deploy an application immediately, or set a timer to deploy the application for a specific period of time.

You can update Leap applications with existing data that are currently deployed. However, these types of changes might impact existing data, and forms in-progress, depending on the type of changes made to the application. The impact occurs when the application is deployed, not during the design phase. The following changes might result in data loss, or prevent in-progress forms from being completed:

-   If you delete fields that capture data from a form, any existing data for those fields is removed.
-   If you change the ID of a field that contains data, any existing data is removed.
-   If you change Access settings, users might no longer have access to existing data or forms in progress.
-   If you change Stage IDs, in-progress applications at or before the stage are not completed.

1.  Before deploying an application, click **Save** to ensure the latest version of the application is saved.

    **Note:** If you make changes to an application while it is deployed, a warning icon is displayed on the **Manage** tab next to **Deploy**. This is to remind you to redeploy the application after making changes.

2.  Go to the **Manage** tab, and click **Deploy** for the application.

    The Deployment Settings window opens.

3.  Set the deployment options for your application from the **Basic** and **Advanced** tabs.

    Leap can send out email notifications when an application is deployed or stopped. These notifications are triggered from the Email Notifications section on the Deployment Setting window. The notifications are not triggered if the application is stopped on a preset Stop Date. The Stop notifications are only sent if the deployment is stopped manually using the Deployment Settings dialog.

4.  Click **Start** to deploy the application.


After an application is deployed, the **Launch** tool is activated.

**Parent topic:**[Deploying applications and viewing data responses](cr_deploy_and_launch_toc.md)

