# Certificates { #helm_certificates .concept }

The customCertificateSecrets parameter can be used to reference certificates or keys that might be required for SSL communication to the Leap server, the LDAP server, the database, or other services.

Changes to the keystores require a restart of the container.

The following is an example of creating a new Secret from TLS Key and Certificate files:

```
kubectl create secret tls myTlsCertSecret --key="certificate.key" --cert="certificate.crt"
```

The following is an example of adding a DB2 SSL certificate to another Secret:

```yaml
kubectl create secret generic myDb2SslSecret --from-file=mydbservercert.arm 
configuration: 
  leap: 
    . . .
    customCertificateSecrets: 
      myTlsCertSecret: "myTlsCertSecret" 
      myDb2SslSecret: "myDb2SslSecret"
```

This adds the certificates and key to the keystore with the id defaultKeyStore which can then be referenced in the server.xml or any overrides. The defaultKeyStore is also used as the default by many configuration elements in Open Liberty that require a keystore.

**Parent topic:** [Preparation](helm_preparation.md)

