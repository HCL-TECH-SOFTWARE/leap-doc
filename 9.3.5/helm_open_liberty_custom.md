# Open Liberty server customizations {#helm_open_liberty_custom .concept}

The configOverrideFiles parameter allows configuration snippets to be passed to the Leap server.

The snippets are merged into the Open Liberty server.xml. After making changes to the .yaml, apply them using the helm upgrade ... command. Changes are picked up by Open Liberty and applied at runtime - this does not require a restart.

**Note:** The name of the customization \(myCustomOverride1 in the following snippet\) can be any string, but you may want it to be descriptive of what is being provided.

``` {#codeblock_t2s_pts_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      myCustomOverride1: | 
        <server description="leapServer"> 
          <basicregistry id="leapRegistry" realm="basicRealm"> 
            <user name="newuser1" password="passw0rd" 
          </basicRegistry> 
        </server>
```

There are several configuration changes that you may need to add to complete your deployment: SMTP, Database, LDAP. Sample snippets have been provided, which will need to be updated with your specific details.

## Connecting to a DB2 Instance {#section_z4t_ckh_jzb .section}

The DB2 jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

``` {#codeblock_y3q_vts_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      db2Override: |  
        <server description="leapServer"> 
          <!-- Disable the hard-coded derby datasource -->
          <dataSource id="leapDerbyDatasource" jndiName="disabled" statementCacheSize="10" />
          <authData id="db2AuthAlias" user="db2inst1" password="diet4coke" /> 
          <library id="jdbcDB2" > 
            <fileset dir ="${server.config.dir}/lib" includes="db2jcc4.jar db2jcc_license_cu.jar" /> 
          </library> 
          <dataSource id="febDataSource" jndiName="jdbc/BuilderDataSource" statementCacheSize="30" containerAuthDataRef="db2AuthAlias"> 
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

## Connecting to an Oracle Instance {#section_p2d_3kh_jzb .section}

The oracle jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

**Note:** To connect over SSL, complete the following steps:

1.  change the URL to:

    ``` {#codeblock_qsm_b5s_gxb}
    jdbc:oracle:thin:@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCPS)(PORT=2484)(HOST=leap-oracle-db.example.com))(CONNECT_DATA=(SERVICE_NAME=orclpdb1)))
    ```

    You will need to update the host and service name for your database instance.

2.  Create a secret for the SSL certificate used by the Oracle instance.
3.  Specify the connection properties that point to the trust or key store that contain the certificate used by your Oracle instance `${shared.resource.dir}/security/key.p12`

Below is an example snippet for configuring the Leap application to use an Oracle database.

``` {#codeblock_bc4_g5s_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      oracleOverride: | 
        <server description="leapServer"> 
            <!-- Disable the hard-coded derby datasource -->
            <dataSource id="leapDerbyDatasource" jndiName="disabled" statementCacheSize="10" />
            <library id="jdbcOracle" >
                <fileset dir="${server.config.dir}/lib" includes='ojdbc8.jar' />
            </library>
            <dataSource id="leapDataSource" jndiName="jdbc/BuilderDataSource" containerAuthDataRef="oracleAuthAlias"> 
                <jdbcDriver libraryRef="jdbcOracle"/> 
                <properties.oracle URL="jdbc:oracle:thin:@leap-oracle-db.example.com:1521/orclpdb1"/> 
                <connectionManager  
                    minPoolSize="0" maxPoolSize="10" maxIdleTime="10m" 
                    purgePolicy="ValidateAllConnections" 
                /> 
            </dataSource> 
            <authData id="oracleAuthAlias" user="leap_admin" password="{xor}KDozPDAyOm5tbA==" /> 
        </server>
```

## Connecting to a PostgreSQL database {#section_cll_jkh_jzb .section}

The PostgreSQL jdbc driver has been included and can be found at $\{server.config.dir\}/lib.

``` {#codeblock_nx3_4vk_gyb}
leap: 
    configOverrideFiles: 
      postgreSQLOverride: |  
        <server description="leapServer"> 
          <!-- Disable the hard-coded derby datasource -->
          <dataSource id="leapDerbyDatasource" jndiName="disabled" statementCacheSize="10" />
          <library id="jdbcPostgreSQL" > 
            <fileset dir ="${server.config.dir}/lib" includes="postgresql-42.6.0.jar" /> 
          </library> 
          <dataSource id="febDataSource" jndiName="jdbc/BuilderDataSource"> 
            <properties.postgresql  
                serverName="postgresql.acme.com"  
                databaseName="leapDB"
                portNumber="5432" 
                user="dbuser"
                password="dbpassword"
            /> 
            <jdbcDriver libraryRef="jdbcPostgreSQL"/> 
            <connectionManager connectionTimeout="180" maxPoolSize="100" minPoolSize="1" numConnectionsPerThreadLocal="1" /> 
          </dataSource> 
        </server>

```

## Connecting to an SMTP Server {#section_t4v_kkh_jzb .section}

Below is an example snippet of configuring Leap to use a mail server. The smtphost will need to be replaced with the proper hostname of the mail server. If authentication is required to communicate with the mail server then replace smtpUser and smtpPassword with the correct values, otherwise remove those likes from the snippet.

``` {#codeblock_xhw_l5s_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      mailOverride: | 
        <server description="leapServer"> 
            <mailSession  
                id="leapMail"
                host="smtphost.com"  
                from="no-reply@smtphost.com"  
                jndiName="mail/BuilderMailSession"  
                description="Leap MailSession"  
                mailSessionID="leapMail" 
                user="smtpUser" 
                password="smtpPassword"> 
                <property name="mail.smtp.auth" value="false" /> 
                <property name="mail.smtp.port" value="25" /> 
            </mailSession> 
        </server>
```

## Connecting to an LDAP Server {#section_fwn_mkh_jzb .section}

Below is an example snippet of configuring Leap to use an LDAP server as part of a federated repository. The baseDN, bindDN and bindPassword will need to be replaced with the proper values. The searchBase for the ldap entity types will also need to be updated. The participatingBaseEntry will need to match the baseDN defined in the LDAP server snippet.

**Note:** The userSecurityNameMapping and groupSecurityNameMapping are required. These properties control how users and groups are displayed while using Leap.

**Note:** For Leap to be able to send mail the loginProperty must be set to mail.

``` {#codeblock_fqn_n5s_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      ldapOverride: | 
        <server description="leapServer"> 
           <federatedRepository id="fedrepo"> 
             <primaryRealm name="FEDREALM"> 
               <participatingBaseEntry name="dc=Acme"/> 
               <userSecurityNameMapping outputProperty="mail" /> 
               <groupSecurityNameMapping outputProperty="cn" /> 
             </primaryRealm> 
           </federatedRepository>
           <ldapRegistry id="OpenLdap" 
              name="dc=Acme" 
              ldapType="Custom" 
              host="ldaphost.acme.com" port="389" 
              baseDN="dc=Acme" 
              searchTimeout="8m" 
              ignoreCase="true" 
              bindDN="cn=Manager,dc=Acme" 
              bindPassword="secret" 
              sslEnabled="false" 
              derefAliases="never"> 
                <loginProperty name="mail"></loginProperty> 
                <ldapEntityType name="PersonAccount"> 
                  <objectClass>inetOrgPerson</objectClass> 
                  <searchBase>ou=People,dc=Acme</searchBase> 
                </ldapEntityType> 
                <ldapEntityType name="Group"> 
                  <objectClass>groupOfUniqueNames</objectClass> 
                  <searchBase>ou=Groups,dc=Acme</searchBase> 
                </ldapEntityType> 
                <customFilters userIdMap="*:mail" groupIdMap="*:cn" groupMemberIdMap="*:uniqueMember" userFilter="(&amp;(mail=%v)(objectclass=inetOrgPerson))" groupFilter="(&amp;(cn=%v)(objectclass=groupOfUniqueNames))"/> 
           </ldapRegistry> 
        </server>
```

## Configure SSL behavior {#section_zlv_nkh_jzb .section}

The default behavior of Open Liberty is that it will not trust any default certificates, which are typically included in all mainstream browsers. By providing this config setting, the default certificates will be trusted enabling communication with third-party services.

``` {#codeblock_hxb_qjz_gxb}
configuration:
  leap:
    configOverrideFiles:
      sslOverride: |
         <ssl id="defaultSSLConfig" trustDefaultCerts="true" />
```

**Parent topic:**[Preparation](helm_preparation.md)

