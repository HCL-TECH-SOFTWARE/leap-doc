# Kubernetes Helm deployment {#kubernetes_helm_deployment .concept}

The Kubernetes container platform allows orchestration features for the automated deployment, coordination, scaling, and management of containerized applications. This deployment mechanism leverages Helm to establish a reliable and repeatable containerized solution.

Learn how to deploy HCL Leap to a Kubernetes-friendly container platform using Helm. This section provides administrators with all Helm-based deployment tasks to deploy HCL Leap and later releases to supported Kubernetes platforms. This includes preparation, installation, and uninstallation of the deployments using Helm.

**Note:** Deploying the Leap image without using our provided Helm chart is not recommended and not currently supported.

Originally designed by Google, now governed by the Cloud Native Computing Foundation \(CNCF\) and developed by Google, Red Hat, and many others, Kubernetes is now widely used by organizations of various sizes to run containers in a cloud environment.

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
-   **[Migrating From WebSphere to Liberty](migrating_websphere_liberty.md)**  
It is possible to migrate from Leap on a WebSphere platform to Leap on Open Liberty.

**Parent topic:**[Deploying Leap](in_overview.md)

