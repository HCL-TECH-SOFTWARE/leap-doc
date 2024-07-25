# Creating a DB2 database {#settingupwas .task}

The following instructions describe how to manually create the DB2® database for Leap.

In a production environment, you must create DB2 database before you install HCL Leap to WebSphere® Application Server.

**Note:** Do not create a database if you want to continue using the same database with the existing user content.

1.  To set up the DB2 database:

    1.  Create an empty DB2 database with a maximum database name of 8 characters, and a maximum page size of 32768.

    2.  Connect to the database and create a User Temporary table space.

        Use the following settings for the temporary table space:

        -   Large\_usertemp pagesize 32K
        -   Managed by automatic storage extentsize 16
        -   <bufferpool-name\> is the name of your DB2 large buffer pool. Each DB2 server can have a different name.
        ```
        db2 "CREATE DB LEAPDB using codeset UTF-8 territory us PAGESIZE 32768"
         db2 connect to LEAPDB
        db2 "CREATE BUFFERPOOL bufferpool-name IMMEDIATE SIZE 250 PAGESIZE 32K"
        db2 "CREATE USER TEMPORARY TABLESPACE LARGE_USERTEMP PAGESIZE 32k MANAGED BY AUTOMATIC STORAGE EXTENTSIZE 16 PREFETCHSIZE 16 BUFFERPOOL bufferpool-name"
        ```

## Minimum Permissions

If you do not want to give the DB2 user DBADM then you will need to assign the following permissions otherwise Leap will fail.

- CONNECT
- SELECT
- INSERT
- UPDATE
- DELETE
- CREATETAB
- IMPLICIT_SCHEMA
- USE of tablespace



**Parent topic:** [Create a Database](in_create_db.md)

