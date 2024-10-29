# Creating a PostgreSQL database {#create_postgresql_db .task}

The following instructions describe how to manually create the PostgreSQL database for Leap.

In a production environment, you must create a PostgreSQL database before you install HCL Leap to WebSphere Application Server.

**Note:** Do not create a new database if you want to continue using the same database with the existing user content.

Create an empty PostgreSQL database following standard naming conventions. There are two methods:

    -   Use PGAdmin.
    -   Run psql.exe and execute the command create database mydbname;.
    **Note:** The default page size will be 8KB.


**Parent topic: **[Create a Database](in_create_db.md)

