# Configuring Pod Resource Requests and Limits

## Default pod resources

By default, a Leap pod is deployed with the following resource settings:

- Requests
  - CPU: 1 core
  - Memory: 2 GB

- Limits
  - CPU: 3 cores
  - Memory: 4 GB

These defaults provide a starting point for development and testing environments. However, they might not be sufficient for production workloads.

## When to override the defaults

Consider overriding the default pod resources in the following scenarios:

- Your Leap application serves a moderate to high volume of users
- The cluster is busy or resource-constrained
- You are migrating an existing, larger Leap deployment
- You observe performance symptoms such as slow response times or thread starvation

In production environments, explicitly request the resources your workload requires instead of relying on Kubernetes to scale CPU.

## CPU throttling considerations (important)

Leap runs on Open Liberty, which is highly performant but sensitive to CPU throttling. When a pod reaches its CPU limit, Kubernetes may throttle the container, even if additional CPU is available on the node.

CPU throttling can lead to:

  - Increased request latency
  - Hung or stalled threads
  - Reduced throughput under load

For these reasons, it is strongly recommended to:

  - Set CPU requests close to the expected sustained usage
  - Avoid restrictive CPU limits in production
  - Ensure sufficient headroom for peak load and bursty demand

Reserving adequate CPU up front allows the Kubernetes scheduler to place the pod appropriately and helps prevent throttling-related performance issues. 

To effectively reserve the resources and prevent CPU throttling, set the CPU requests and CPU limits to be the same. This ensures the scheduler places the Leap pod only on nodes that can support the workload.

## Memory sizing guidance

Memory limits should be sized to comfortably accommodate:

  - [JVM heap](helm_jvm_options.md)
  - Native memory (threads, JIT, class metadata)
  - Application caches
  - Temporary workload spikes

Setting memory limits too low can result in out-of-memory (OOM) kills, while overly aggressive limits may constrain JVM performance.

## Example override in custom_values.yaml
Below is an example of increasing pod resources for a production deployment:

```yaml
resources:
  leap:
    requests:
      cpu: “4”
      memory: "4Gi"
    limits:
      cpu: "4"
      memory: "4Gi"
```

Monitor your Kubernetes cluster and the Leap container for performance. If the Leap container reaches capacity or is restarts because of out of memory kills, increase the pod size.

**Parent topic:** [Preparation](helm_preparation.md)