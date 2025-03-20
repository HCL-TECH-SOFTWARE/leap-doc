# Upgrading Leap

The following instructions describe how to upgrade Leap. Before you begin you must backup your DB2®, Oracle, or PostgreSQL database.

## Back up the database

Refer to the documentation of the configured database on how to perform a full backup. You will need to have a backup of all the tables in the FREEDOM, APP_DATA, and IF_CMIS schemas.

## Upgrading Leap on Kubernetes

The following instructions describe how to upgrade Leap running on Kubernetes by using Helm.

1. Update the yaml file to point to the new Leap package on Harbor. For details refer to [Load image from HCL Harbor container registry](helm_load_images.md#load-image-from-hcl-harbor).

2. Update the pod by running the [Helm upgrade command](helm_update_install.md#helm-upgrade-configuration-command).

3. Restart the pod.


## Upgrading Leap on WebSphere® Application Server { #upgradingformsexperiencebuilder .task }

The following instructions describe how to upgrade Leap by using the WebSphere® Application Server Administrative console.

-   Download the upgrade package from HCL Software Portal.
-   Back up your existing installation prior to installing the update.

### Back up the existing Leap EAR file

To back up your current Leap installation, export the Leap EAR file by following the steps:

1.  Open the WebSphere Application Server Administrative console.

2.  Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**.

3.  Select Leap.

4.  Click **Export**.

5.  Click Leap.ear to download the installation file as a backup.


### Install the new Leap EAR file

After the backup is complete, use the following instructions to install the upgrade file.

1.  Stop the Leap server.

    1.  Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**

    2.  Select Leap, and click **Stop**.

2.  Check the version of your currently installed Leap.

    1.  Go to **Modules** \> **Display module build Ids**.

    2.  Check the version for the HCL Leap WAR. An example module version is  “Leap 9.3.8.12 GA”.

3.  Update the Leap installation.

    1.  Return to **Applications** \> **Application Types** \> **WebSphere enterprise applications** \> **Leap**, and click **Update**.

    2.  In the **Application update options**, select **Replace the entire application**.

    3.  In **Specify the path to the replacement ear file**, select **Local file system**, and provide the location of the EAR file you downloaded from HCL License Portal.

    4.  Click **Next**.

    5.  In **Preparing for the application update**, click **Next**.

        Do not change the default settings on the page.

    6.  On the **Install New Application** page, go to **Step 3: Map resource references to resources**.

        -   In the **javax.mail.Session** table, set the **Target Resource JDMI Name**. Click **Browse** and select <Leap Mail Session\>.
        -   In the **javax.sql.DataSource** table, set the **Target Resource JDMI Name**. Click **Browse** and select <Leap Data Source\>.
    7.  Click **Next**.

    8.  Go to **Step 4: Map virtual hosts for Web modules** to validate that both **Virtual host** names are identical and correct, then click **Next**.

    9.  Click **Finish** to save the update.


### Clustered deployment

If Leap is running on nodes that are managed by Deployment Manager. Follow the steps below to synchronize all nodes where Leap is installed:

1.  Open the WebSphere Application Server Administrative console.

2.  Go to **System Administration** \> **Nodes**.

3. Select all nodes where Leap is installed.

4. Click **Synchronize**.

5. When the upgrade is complete, restart the Leap server.

6. Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**

7. Select Leap.

8. Click **Start**.


### WebSphere Portal - Leap portlet (Deprecated)

If you use Leap with WebSphere Portal, you must update the Leap Portlet.

1. Log in to WebSphere Portal as an administrative user.

2. Go to **Portlet Management** \> **Web Modules** and locate LeapPortlet.war.

3. Click the **Update Web module** icon.

    The **Update Web module** icon is located to the right of the **Web module properties** icon.

4. Click **Browse** to select the updated version of the Leap Portlet, and click **Next**.

5. Review your changes and click **Finish**.


**Parent topic:** [Upgrading](upgradingleap_sec.md)

