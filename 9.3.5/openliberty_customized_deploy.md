# Customized deployment {#openliberty_customized_deploy .concept}

The following are the most common changes needed for a production deployment:

-   [Specify persistent volumes](deploy_container_kubernetes_openliberty.md#section_f4f_24s_gxb)
-   Change admin credentials
-   Configure a database
-   Configure an SMTP server
-   Configure an LDAP
-   Define Custom Service Configurations
-   Modify Leap properties

## Encoding passwords {#section_ev2_553_hxb .section}

All passwords passed in the .yaml file should be encoded. You can encode a password using a utility provided by Open Liberty. To access this utility in your kubernetes environment use the command:

``` {#codeblock_g5v_v53_hxb}
kubectl -n dxns exec -it leap-deployment-leap-0 -- /opt/openliberty/wlp/bin/securityUtility encode <thePassword>
```

The result of the command will be a string value like `{xor}Kzc6Dz4sLCgwLTs=`. Use this encoded value when specifying a password.

## Change server Admin credentials {#section_edb_2js_gxb .section}

This is optional. The credentials supplied below are used in the container startup to run configuration tasks and setup Leap.

The default credentials are set to leapadmin for username and password.

To change the default admin, add this snippet to your .yaml file and update the `adminUser` and `adminPassword` properties.

``` {#codeblock_wb4_shm_gxb}
security: 
  leap: 
    adminUser: "leapadmin" 
    adminPassword: "leapadmin"
```

## SAML configuration {#section_g5g_x5s_gxb .section}

The Leap Helm chart and container offer a basic SAML configuration through the Helm values. This can be used to enable SAML, deploy the WebSphereSamlSP.ear, configure the ACS URL, pass the IdP Metadata of the identity provider and add trusted realms.

**Note:** Please note that this configuration can currently only be used to enable the SAML TAI SSO. To disable it, please set the enabled flag to false and remove the Trust Association manually in WebSphere.

The idpMetadata accepts IdP Metadata in xml format. Please use the [multiline string feature of Helm](https://helm.sh/docs/chart_template_guide/yaml_techniques/#strings-in-yaml) to pass this value.

The `ssoId9999` is used to create the SAML TAI SSO.Example configuration:

``` {#codeblock_q15_y3m_gxb}
security:
  leap:
    saml:
      enabled: true
      acsUrl: "https://native-kube-kevin.team-q-dev.com:9443/samlsps/acs"
        idpMetadata: |
          <EntityDescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="SAMLtestIdP" xmlns:ds="http://www.w3.org/2000/09/xmldsig#" xmlns:shibmd="urn:mace:shibboleth:metadata:1.0" xmlns:xml="http://www.w3.org/XML/1998/namespace" xmlns:mdui="urn:oasis:names:tc:SAML:metadata:ui" validUntil="2100-01-01T00:00:42Z" entityID="https://samltest.id/saml/idp">
             <IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol urn:oasis:names:tc:SAML:1.1:protocol urn:mace:shibboleth:1.0">
               <Extensions>
                 <shibmd:Scope regexp="false">samltest.id</shibmd:Scope>
                 <mdui:UIInfo>
                   <mdui:DisplayName xml:lang="en">SAMLtest IdP</mdui:DisplayName>
                   <mdui:Description xml:lang="en">A free and basic IdP for testing SAML deployments</mdui:Description>
                   <mdui:Logo height="90" width="225">https://samltest.id/saml/logo.png</mdui:Logo>
                 </mdui:UIInfo>
               </Extensions>
               <KeyDescriptor use="signing">
                 <ds:KeyInfo>
                   <ds:X509Data>
                     <ds:X509Certificate>
                       ...
                     </ds:X509Certificate>
                   </ds:X509Data>
                 </ds:KeyInfo>
               </KeyDescriptor>
               <ArtifactResolutionService Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP" Location="https://samltest.id/idp/profile/SAML2/SOAP/ArtifactResolution" index="1" />
               <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://samltest.id/idp/profile/SAML2/Redirect/SLO"/>
               <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://samltest.id/idp/profile/SAML2/POST/SLO"/>
               <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST-SimpleSign" Location="https://samltest.id/idp/profile/SAML2/POST-SimpleSign/SLO"/>
               <SingleSignOnService Binding="urn:mace:shibboleth:1.0:profiles:AuthnRequest" Location="https://samltest.id/idp/profile/Shibboleth/SSO"/>
               <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://samltest.id/idp/profile/SAML2/POST/SSO"/>
               <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST-SimpleSign"  Location="https://samltest.id/idp/profile/SAML2/POST-SimpleSign/SSO"/>
               <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://samltest.id/idp/profile/SAML2/Redirect/SSO"/>
               <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP" Location="https://samltest.id/idp/profile/SAML2/SOAP/ECP"/>
             </IDPSSODescriptor>
         </EntityDescriptor>
```

## Certificates {#section_x5j_x5s_gxb .section}

The customCertificateSecrets parameter can be used to reference certificates or keys that might be required for SSL communication to the Leap server, the LDAP server, the database, or other services. Changes to the keystores require a restart of the container.

The following is an example of creating a new Secret from TLS Key and Certificate files:

``` {#codeblock_qhf_vss_gxb}
kubectl create secret tls myTlsCertSecret --key="certificate.key" --cert="certificate.crt"
```

The following is an example of adding a DB2 SSL certificate to another Secret:

``` {#codeblock_o41_wss_gxb}
kubectl create secret generic myDb2SslSecret --from-file=mydbservercert.arm 
configuration: 
  leap: 
    customCertificateSecrets: 
      myTlsCertSecret: "myTlsCertSecret" 
      myDb2SslSecret: "myDb2SslSecret"
```

This adds the certificates and key to the keystore with the id defaultKeyStore which can then be referenced in the server.xml or any overrides. The defaultKeyStore is also used as the default by many configuration elements in Open Liberty that require a keystore.

## Open Liberty server customizations {#section_pqj_3ts_gxb .section}

The configOverrideFiles parameter allows configuration snippets to be passed to the Leap server. The snippets are merged into the Open Liberty server.xml. After making changes to the .yaml, apply them using the helm upgrade ... command. Changes are picked up by Open Liberty and applied at runtime - this does not require a restart.

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

**Connecting to a DB2 Instance**

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

**Connecting to an Oracle Instance**

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

**Connecting to a PostgreSQL database**

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

**Connecting to an STMP Server**

Below is an example snippet of configuring Leap to use a mail server. The smtphost will need to be replaced with the proper hostname of the mail server. If authentication is required to communicate with the mail server then replace smtpUser and smtpPassword with the correct values, otherwise remove those likes from the snippet.

``` {#codeblock_xhw_l5s_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      mailOverride: | 
        <server description="leapServer"> 
            <mailSession  
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

**Connecting to an LDAP Server**

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

**Configure SSL behavior**

The default behavior of Open Liberty is that it will not trust any default certificates, which are typically included in all mainstream browsers. By providing this config setting, the default certificates will be trusted enabling communication with third-party services.

``` {#codeblock_hxb_qjz_gxb}
configuration:
  leap:
    configOverrideFiles:
      sslOverride: |
         <ssl id="defaultSSLConfig" trustDefaultCerts="true" />
```

## Service Catalog {#section_jbb_r5s_gxb .section}

The serviceCatalog parameter can be used to pass service descriptions to Leap, which will be picked up by Leap automatically.

Each service definition in the .yaml is made up of a label and the xml content of the service description. The XML content will be copied into a file and placed in the service catalog.

For more information on creating service descriptions, see [Service Description](ref_service_service_description.md).

Example:

``` {#codeblock_n2n_fkt_gxb}
configuration:
  leap:
    serviceCatalog:
       sampleServiceDescription.xml: |
         <?xml version="1.0" encoding="utf-8"?>
         <serviceDescription>
         <id>sample-service-description</id>
         <defaultLocale>en</defaultLocale>
         <transportId>HTTPServiceTransport</transportId>
         <name xml:lang="en">Sample service Description</name>
         <description xml:lang="en"></description>
            . . . 
         </serviceDescription>
```

## Leap Properties {#section_ynm_t5s_gxb .section}

The leapProperties parameter can be used to add or modify properties to Leap.

**Note:** The property ibm.nitro.NitroConfig.loginIdIsEmail must be added and set to true.

Below is an example snippet of setting leap-specific properties:

``` {#codeblock_hd4_vjt_gxb}
configuration:
   leap:
     leapProperties: | 
        ibm.nitro.InfoEntryPoint.dailyInfo = <div>Welcome to <b>HCL Leap 9.3.2</b> in Kubernetes!</div> 
        ibm.nitro.NitroConfig.serverURI=http://myleapserver.example.com
        ibm.nitro.NitroConfig.loginIdIsEmail = true
```

For more information, see [Configuration properties](co_configuration_properties.md).

## JVM options {#section_dc2_rjz_gxb .section}

JVM options can be specified by passing them as environment variables. The snippet below sets the maximum jvm memory usage to 2GB.

``` {#codeblock_qgx_sjz_gxb}
environment:
   pod:
     leap:
       name:  JVM_MAX
       value: "-Xmx2048m"
```

## Changing the log level {#section_nfl_hhh_hxb .section}

Sometimes you may need to increase the log level to troubleshoot unexpected behavior. Below is an example of how to change the log level.

``` {#codeblock_akc_jhh_hxb}
logging:
  leap:
    level: Leap:*=detail:com.ibm.form.nitro.*=finest
```

## Assigning User's to Leap Roles {#section_tm4_n53_hxb .section}

Leap has several application-level roles that control who can access different features. You must map Administrative users and Edit Application users to an appropriate realm.

-   **SuperAdminUsers** - Super Administrative Users are users, or groups, with administrator privileges for all Leap applications without explicit security settings.
-   **AdministrativeUsers** - Administrative users are able to set up the Leap server. You must have an Administrative User to complete the installation process.
-   **EditApplicationUsers** - Authenticated users that can design, deploy, and use Leap applications.
-   **UseApplicationsUsers** - Authenticated users that can use deployed Leap applications. All users in the AdministrativeUsers, and EditApplicationUsers automatically have access to use deployed applications. Only adjust this setting if you want to allow a broader set of users than those listed in the AdministrativeUsers, and EditApplicationUsers roles. Otherwise, leave this role unmapped.

``` {#codeblock_st2_s53_hxb}
configuration:
  leap:
    roleMapping:
      SuperAdminUsers:
        Everyone: false
        AllAuthenticated: false
        MappedUsers:
          - leapadmin
        MappedGroups: []
        AllAuthenticatedInTrustedRealms: false
        MappedUsersAccessIDs: []
        MappedGroupsAccessIDs: []
      EditApplicationsUsers:
        Everyone: false
        AllAuthenticated: false
        MappedUsers:
          - leapadmin
        MappedGroups: []
        AllAuthenticatedInTrustedRealms: false
        MappedUsersAccessIDs: []
        MappedGroupsAccessIDs: []
      AdministrativeUsers:
        Everyone: false
        AllAuthenticated: false
        MappedUsers:
          - leapadmin
        MappedGroups: []
        AllAuthenticatedInTrustedRealms: false
        MappedUsersAccessIDs: []
        MappedGroupsAccessIDs: []
      UseApplicationsUsers:
        Everyone: false
        AllAuthenticated: false
        MappedUsers: []
        MappedGroups: []
        AllAuthenticatedInTrustedRealms: true
        MappedUsersAccessIDs: []
        MappedGroupsAccessIDs: []
```

