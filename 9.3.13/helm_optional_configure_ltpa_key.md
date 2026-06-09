# LTPA Configuration

## Overview

LTPA (Lightweight Third Party Authentication) enables single sign-on (SSO) capabilities for Leap. Leap uses custom Kubernetes secrets for LTPA configuration.

## Configuration Method

Leap LTPA configuration uses a **custom secret reference** approach:

```yaml
configuration:
  leap:
    ltpa:
      customLtpaSecret: "my-leap-ltpa-secret"
```


## Generating LTPA Keys

To generate LTPA keys for Leap, you can use the OpenLiberty `securityUtility` command:

1. Exec into the Leap pod:
   ```bash
   kubectl -n <namespace> exec -it pod/<release>-leap-0 -- /bin/bash
   ```

2. Generate an LTPA key using the securityUtility command:
   ```bash
   /opt/openliberty/wlp/bin/securityUtility createLTPAKeys --file=/opt/hcl/ltpa.keys --password=<your-password>
   ```

3. Print the LTPA key file content:
   ```bash
   cat /opt/hcl/ltpa.keys
   ```

4. Exit the pod:
   ```bash
   exit
   ```

5. Save the LTPA key file content for creating the secret in the next section

## Secret Structure

The custom LTPA secret must contain these data keys:

| Key | Description | Format |
|-----|-------------|--------|
| `ltpa.keys` | LTPA keys file content | Base64-encoded binary data |
| `password` | Password for LTPA keys | Plain text string |

### Creating a Custom LTPA Secret for Leap

#### Using kubectl

```bash
kubectl create secret generic my-leap-ltpa-secret \
  --from-file=ltpa.keys=/path/to/ltpa.keys \
  --from-literal=password='your-ltpa-password' \
  -n <your-namespace>
```

#### Using a YAML manifest

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-leap-ltpa-secret
  namespace: leap-namespace
type: Opaque
stringData:
  password: "your-ltpa-password"
data:
  ltpa.keys: <base64-encoded-binary-content>
```

## Configuration Examples

### Example 1: Basic Leap LTPA Setup

```yaml
configuration:
  leap:
    ltpa:
      customLtpaSecret: "my-leap-ltpa-secret"
```

**Pre-requisite:** Create the secret

```bash
kubectl create secret generic my-leap-ltpa-secret \
  --from-file=ltpa.keys=./ltpa.keys \
  --from-literal=password='myLtpaPassword' \  
  -n production
```

### Example 2: Leap with Configuration Sharing

Enable shared LTPA configuration for other applications:

```yaml
incubator:
  enableConfigurationSharing: true

configuration:
  leap:
    ltpa:
      customLtpaSecret: "my-leap-ltpa-secret"
```

The Leap LTPA configuration is exported to `leap-shared-config-v1` secret for consumption by other products (DX, etc.).

## Kubernetes Secret Details

### Generated/Referenced Secret Structure

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-leap-ltpa-secret
  namespace: leap-namespace
type: Opaque
data:
  ltpa.keys: <base64-encoded-binary>
stringData:
  password: "your-password"
```

## Troubleshooting

### Issue: LTPA Keys File Not Found

**Symptom:** Leap pod fails with error indicating LTPA keys file is missing.

**Solution:**
1. Verify secret exists:
   ```bash
   kubectl get secret my-leap-ltpa-secret -n <namespace>
   ```

2. Verify key name:
   ```bash
   kubectl describe secret my-leap-ltpa-secret -n <namespace>
   ```

3. Recreate secret with correct key:
   ```bash
   kubectl delete secret my-leap-ltpa-secret
   kubectl create secret generic my-leap-ltpa-secret \
     --from-file=ltpa.keys=/path/to/ltpa.keys \
     --from-literal=password='password'
   ```

**Parent topic:** [Configuration Sharing for co-deployments](helm_config_sharing.md)