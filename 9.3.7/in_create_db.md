# Create a database {#createdb .concept}

This section describes how to prepare a database for Leap.

Leap is compatible with a DB2, Oracle, or PostgreSQL database.

!!!note
    Keeping the Leap application and database servers co-located is essential.  Leap's frequent database calls necessitate rapid communication between the servers.  Co-location minimizes latency, resulting in faster data retrieval, quicker response times, and improved overall system efficiency.  Separating the servers introduces network latency, slowing performance.  Co-location supports smooth, real-time operations, especially for database-intensive tasks like querying, updating records, and transaction processing.

-   **[Creating a DB2 database](in_create_db2.md)**  
The following instructions describe how to manually create the DB2® database for Leap.
-   **[Creating an Oracle database](in_oracle_creating_db.md)**  
The following steps describe how to manually create an Oracle database for use with Leap.
-   **[Creating a PostgreSQL database](create_postgresql_db.md)**  
The following instructions describe how to manually create the PostgreSQL database for Leap.

**Parent topic:** [Preparing to deploy](in_prep.md)

