# Creating a PostgreSQL database {#create_postgresql_db .task}

The following instructions describe how to manually create the PostgreSQL database for Leap.

In a production environment, you must create a PostgreSQL database before you install HCL Leap to WebSphere Application Server.

**Note:** Do not create a new database if you want to continue using the same database with the existing user content.

1.  Create an empty PostgreSQL database following standard naming conventions. There are two methods:

    -   Use PGAdmin.
    -   Run psql.exe and execute the command create database mydbname;.
    **Note:** The default page size will be 8KB.

2.  Optionally, you may create a user for administering the Leap database:

    ``` {#codeblock_t1s_k5k_gyb}
    CREATE ROLE “leap-admin” WITH
    	NOLOGIN
    	NOSUPERUSER
    	NOCREATEDB
    	NOCREATEROLE
    	INHERIT
    	NOREPLICATION
    	CONNECTION LIMIT -1
    	PASSWORD ‘xxx’;
    GRANT pg_database_owner to “leap-admin” WITH ADMIN OPTION;
    
    ```


**Parent topic:**[Create a Database](in_create_db.md)

