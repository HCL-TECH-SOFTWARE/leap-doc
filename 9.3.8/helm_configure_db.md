# Connecting to a Database
To connect Leap with a database you must use the [configOverrideFiles](helm_open_liberty_custom.md) parameter. Sample snippets have been provided, which will need to be updated with your specific details.

!!! note
    All user names and passwords should be managed using [custom secrets](helm_admin_customsecret.md#helm_admin_customsecret).

## Connecting to a DB2 database { #section_z4t_ckh_jzb .section }

The DB2 jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

```yaml
configuration: 
  leap:
    . . . 
    configOverrideFiles: 
      . . .
      db2Override: |  
        <server> 
          <!-- Disable the hard-coded derby datasource -->
          <dataSource id="leapDerbyDatasource" jndiName="disabled" />
          <!-- Adds the DB2 JDBC library to the Leap application classpath -->
          <library id="jdbcDB2" > 
            <fileset dir ="${server.config.dir}/lib" includes="db2jcc4.jar" /> 
          </library> 
          <application id="leap">
            <classloader id="leapClassloader" commonLibraryRef="jdbcDB2"/>
          </application>          
          <authData id="db2AuthAlias" user="${DB_USERNAME}" password="${DB_PASSWORD}" /> 
          <dataSource id="leapDB2DataSource" jndiName="jdbc/BuilderDataSource" statementCacheSize="30" containerAuthDataRef="db2AuthAlias"> 
            <properties.db2.jcc  
                databaseName="LEAPDB"  
                driverType="4" 
                serverName="db2server.acme.com"  
                portNumber="50000" 
                fullyMaterializeLobData="false"  
                progressiveStreaming="2" 
                sslConnection="true" 
                streamBufferSize="2097152"
                isolationLevel="2"
            /> 
            <jdbcDriver libraryRef="jdbcDB2"/> 
            <connectionManager connectionTimeout="180" maxPoolSize="10" minPoolSize="1" reapTime="180" maxIdleTime="1800" agedTimeout="7200" purgePolicy="EntirePool"/> 
          </dataSource> 
        </server>
```

## Connecting to an Oracle database { #section_p2d_3kh_jzb .section }

The oracle jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

!!! note
    To connect over SSL, complete the following steps:

1.  change the URL to:

    ```
    jdbc:oracle:thin:@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCPS)(PORT=2484)(HOST=leap-oracle-db.example.com))(CONNECT_DATA=(SERVICE_NAME=orclpdb1)))
    ```

    You will need to update the host and service name for your database instance.

2.  Create a secret for the SSL certificate used by the Oracle instance.
3.  Specify the connection properties that point to the trust or key store that contain the certificate used by your Oracle instance `${shared.resource.dir}/security/key.p12`

Below is an example snippet for configuring the Leap application to use an Oracle database.

```yaml
configuration: 
  leap:
    . . . 
    configOverrideFiles: 
      . . .
      oracleOverride: | 
        <server> 
            <!-- Disable the hard-coded derby datasource -->
            <dataSource id="leapDerbyDatasource" jndiName="disabled" />
            <!-- Adds the jdbc library to the Leap application classpath -->
            <library id="jdbcOracle" >
                <fileset dir="${server.config.dir}/lib" includes='ojdbc8.jar' />
            </library>
            <application id="leap">
                <classloader id="leapClassloader" commonLibraryRef="jdbcOracle"/>
            </application>            
            <authData id="oracleAuthAlias" user="${DB_USERNAME}" password="${DB_PASSWORD}" /> 
            <dataSource id="leapOracleDataSource" jndiName="jdbc/BuilderDataSource" containerAuthDataRef="oracleAuthAlias"> 
                <jdbcDriver libraryRef="jdbcOracle"/> 
                <properties.oracle URL="jdbc:oracle:thin:@leap-oracle-db.example.com:1521/orclpdb1"/> 
                <connectionManager  
                    minPoolSize="0" maxPoolSize="10" maxIdleTime="10m" 
                    purgePolicy="ValidateAllConnections" 
                /> 
            </dataSource> 
        </server>
```

## Connecting to a PostgreSQL database { #section_cll_jkh_jzb .section }

The PostgreSQL jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

```yaml
configuration: 
  leap:
    . . . 
    configOverrideFiles: 
      . . .
      postgreSQLOverride: |  
        <server> 
          <!-- Disable the hard-coded derby datasource -->
          <dataSource id="leapDerbyDatasource" jndiName="disabled" />
          <!-- Adds the jdbc library to the Leap application classpath -->        
          <library id="jdbcPostgreSQL" > 
            <fileset dir ="${server.config.dir}/lib" includes="postgresql.jar" /> 
          </library> 
          <application id="leap">
            <classloader id="leapClassloader" commonLibraryRef="jdbcPostgreSQL"/>
          </application>        
          <authData id="postgresAuthAlias" user="${DB_USERNAME}" password="${DB_PASSWORD}" />  
          <dataSource id="leapPostgresDataSource" jndiName="jdbc/BuilderDataSource" containerAuthDataRef="postgresAuthAlias"> 
            <properties.postgresql  
                serverName="postgresql.acme.com"  
                databaseName="leapDB"
                portNumber="5432"
            />
            <jdbcDriver libraryRef="jdbcPostgreSQL"/> 
            <connectionManager connectionTimeout="180" maxPoolSize="100" minPoolSize="1" numConnectionsPerThreadLocal="1" /> 
          </dataSource> 
        </server>
```

**Parent topic:** [Open Liberty server customizations](helm_open_liberty_custom.md)