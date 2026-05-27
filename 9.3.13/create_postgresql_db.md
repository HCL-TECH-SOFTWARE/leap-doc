# Creating a PostgreSQL database { #create_postgresql_db .task }

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

The default database settings are adequate; however, the user that is used for Leap's datasource must have full permissions on the database. For example:
```
GRANT ALL PRIVILEGES ON DATABASE leap_db TO leap_db_user
```

!!!warning
    The Leap DB should be the only database in the PostgreSQL deployment.

    The privileges are not set correctly, if you see an error like:
    
     ```Caused by: org.postgresql.util.PSQLException: ERROR: cannot drop schema app_data because other objects depend on it Detail: table app_data."568BSH9EJH8K7O0GQLR0NE2MM9" depends on schema app_data Hint: Use DROP ... CASCADE to drop the dependent objects too.```


**Parent topic:** [Create a Database](in_create_db.md)

