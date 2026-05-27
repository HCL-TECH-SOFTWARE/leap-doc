# Scaling the Leap deployment

There are two supported ways to run multiple Leap pods in Kubernetes: fixed scaling and horizontal pod autoscaling (HPA). These approaches increase capacity but serve different goals.

## Option 1: Fixed scaling (recommended for high availability)

With fixed scaling, Leap runs with a predefined number of pods that you configure explicitly. All pods are started at deployment time and remain running continuously.

This approach is recommended when:
  - Your primary goal is high availability and failover
  - You want predictable resource usage
  - Your workload is relatively stable

In this configuration, Leap always runs multiple pods, and Kubernetes automatically routes traffic to healthy pods if one becomes unavailable. Horizontal pod autoscaling is not required. For new deployments, start with fixed scaling and add the HPA later if workload patterns change.

## Option 2: Horizontal pod autoscaling (HPA)

With horizontal pod autoscaling, Kubernetes dynamically adjusts the number of Leap pods based on resource usage, such as CPU or memory.

In this configuration:
  - Leap typically starts with a single pod
  - Additional pods are created automatically when defined thresholds are exceeded
  - Pods may scale back down when demand decreases

This approach is recommended when:

  - Workload is variable or bursty
  - You want to optimize resource usage
  - You are comfortable with autoscaling behavior and tuning thresholds

HPA can be used in combination with multiple pods, but it is not required solely for high availability.

## Prerequisite – Configure ingress session affinity (required for multiple replicas)

Before increasing the number of Leap replicas (fixed or autoscaled), configure session affinity (also known as sticky sessions) on the ingress. This ensures that a user’s session is consistently routed to the same Leap pod.

Leap does not require a specific ingress controller. However, the following instructions apply to the NGINX Ingress Controller. If you use a different ingress controller, see your controller documentation or contact HCL Support for information

**Important:** This step is required when running more than one Leap pod. Without session affinity, user sessions can be routed to different pods, resulting in authentication or application errors.

### Steps

!!!note
    Use the namespace where Leap is installed instead of <namespace> in the commands below

1. Identify the Leap ingress resource:

    ```kubectl get ingress -n <namespace>```

2. From the output, note the name of the ingress associated with Leap.

3. Edit the ingress resource:

    ```kubectl edit ingress <ingress-name> -n <namespace>```

4. Locate the annotations section of the ingress and add the following entries:

    ```
    nginx.ingress.kubernetes.io/affinity: "cookie"
    nginx.ingress.kubernetes.io/affinity-mode: "persistent"
    nginx.ingress.kubernetes.io/session-cookie-name: "LEAP_affinity"
    nginx.ingress.kubernetes.io/session-cookie-path: "/"
    nginx.ingress.kubernetes.io/session-cookie-samesite: "Lax"
    nginx.ingress.kubernetes.io/session-cookie-expires: "86400"
    nginx.ingress.kubernetes.io/session-cookie-max-age: "86400"
    ```

    !!!note
        If Leap is embedded in another application (for example, HCL Digital Experience), you may need to change session-cookie-samesite from Lax to None. When using SameSite=None, the cookie must also be marked as Secure, which NGINX Ingress enforces automatically for HTTPS connections.

5. Save and exit the editor.

**Verify session affinity**

Before proceeding with scaling:

  1. Open your browser’s developer tools.
  2. Load the Leap application.
  3. Inspect a network request and view the Cookies section.
  4. Confirm that a cookie named LEAP_affinity is present.

The presence of this cookie confirms that session affinity is configured correctly.

## Scaling Leap without autoscaling (fixed replicas)

To run multiple Leap pods without autoscaling, configure a fixed number of replicas in your Helm values file.

1. Open your custom values.yaml file.

2. Add the following section:
scaling:

    ```
      replicas:
        leap: 2
    ```

    You can increase the replica count above 2 if additional capacity is required.

3. Save the file and apply the change using Helm:

    ```helm upgrade <release-name> <chart> -f values.yaml```

4. Verify that multiple Leap pods are running (substitute your namespace as needed):

    ```kubectl get pods -n <namespace>```

## Autoscaling

The following Kubernetes components are used when configuring autoscaling for HCL Leap.

- **Horizontal Pod Autoscaler (HPA)** A Kubernetes controller that automatically adjusts the number of running pods based on observed resource usage, such as CPU or memory.

- **metrics-server** A cluster-wide service that collects CPU and memory usage metrics from kubelets and makes them available to the HPA.

- **Leap autoscaler configuration (HPA manifest)** A Kubernetes YAML file that defines scaling thresholds, minimum and maximum pod counts, and the Leap workload to be scaled.

### Platform considerations

Each Kubernetes distribution (for example, OpenShift, GKE, EKS, AKS) has its own documented approach for enabling the Horizontal Pod Autoscaler and installing the metrics pipeline. These platform-specific steps are outside the scope of this article. Consult your Kubernetes vendor documentation for details, or engage **HCL Services** for assistance with Kubernetes strategy and implementation.

### Prerequisites

Before enabling autoscaling for Leap, ensure the following prerequisites are met:

1. **HPA support is enabled in the cluster**

    The Kubernetes API must support the autoscaling/v2 API version.

    To verify that the HPA is supported on the cluster, run:
    ```kubectl api-versions | grep autoscaling```

    The output must include autoscaling/v2

2. **metrics-server is installed and healthy**

    To verify that metrics-server is available, run:
    ```kubectl get apiservices | grep metrics```

    The output should include:
    v1beta1.metrics.k8s.io

    These additional checks will also ensure that metrics-server is functioning

    ```
    kubectl top nodes
    kubectl top pods -n <namespace>
    ```

    Each should output the amount of CPU and memory used.

    **If metrics-server is not installed**

    The metrics-server component is not installed by default in all Kubernetes distributions. If the metrics API (metrics.k8s.io) is not available, the HPA cannot retrieve CPU or memory usage and autoscaling will not function.

    Metrics-server is typically installed using vendor-specific tooling:

    - **OpenShift** – Provided and managed by the cluster (do not install manually)

    - **GKE / EKS / AKS** – Available as an add-on or via the Kubernetes project manifests

    - **Self-managed Kubernetes** – Installed using the official metrics-server manifests

    Refer to your Kubernetes vendor documentation for the supported installation method. Alternatively, HCL Services can assist with Kubernetes platform setup and validation.

    **Important:** Do not install metrics-server manually on platforms where it is already managed by the vendor (for example, OpenShift), as this may cause conflicts.

    For more information, see [https://github.com/kubernetes-sigs/metrics-server](https://github.com/kubernetes-sigs/metrics-server).

3. **CPU requests are defined for Leap pods**

The HPA calculates utilization as a percentage of the pod’s CPU request. If CPU requests are not defined, autoscaling will not function. You can use the default, or override them based on your workload requirements.

### Creating the Horizontal Pod Autoscaler

Once the metrics pipeline is in place and CPU requests are configured for Leap, you can create a Horizontal Pod Autoscaler resource to enable autoscaling for the Leap StatefulSet.

Steps:

  1. Create a new file named leap-hpa.yaml.
  2. Paste the following content into the file.

      ```yaml
      apiVersion: autoscaling/v2
      kind: HorizontalPodAutoscaler
      metadata:
        name: leap-hpa
        namespace: leap
      spec:
        scaleTargetRef:
          apiVersion: apps/v1
          kind: StatefulSet
          name: leap-leap
        minReplicas: 1
        maxReplicas: 4
        metrics:
        - type: Resource
          resource:
            name: cpu
            target:
              type: Utilization
              averageUtilization: 50
      ```

  3. Substitute your settings in the example.

      Modify the example to match your environment:

      - **Namespace**
        Set this to your Leap namespace. If Leap is deployed in the default namespace, use default.
      - **minReplicas**
        The minimum number of Leap pods that will run at all times. In larger or production environments, consider starting with a value of 2.
      - **maxReplicas**
        The maximum number of pods the autoscaler is allowed to create. Ensure that sufficient CPU and memory resources are available on the cluster nodes to support the maximum replica count.
      - **averageUtilization**
        The target average CPU utilization percentage across all Leap pods. When this threshold is exceeded, the HPA scales out by creating additional pods.
        
        Avoid setting this value too high, as short bursts of demand may not trigger scaling quickly enough to handle incoming requests.

  4. Apply the HPA configuration by running the following command:

      ```kubectl apply -f leap-hpa.yaml```

  5. **Verify that the HPA was created successfully**

      Run the following command, substituting the namespace used for Leap:

      ```kubectl describe hpa -n <namespace>```

      Confirm that:

      - The HPA named leap-hpa is listed
      - The Target references the Leap StatefulSet
      - The Metrics section shows CPU utilization
      - No error messages are displayed in the Events section


    !!!note
        If CPU usage is currently below the configured threshold, no scaling activity will occur. This is expected behavior.


**Parent topic:** [Kubernetes helm deployment](kubernetes_helm_deployment.md)