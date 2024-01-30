# Creating an Oracle database {#Creating_Oracle_db .task}

The following steps describe how to manually create an Oracle database for use with Leap.

To set up an Oracle database:

1.  Log into Oracle SQLPlus using the SYS DBA role.

    For example, sqlplus / as sysdba.

2.  Create three users.

    Each user is mapped to a schema, where Leap will create tables.

    ```
    ALTER SESSION SET CONTAINER = <Pluggable Database Name>;
    
    CREATE USER FREEDOM IDENTIFIED BY <password>;
    CREATE USER IF\_CMIS IDENTIFIED BY <password>;
    CREATE USER APP\_DATA IDENTIFIED BY <password>;
    
    ```

    Where <password\> is an Oracle accepted password you create.

3.  Create the administrator role.

    Leap accesses the Oracle database through a data source. An administrator is required to establish the connection to the database.

    ```
    CREATE USER <admin> IDENTIFIED BY <password>;
    ```

    Where <admin\> is an administrator's user name, and <password\> is the administrator's password you create.

4.  Set the permissions for the administrative user.

    The following commands grant all permissions and privileges so the administrative user can access the database.

    ```
    GRANT ALL PRIVILEGES TO <admin>;
    GRANT EXECUTE ANY PROCEDURE TO <admin>;
    ```

5.  Set table space quotas for the three users of the schemas.

    ```
    GRANT UNLIMITED TABLESPACE TO FREEDOM;
    GRANT UNLIMITED TABLESPACE TO IF\_CMIS;
    GRANT UNLIMITED TABLESPACE TO APP\_DATA;
    GRANT UNLIMITED TABLESPACE TO <admin\>;
    ```


The Oracle database is created.

**Parent topic:**[Create a Database](in_create_db.md)

