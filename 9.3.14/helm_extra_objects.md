# Extra Objects

The `extraObjects` property allows you to inject additional, raw YAML documents or manifests directly into the deployment configuration. This is primarily used to append custom, auxiliary resources—such as sidecars, monitoring tools, ConfigMaps, or third-party extensions—that are not natively exposed or structured in the standard configuration schema.

## Secrets

The following configuration parameters represent credentials which can be used by the {{shortLeapProductName}}. During deployment, the system automatically processes these properties to generate native Kubernetes Secret resources.

To maintain security best practices, it is strongly recommended to store these values in a dedicated, secure file (such as `values.secrets.yaml`) and ensure it is excluded from your version control system.

### Image Credentials

Credentials used to authenticate with your container registry (e.g., hclcr.io) to pull application images securely.

| Key | Description |
|-----|-------------|
| `imageCredentials.registry` | Registry hostname (for example, `hclcr.io`) — triggers automatic `hcl-harbor-registry-secret` creation |
| `imageCredentials.username` | Registry username (set in `values.secrets.yaml`) |
| `imageCredentials.password` | Registry password/token (set in `values.secrets.yaml`) |


```yaml
extraObjects:
  ...
  imageCredentials:
    registry: "hclcr.io"
    username: "registry-user"
    password: "secure-registry-password"
  ...
```


### OIDC Credentials

Authentication tokens and Lightweight Directory Access Protocol (LDAP) bind credentials used to secure OpenID Connect identity provider integrations.

| Key | Description |
|-----|-------------|
| `oidcCredentials.oidcClientSecret` | OIDC client secret (set in `values.secrets.yaml`) |
| `oidcCredentials.ldapBindPassword` | LDAP bind password (set in `values.secrets.yaml`) |
| `oidcCredentials.ldapBindDN` | LDAP bind DN (set in `values.secrets.yaml`) |

```yaml
extraObjects:
  ...
  oidcCredentials:
    oidcClientSecret: "oidc-client-secret-string"
    ldapBindDN: "cn=admin,dc=example,dc=com"
    ldapBindPassword: "secure-ldap-password"
  ...
```

### DB Credentials

Connection credentials (username and password) required to authenticate with the application database.

| Key | Description |
|-----|-------------|
| `db.username` | PostgreSQL username (set in `values.secrets.yaml`) |
| `db.password` | PostgreSQL password (set in `values.secrets.yaml`) |

```yaml
extraObjects:
  ...
  db:
    username: "db-admin"
    password: "secure-database-password"
  ...
```

### SSO - LTPA Credentials

The encryption key password required to configure Lightweight Third-Party Authentication (LTPA) tokens for single sign-on (SSO) environments.

| Key | Description |
|-----|-------------|
| `ltpaCredentials.keyPassword` | LTPA password (set in `values.secrets.yaml`) |

```yaml
extraObjects:
  ...
  ltpaCredentials:
    keysPassword: "secure-ltpa-key-password"
  ...
```


## Truststore Properties

Configuration properties for the certificate truststore.

| Key | Description |
|-----|-------------|
| `truststore.cert` | PEM certificate (or chain); if set, a Job auto-generates a PKCS12 Secret |
| `truststore.password` | PKCS12 keystore password (default: `changeit`) |
| `truststore.secretName` | Name of the generated Secret that will be created to hold the truststore cert (default: `leap-ldap-ca`) |
| `truststore.keyName` | Key inside the Secret (default: `ldaptruststore.p12`) |
| `truststore.job.image` | Image for the conversion Job — must have `keytool` and `kubectl` available |
| `truststore.job.imagePullPolicy` | Image pull policy (default: `IfNotPresent`) |

```yaml
extraObjects:
  ...
  truststore:
    cert: |
      # DominoMicro CA — CN=<your_ldap_cn> 
      -----BEGIN CERTIFICATE-----
      <your_domino_microca_cert>
      -----END CERTIFICATE-----
    secretName: leap-ldap-ca
    keyName: ldaptruststore.p12
    password: "changeit"
    job:
      image: "alpine/k8s:1.35.5"
      imagePullPolicy: IfNotPresent
  ...
```

## Image Properties

Configuration properties for pulling the {{shortLeapProductName}} from the image repository.

| Key | Description |
|-----|-------------|
| `images.imagePullSecrets.name` | The secret name for pulling the image from the repository (default: `hcl-harbor-registry-secret`) |
| `images.repository` | The image repository (default: `hclcr.io`) |
| `images.tags.leap` | The version tag `9.3.xx.xx` |

{% if isDWLeap %}
```yaml
extraObjects:
  ...
  images:
    imagePullSecrets:
      - name: hcl-harbor-registry-secret
    repository: hclcr.io
    tags:
      leap: "9.3.13.41"
    names:
      leap: domino-workspace/leap
  ...
```
{% endif %}

{% if isLeap %}
```yaml
extraObjects:
  ...
  images:
    imagePullSecrets:
      - name: hcl-harbor-registry-secret
    repository: hclcr.io
    tags:
      leap: "9.3.13.41"
    names:
      leap: leap
  ...
```
{% endif %}

**Parent topic:** [Prepare a custom configuration file](prepare_config_helm.md)
