# Connect Leap to LDAP
To connect Leap with an LDAP you must use the [configOverrideFiles](helm_open_liberty_custom.md) parameter. A sample snippet has been provided, which will need to be updated with your specific details.

Below is an example snippet of configuring Leap to use an LDAP server as part of a federated repository. The baseDN, bindDN and bindPassword will need to be replaced with the proper values. The searchBase for the ldap entity types will also need to be updated. The participatingBaseEntry will need to match the baseDN defined in the LDAP server snippet.

Valid values for the "ldapType" are:
- Custom
- IBM Lotus Domino
- IBM SecureWay Directory Server
- IBM Tivoli Directory Server
- Microsoft Active Directory
- Netscape Directory Server
- Novell eDirectory
- Sun Java System Directory Server

It is recommended to specify a "realmName" as it makes it easier to reference entries from this LDAP configuration, specifically in the Leap role assignments.

For more specific details on what is supported by OpenLiberty, refer to their [ldap registry documentation](https://openliberty.io/docs/latest/reference/config/ldapRegistry.html).

**Note:** The userSecurityNameMapping and groupSecurityNameMapping are required. These properties control how users and groups are displayed while using Leap.

**Note:** For Leap to be able to send mail the loginProperty must be set to mail.

## Example connecting to OpenLdap
```
configuration: 
  leap: 
    configOverrideFiles: 
      ldapOverride: | 
        <server description="leapServer"> 
           <federatedRepository id="leapRepo"> 
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

## Example Connecting to Domino LDAP
```
configuration: 
  leap: 
    configOverrideFiles: 
      ldapOverride: | 
        <server description="leapServer"> 
           <federatedRepository id="leapRepo"> 
             <primaryRealm name="FEDREALM"> 
               <participatingBaseEntry name="o=Acme"/> 
               <userSecurityNameMapping outputProperty="mail" /> 
               <groupSecurityNameMapping outputProperty="cn" /> 
             </primaryRealm> 
           </federatedRepository>
           <ldapRegistry id="DominoLdap" 
              name="o=Acme" 
              ldapType="IBM Lotus Domino" 
              host="ldaphost.acme.com" port="389" 
              baseDN="o=Acme" 
              searchTimeout="8m" 
              ignoreCase="true" 
              bindDN="cn=Manager/o=Acme" 
              bindPassword="secret"
              realmName="acmeRealm" 
              sslEnabled="false" 
              derefAliases="never"> 
                <loginProperty name="mail"></loginProperty> 
                <ldapEntityType name="PersonAccount"> 
                  <objectClass>dominoPerson</objectClass>
                </ldapEntityType> 
                <ldapEntityType name="Group"> 
                  <objectClass>dominoGroup</objectClass> 
                </ldapEntityType> 
                <customFilters userIdMap="*:mail" groupIdMap="*:cn" groupMemberIdMap="dominoGroup:member" userFilter="(&amp;(mail=%v)(objectclass=dominoPerson))" groupFilter="(&amp;(cn=%v)(objectclass=dominoGroup))"/> 
           </ldapRegistry> 
        </server>
```

**Parent topic:** [Preparation](helm_preparation.md)