# Certificates { #helm_certificates .concept }

The customCertificateSecrets parameter can be used to reference certificates or keys that might be required for SSL communication to the {{shortLeapProductName}} server, the LDAP server, the database, or other services.

All keys and values under customCertificateSecrets must consist of lower-case alphanumeric characters or '-', and must start and end with an alphanumeric character \(e.g. 'my-name', or '123-abc'\).

Changes to the keystores require a restart of the container.

The following is an example of creating a new Secret from TLS Key and Certificate files:

```
kubectl create secret tls my-tls-cert-secret --key="certificate.key" --cert="certificate.crt"
```

The following is an example of adding a DB2 SSL certificate to another Secret:

```yaml
kubectl create secret generic my-db2-ssl-secret --from-file=mydbservercert.arm
configuration: 
  leap: 
    . . .
    customCertificateSecrets: 
      my-tls-cert-secret: "my-tls-cert-secret"
      my-db2-ssl-secret: "my-db2-ssl-secret"
```

This adds the certificates and key to the keystore with the id defaultKeyStore which can then be referenced in the server.xml or any overrides. The defaultKeyStore is also used as the default by many configuration elements in Open Liberty that require a keystore.

**Parent topic:** [Preparation](helm_preparation.md)

