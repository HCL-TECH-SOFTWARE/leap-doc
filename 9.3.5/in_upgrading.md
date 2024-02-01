# Upgrading Leap on a traditional platform {#upgradingformsexperiencebuilder .task}

The following instructions describe how to upgrade Leap by using the WebSphere® Application Server Administrative console.

-   Download the upgrade package from HCL License Portal.
-   Back up your existing installation prior to installing the update.
-   Back up your DB2® or Oracle database before you install the update.

1.  To back up your current Leap installation:
2.  Export the Leap EAR file.

    1.  Open the WebSphere Application Server Administrative console.

    2.  Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**.

    3.  Select Leap.

    4.  Click **Export**.

    5.  Click Leap.ear to download the installation file as a backup.

3.  After the backup is complete, use the following instructions to install the upgrade file.

4.  Stop the Leap server.

    1.  Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**

    2.  Select Leap, and click **Stop**.

5.  Check the version of your currently installed Leap.

    You need the version number in step 4c.

    1.  Go to **Modules** \> **Display module build Ids**.

    2.  Check the version for the HCL Leap WAR. An example module version is  “Leap 9.0.0.0 GA”.

6.  Update the Leap installation.

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

7.  If Leap is running on nodes that are managed by Deployment Manager, you must synchronize all nodes where Leap is installed.

8.  Open the WebSphere Application Server Administrative console.

9.  Go to **System Administration** \> **Nodes**.

10. Select all nodes where Leap is installed.

11. Click **Synchronize**.

12. When the upgrade is complete, restart the Leap server.

13. Go to **Applications** \> **Application Types** \> **WebSphere enterprise applications**

14. Select Leap.

15. Click **Start**.

16. If you use Leap with WebSphere Portal, you must update the Leap Portlet.
17. Log in to WebSphere Portal as an administrative user.

18. Go to **Portlet Management** \> **Web Modules** and locate LeapPortlet.war.

19. Click the **Update Web module** icon.

    The **Update Web module** icon is located to the right of the **Web module properties** icon.

20. Click **Browse** to select the updated version of the Leap Portlet, and click **Next**.

21. Review your changes and click **Finish**.


**Parent topic: **[Upgrading](upgradingleap_sec.md)

