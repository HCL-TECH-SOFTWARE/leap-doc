# Creating a PostgreSQL database {#create_postgresql_db .task}

The following instructions describe how to manually create the PostgreSQL database for Leap.

In a production environment, you must create a PostgreSQL database before you install HCL Leap to WebSphere Application Server.


!!! note

    Do not create a new database if you want to continue using the same database with the existing user content.

Create an empty PostgreSQL database following standard naming conventions. 

!!! note

    Unquoted database names that contain uppercase letters will be converted to lower case.

There are two methods:

-   Use PGAdmin tooling
-   Use the `psql` command 

Default database settings are adequate; however, it is required that the user that is used for Leap's datasource has full permissions on the database. For example:   
```
GRANT ALL PRIVILEGES ON DATABASE leap_db TO leap_db_user
```


**Parent topic: **[Create a Database](in_create_db.md)

