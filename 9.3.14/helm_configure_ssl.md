
# Configure SSL behavior

The default behavior of Open Liberty is that it will not trust any default certificates, which are typically included in all mainstream browsers. By providing this config setting, the default certificates will be trusted enabling communication with third-party services.

```yaml 
configuration:
  leap:
    configOverrideFiles:
      . . .
      sslOverride: |
         <server description="leapServer">
           <keystore id="ldapTrustStore" location="/mnt/customSecrets/ldap-ca/ldaptruststore.p12 password="changeit" type="PKCS12" />
           <ssl id="defaultSSLConfig" trustDefaultCerts="true" trustStoreRef="ldapTrustStore"/>
         </server>
```

**Parent topic:** [Open Liberty server customizations](helm_open_liberty_custom.md)