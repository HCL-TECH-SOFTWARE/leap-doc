# Probes configuration in values.yaml file { #helm_probes_config_valuesfile .concept }

The `liveness` and `readiness` probes such as the status thresholds and time values can be modified.

```
probes:
  leap:
    # Liveness probe using the applications HTTP probe endpoint  
    livenessProbe: 
      failureThreshold: 4 
      initialDelaySeconds: 30 
      periodSeconds: 30 
      successThreshold: 1 
      timeoutSeconds: 30 
    # Readiness probe using the applications HTTP probe endpoint 
    readinessProbe: 
      failureThreshold: 2 
      initialDelaySeconds: 30 
      periodSeconds: 30 
      successThreshold: 1 
      timeoutSeconds: 30 
```

Information about the configuration options can be found in the [Kubernetes documentation](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#configure-probes).

**Parent topic:** [Preparation](helm_preparation.md)

