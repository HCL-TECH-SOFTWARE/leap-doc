# Container resource management

The default Helm values included in the HCL Leap Helm Chart provide only the minimum supported CPU and memory configuration. You can customize these settings in `custom-values.yaml` to suit your deployment requirements, in accordance with the [Kubernetes Resource Management guidelines](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/).

!!!note
    This configuration defines the minimum requirements. For production environments or higher workloads, scale to small, medium, or larger configurations as appropriate. If performance issues occur, increase resource allocations accordingly.

```yaml
# Resource allocation settings, definition per pod
# Use number + unit, e.g. 1500m for CPU or 1500M for Memory
resources:
  # Leap resource allocation
  leap:
    requests:
      cpu: "1000m"
      memory: "2G"
    limits:
      cpu: "3000m"
      memory: "4G"
```

## Unlimited resource limits

All limits are explicitly set to null to unset them in Kubernetes and allow for unlimited resources depending on the Kubernetes Cluster. Cluster and namespace level resource limits still apply.

The limits are removed individually for either CPU or Memory. For example, to remove the Leap CPU limit set the following:

```yaml
resources:
  leap:
    limits:
      cpu: null
      memory: "6144Mi"
```

To remove the limits entirely for an application, set the following:

```yaml
resources:
  leap:
    limits: null
```

**Parent topic:** [Preparation](helm_preparation.md)