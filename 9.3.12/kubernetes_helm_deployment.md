# Kubernetes Helm deployment { #kubernetes_helm_deployment .concept }

The Kubernetes container platform allows orchestration features for the automated deployment, coordination, scaling, and management of containerized applications. This deployment mechanism leverages Helm to establish a reliable and repeatable containerized solution.

Kubernetes is a third-party product. HCL support is available to assist in configuration and support-related issues as they pertain to the Leap product. If you require assistance with a full Kubernetes deployment, reach out to HCL Services or one of our HCL Business Partners to inquire about professional services.

Learn how to deploy HCL Leap to a Kubernetes-friendly container platform using Helm. This section provides administrators with all Helm-based deployment tasks to deploy HCL Leap and later releases to supported Kubernetes platforms. This includes preparation, installation, and un-installation of the deployments using Helm.

!!! note
    Deploying the Leap image without using our provided Helm chart is not recommended and not currently supported.

Originally designed by Google, now governed by the Cloud Native Computing Foundation \(CNCF\) and developed by Google, Red Hat, and many others, Kubernetes is now widely used by organizations of various sizes to run containers in a cloud environment.

## Manage operations

Kubernetes automates the deployment and management of containerized applications. The number of concurrent users that Leap can support depends on the size of the deployment. For sizing and deployment-related questions, contact HCL. If you are unfamiliar with this technology, see:

- [Introduction to using Helm](https://helm.sh/docs/intro/using_helm)
- [Kubernetes overview](https://kubernetes.io/docs/concepts/overview)
- [Kubernetes getting started](https://kubernetes.io/docs/setup)

**Cloud deployment:** You can run a Kubernetes cluster on your own hardware or a different cloud provider. You can also use a third-party Kubernetes cloud provider, such as Amazon EKS, Google GKE, or other third-party Kubernetes provider to deploy Leap. Each cloud provider makes security recommendations for running workloads securely in their environment. Refer to the cloud provider's security documentation for further details.

## Scalability

Kubernetes automatically scales a cluster up and down in line with demand without increasing your operations team. To achieve optimal performance, you can provision the infrastructure for Kubernetes before you can install, configure, and connect a component to create a cluster.

## Security

With Kubernetes, you must integrate security throughout the layers of the solution stack before deploying and running the container. Because cloud-native security is multilayer, it is an effective way to address threats across every level of workflow.

For additional information, see [Overview of Cloud Native Security](https://kubernetes.io/docs/concepts/security/overview/) in the Kubernetes documentation.

## Disaster recovery

The backup and restore process is handled outside of Leap. Consult with your Kubernetes vendor for details.

## Namespaces

Many existing production environments use namespaces. A namespace can be used for Leap, but it is not required. When you enable autoscaling, you are creating a namespace for monitoring and custom-metrics. If a namespace is created for Leap, be sure to add the namespace argument to the helm and kubectl commands. For example, if you deploy Leap in a namespace called "leap" and you want to view a list of pod, issue the following command:

```
kubectl -n leap get pods
```

To see a list of namespaces that are configured, issue the following command:

```
kubectl get namespaces
```

For additional information, see [Namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces) topic in the Kubernetes documentation.

## Network

If you are new to Kubernetes, there are some concepts that are helpful to understand how to configure your firewall. There are small differences between cloud providers and on-prem providers where the names of the features may vary. The following information is generic to introduce the concept. It is important to understand the IP addresses used in a deployment have different ranges, and when configuring a firewall rule, the source IP and destination IP need to be considered.

**Node:** A node is the virtual machine or hardware running the Kubernetes cluster, it hosts the pods that run the Leap workloads. A node has an IP address in the node IP range, it will have both an internal IP address and an external IP address. Video nodes are reached by end users from their public IP address directly to the node’s external IP address.

**Pod:** A pod is a Kubernetes based workload, which has one or more containers inside. These are stateless in Leap which means they have a defined life cycle and they do not persist. Each pod has its own unique cluster-wide IP address which changes as the pods are scaled. Typical container-to-container communications between pods on the same host are normally permitted without any additional configuration. For example, the community pod communicating to the proxy pod.

Pods have no awareness of the node host ports or IP addresses. Additionally, you cannot directly reach a pod IP address from outside of the cluster. To expose an application that is running in your pods to be reachable from outside your cluster, Kubernetes services and ingress are used. 

**Network Address Translation (NAT):** If you cannot permit your firewall to allow the entire pod IP address range, consider deploying a Network Address Translation (NAT). A source NAT can replace the source IP address on a packet. Note that each Kubernetes cloud provider has its own implementation and features for NAT. For an overview, see the [Using Source IP](https://kubernetes.io/docs/tutorials/services/source-ip/) topic in the Kubernetes documentation.


## Additional Topics

-   **[Preparation](helm_preparation.md)**  
This section outlines mandatory and optional tasks that need to be done before installation of the HCL Leap Container and later releases using Helm.
-   **[Install commads to deploy](helm_install_commands.md)**  
This topic details install commands that are used to deploy HCL Leap Helm Charts.
-   **[Uninstall Helm deployment](helm_uninstall.md)**  
To remove your HCL Leap deployment from your server deployed using Helm, it is recommended that you use Helm uninstall.
-   **[Update the settings of an existing installation](helm_update_install.md)**  
This section describes how to update the configuration of an HCL Leap or later deployment to Kubernetes or OpenShift installed using Helm.
-   **[Configuring Leap with OIDC](helm_oidc_config.md)**  
This topic describes how to configure an HCL Leap server that was deployed using Helm with an OpenID Connect identity provider.
-   **[Configuring SSO between Leap and DX](https://support.hcl-software.com/community?id=community_blog&sys_id=ba541e4b1b820614f37655352a4bcbc4)**
This article describes how to configure SSO between HCL Leap and HCL Digital Experience (DX)..
-   **[Migrating From WebSphere to Liberty](migrating_websphere_liberty.md)**  
It is possible to migrate from Leap on a WebSphere platform to Leap on Open Liberty.

**Parent topic:** [Deploying Leap](in_overview.md)

