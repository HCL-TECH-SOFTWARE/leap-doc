# Completing the post-deployment tasks {#settingupthefebenvironment .task}

After you run the HCL Leap installer for WebSphere® Application Server, you must complete the deployment by setting up the Leap environment.

Ensure that you have the Administrative user ID and password for deployment.

-   **WebSphere Application Server installations:** The Administrative user ID and Password of your WebSphere Application Server.

When you attempt to log in to Leap for the first time, you are shown a setup screen. Following the steps on the setup screen completes the Leap installation.

There are two phases to set up the Leap environment:

-   Phase 1 - Basic Environment Setup
-   Phase 2 - Secured Environment Setup

    **Note:** To disable this setup page and required admin interaction, add the following property to the Leap\_config.properties:

    ``` {#codeblock_urq_h55_jzb}
    ibm.nitro.SetupAll.setupStatus = start
    ```


1.  Go to the location of your Leap installation. Open a web browser and enter http://hostname:port/apps/

    The web browser shows the following message: “ HCL Leap is not set up. Until that occurs, all normal requests are disabled. Click **Setup** to start the setup process.”

2.  Click **Setup**.

    The Leap setup window opens and automatically runs Phase 1: Basic Environment Setup.

3.  To begin Phase 2- Secured Environment Setup, click **Continue to Secured Setup**.

    You are shown the Leap log in screen.

4.  Log in using the Administrative user ID and Password for WebSphere Application Server

    After you log in, you are returned to the Leap setup page, and the Secured Setup continues automatically.

5.  When the Secured Setup is complete, click **Continue to Manager**.

    Leap is now ready to use.

    1.  If there are any upgrades that must be done, a **Fix** button is shown. Click**Fix** to run the required upgrades.

        Once the upgrades have started, read the on-screen instructions and click **Continue to Manager** to begin working with Leap.

6.  After you have verified that Leap is working, create the these extra table spaces to minimize the database size as applications are created. Connect to the Leap DB2® as a DB2 administrator. Enter the following commands:

    ```
    CREATE BUFFERPOOL FEB4KBP IMMEDIATE SIZE 250 AUTOMATIC PAGESIZE 4 K
    
    CREATE LARGE TABLESPACE USERSPACE4K PAGESIZE 4 K MANAGED BY AUTOMATIC STORAGE BUFFERPOOL FEB4KBP
    
    CREATE BUFFERPOOL FEB8KBP IMMEDIATE SIZE 250 AUTOMATIC PAGESIZE 8 K
    
    CREATE LARGE TABLESPACE USERSPACE8K PAGESIZE 8 K MANAGED BY AUTOMATIC STORAGE BUFFERPOOL FEB8KBP
    
    CREATE BUFFERPOOL FEB16KBP IMMEDIATE SIZE 250 AUTOMATIC PAGESIZE 16 K
    
    CREATE LARGE TABLESPACE USERSPACE16K PAGESIZE 16 K MANAGED BY AUTOMATIC STORAGE BUFFERPOOL FEB16KBP
    ```

    **Note:** This is for DB2 databases only.


**Parent topic:**[Deploying Leap](in_overview.md)

**Related information**  


[Configuring the properties file](co_configuring_the_properties_file.md)

