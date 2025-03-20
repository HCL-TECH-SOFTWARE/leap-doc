# Manually deploying to WebSphere Application Server { #settingupwas .task }

The following instructions describe how to manually deploy HCL Leap to WebSphere® Application Server.

## Prepare database

Prior to deploying HCL Leap to WebSphere Application Server, you must create a new DB2®, Oracle, or PostgreSQL database.

-  To set up the DB2 database, see [Creating a DB2 database](in_create_db2.md).
-  To set up an Oracle database, see [Creating an Oracle database](in_oracle_creating_db.md#)
-  To set up a PostgreSQL database, see [Creating a PostgreSQL database](create_postgresql_db.md).

## Deploy Leap to WebSphere Application Server

To deploy Leap to WebSphere Application Server, open the WebSphere Application Server Administrative console.

### Configure data source

The datasource defines how WebSphere can communicate with your database.  The necessary settings will depend on the database being used.

1. Depending on your version of WebSphere Application Server, go to either **Resources** or **Application server**.

2. Expand the **JDBC** tree, and go to **Data sources**.

3. Create a new data source. Provide the:
    - host name
    - port
    - database name \(PDB database service name must be used for Oracle\)
    - connection ID (The connection ID must have dbadmin access granted for the database.)
    - password

    !!!note
        If you are connecting to a DB2 database with WebSphere Application Server Connection pool data source, ensure that you select a **non-XA DB2 JDBC provider**, and use a Type 4 driver when configuring the data source.

4. Click **Test connection** to ensure that the connection is made.
    
5.  You must set additional properties for the created data source.

    -   Click the name link for the created data source, then click **Custom Properties**.
    -   Set the **webSphereDefaultIsolationLevel** to **2**

    If using DB2:

    - Locate **fullyMaterializeLobData**, and change the value to **false**.
    - Add a property called **progressiveStreaming**, and set the value to **2**.
    - Set **streamBufferSize** to **2097152** \(2MB\). Add this property if it doesn't exist.
    

### Configure Mail session

Go to **Mail** \> **Mail sessions**.

-   Select the correct scope and choose **New**.
-   Choose **Built-in Mail Provider**.
-   Provide a name, and a JNDI Name.
-   Depending on your version of WebSphere Application Server, you might need to click **Apply** before setting the following properties.
-   Complete the **Outgoing Mail Properties**.
-   Set the **Server**, and **Return email address** fields.
-   Click **OK**

### Configure JVM

Go to **Application Servers** \> **server1** \> **Java and Process Management** \> **Process definition** \> **Java Virtual Machine**, and set the default maximum heap size to *at least* 1024 MB.

### Configure J2C Alias

1.  Go to **Security** \> **Global Security** \> **Authentication** \> **Java Authentication and Authorization Service** \> **J2C authentication data**.

2.  Click **New...**

3.  Enter the following information

    -   **Alias**: vmmAdmin
    -   **User Id**: websphere\_admin\_user\_id
    -   **Password**: websphere\_admin\_user\_password
4.  Click **Apply** to apply your changes.


### Deploy the Leap .ear file

1.  Go to **Applications** \> **Application Types** \> **WebSphere Enterprise Applications**.

2.  Select **Install**.

3.  Select **Local file system**, provide the location of the EAR file, and click **Next**.

    For example: <Installation Directory\>/deploy/hcl-leap.ear.

4.  From the “How do you want to install the application?” options, select **Detailed**, then click **Next**.

5.  Accept the defaults presented by clicking **Next** for all steps until **Map resource references to resource**.

6.  On **Map resource references to resource**:

    -   In the javax.mail.Session section, go to **Target Resource JNDI Name**, and select the mail source.
    -   In the javax.sql.DataSource section, go to **Target Resource JNDI Name**, and select the data source.
7.  Click **Next**.

8.  Accept the defaults for the next step and click **Next**.

9.  On **Map context roots for web modules** use the default context roots, and click **Next**.

10. On **Map security roles to users or groups**:

    -   Select the **SuperAdminUsers** role, and click **Map Users...** or **Map Groups...**. Select the super administrative users or groups to map to the role.
    -   Select the **EditApplicationUsers** role, and click **Map Special Subjects**. Select either All authenticated in Application's Realms, or All authenticated in Trusted Realms to map the value to the role. If both options are available, select All authenticated in Trusted Realms.
    -   Select the **AdministrativeUsers** role, and click **Map Users...** or **Map Groups...**. Select the administrative users or groups to map to the role.
    -   Select the **UseApplicationUsers** role, and click **Map Special Subjects**. Select either All authenticated in Application's Realms, or All authenticated in Trusted Realms to map the value to the role. If both options are available, select All authenticated in Trusted Realms.
    
    For detailed information about the available roles, refer to [Understanding Leap roles](in_leap_roles.md).    

11. Continue to the summary page.

12. Click **Finish** to deploy the ear file.


## Post-deployment steps


### Set class loading preferences

1.  Go to **Enterprise Applications** \> **Leap** \> **Class loader**.

2.  Go to **Class loader order** and select “Classes loaded with local class loader first \(parent last\)”.

3.  Go to **Enterprise Applications** \> **Leap** \> **Manage Modules** \> **HCL Leap xxx.war**.

4.  Go to **Class loader order** and select “Classes loaded with local class loader first \(parent last\)”

5.  Click **Apply** to apply changes.


### Enable security

1.  Expand the **Security** tree and select **Global security**.

2.  In the **Administrative security** section, select the check box beside **Enable administrative security**.

3.  In the **Application security** section, select the check box beside **Enable application security**.

4.  In the **User Account Repository**, ensure **Current Realm Definition** is set to Federated repositories.

5.  Click **Apply** to apply your changes.


### Configure user registry

For more information about configuring a user registry, see the [WebSphere Application Server](https://www.ibm.com/docs/en/was/9.0.5?topic=users-selecting-registry-repository) documentation.


**Parent topic:** [Deploying to a traditional platform](deploytraditional_leap.md)

**Related information**  


[Basic Architecture](in_basic_architecture.md)

