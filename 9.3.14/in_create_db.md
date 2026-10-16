# Create a database { #createdb .concept }

This section describes how to prepare a database for {{shortLeapProductName}}.

{{shortLeapProductName}} is compatible with a {% if isLeap %}DB2, Oracle, or {% endif %}PostgreSQL database.

!!!note
    Keeping the {{shortLeapProductName}} application and database servers co-located is essential.  {{shortLeapProductName}}'s frequent database calls necessitate rapid communication between the servers.  Co-location minimizes latency, resulting in faster data retrieval, quicker response times, and improved overall system efficiency.  Separating the servers introduces network latency, slowing performance.  Co-location supports smooth, real-time operations, especially for database-intensive tasks like querying, updating records, and transaction processing.

{% if isLeap %}
-   **[Creating a DB2 database](in_create_db2.md)**  
The following instructions describe how to manually create the DB2® database for {{shortLeapProductName}}.
-   **[Creating an Oracle database](in_oracle_creating_db.md)**  
The following steps describe how to manually create an Oracle database for use with {{shortLeapProductName}}.
{% endif %}
-   **[Creating a PostgreSQL database](create_postgresql_db.md)**  
The following instructions describe how to manually create the PostgreSQL database for {{shortLeapProductName}}.

**Parent topic:** [Preparing to deploy](in_prep.md)

