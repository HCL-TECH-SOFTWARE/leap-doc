# Using custom secrets {#section_gsj_vk4_hzb .concept}

Apart from the admin credentials there can be use cases where credentials, secrets or additional key files are required. To pass them to the deployment, the configuration.leap.customSecrets value can be used to reference additional [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/).



Secrets are both injected as environment variables and mounted as files in /mnt/customSecrets in a subfolder named like the referenced key. From there they can be referenced in the server configuration or the configOverrideFiles.



All keys and values under customSecrets must consist of lower-case alphanumeric characters or '-', and must start and end with an alphanumeric character \(e.g. 'my-name', or '123-abc'\). helm install will throw one of the following errors if this criterion is not met:

1.  "configuration.leap.customSecrets: Additional property is not allowed"
2.  "configuration.leap.customSecrets.: Does not match pattern '^\[a-z0-9\]\(\[-a-z0-9\]\*\[a-z0-9\]\)?$'"


## Use custom secret for defining the admin user and password {#helm_admin_customsecret .section}

Instead of providing adminUser and adminPassword for Leap directly in the custom values, a secret can be used to pass the credentials to the deployments.

1.  Create a secret that will be used to reference credentials, this secret should contain the required credential attributes \(e.g. "username", "password"\).

    ``` {#codeblock_ggz_rk4_hzb}
    kubectl create secret generic <secret-name> --from-literal=username=<your-username> --from-
    literal=password=<your-password> --namespace=<namespace> 
    ```

2.  Reference the secret in the custom Helm values. When a secret is used, the adminUser and adminPassword values must be set to an empty string \(""\) or null. Example configuration:

    ```yaml
    security: 
      leap: 
        adminUser: "" 
        adminPassword: "" 
        customAdminSecret: "my-custom-admin-secret"
    ```

## Using custom secrets for credentials {#section_nc2_1l4_hzb .section}

The following is an example of creating a secret `my-custom-db-credentials`, which contains two entries DB\_USERNAME and DB\_PASSWORD:

``` {#codeblock_dnz_1l4_hzb}
kubectl create secret generic my-custom-db-credentials --from-literal=DB_USERNAME=<your-username> --from-
literal=DB_PASSWORD=<your-password> --namespace=<namespace> 
```

The secret is referenced as `db-credentials` in the custom Helm values:

```yaml
configuration: 
  leap:
    . . . 
    customSecrets: 
      db-credentials: my-custom-db-credentials
```

This will result in:

1.  The environment variables DB\_USERNAME and DB\_PASSWORD being injected into the Pod.
2.  The files DB\_USERNAME and DB\_PASSWORD being mounted in `/mnt/customSecrets/db-credentials` inside the Pod each containing the values specified in the secret.

The environment variables can then be referenced in any of the server configurations. For example, to extend the DB2 configuration:

```yaml
configuration: 
  leap:
    . . . 
    configOverrideFiles:
      . . .
      db2Override: | 
        <server description="leapServer">  
          <authData id="db2AuthAlias" user="${DB_USERNAME}" password="${DB_PASSWORD}" />  
          <library id="jdbcDB2" >  
            ... 
          </library>  
          <dataSource id="febDataSource" jndiName="jdbc/BuilderDataSource" statementCacheSize="30" containerAuthDataRef="db2AuthAlias">  
            ... 
          </dataSource>  
        </server> 
```

## Using custom secrets as key file {#section_wc2_kl4_hzb .section}

Below is an example of creating a secret `my-custom-ltpa-key`  from an LTPA key file including the entry LTPA\_KEY:

```
kubectl create secret generic my-custom-ltpa-key --from-file=./ltpa.keys --namespace=<namespace> 
```

The secret is referenced as `ltpa-key` in the custom Helm values:

```yaml
configuration: 
  leap:
    . . . 
    customSecrets: 
      ltpa-key: my-custom-ltpa-key 
```

This will result in:

1.  The environment variables `ltpa.keys` being injected into the Pod.
2.  The file `ltpa.keys` being mounted in `/mnt/customSecrets/ltpa-key` inside the Pod containing the same content as the input file.

The file can then be referenced in any of the server configurations. For example, to use the LTPA key for the server:

```yaml
configuration: 
  leap:
    . . . 
    configOverrideFiles: 
      . . .
      ltpaOverride: | 
        <server description="leapServer">  
          <ltpa keysFileName="/mnt/customSecrets/ltpa-key/ltpa.keys" keysPassword="myLtpaKeyPassword" /> 
        </server> 
```

**Parent topic:** [Preparation](helm_preparation.md)

