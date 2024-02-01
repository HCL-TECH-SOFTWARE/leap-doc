# Preparation {#helm_preparation .concept}

This section outlines mandatory and optional tasks that need to be done before installation of the HCL Leap Container and later releases using Helm.

**Note:** Deploying the Leap image without using our provided Helm chart is not recommended and not currently supported.

## Mandatory {#section_rkz_1h4_hzb .section}

-   [Prepare a namespace](helm_prepare_namespace.md)
-   [Prepare configuration](prepare_config_helm.md)
-   [Load images](helm_load_images.md)
-   [PersistentVolumeClaims](helm_persistent_volume.md)
-   [Provide admin user a custom secret](helm_admin_customsecret.md)

## Optional {#section_bwh_bh4_hzb .section}

-   [Probes configuration in values.yaml file](helm_probes_config_valuesfile.md)
-   [SAML configuration](helm_saml_config.md)
-   [Certificates](helm_certificates.md)
-   [Open Liberty server customizations](helm_open_liberty_custom.md)
-   [Service Catalog](helm_service_catalog.md)
-   [Leap properties](helm_leap_properties.md)
-   [JVM options](helm_jvm_options.md)
-   [Changing the log level](helm_changing_log_level.md)
-   [Enabling additional Open Liberty features](helm_extending_image.md)

-   **[Prepare a namespace](helm_prepare_namespace.md)**  
You need to create a namespace in your Kubernetes cluster that contains all the resources related to your HCL Leap Container deployment.
-   **[Prepare configuration](prepare_config_helm.md)**  
Create a configuration file that fits the needs of your target HCL Leap Container deployment. The configuration file is the heart of your deployment using Helm. It defines how HCL Leap is deployed to supported platforms, and how it behaves during runtime operations.
-   **[Load images](helm_load_images.md)**  
This section presents how to load the Leap Container or later images into your container image repository, tag them to fit your repository structure, and push them to your repository, so that all Nodes in your Kubernetes or OpenShift cluster can deploy HCL Leap Pods.
-   **[PersistentVolumeClaims](helm_persistent_volume.md)**  
Defining persistent volumes \(PVs\) for Leap is optional and dependent on your needs.
-   **[Provide admin user a custom secret](helm_admin_customsecret.md)**  
Instead of providing adminUser and adminPassword for Leap directly in the custom values, a secret can be used to pass the credentials to the deployments.
-   **[Probes configuration in values.yaml file](helm_probes_config_valuesfile.md)**  
The `liveness` and `readiness` probes such as the status thresholds and time values can be modified.
-   **[SAML configuration](helm_saml_config.md)**  
The Leap Helm chart and container offer a basic SAML configuration through the Helm values. To enable SAML you must pass the IdP Metadata of the identity provider.
-   **[Certificates](helm_certificates.md)**  
The customCertificateSecrets parameter can be used to reference certificates or keys that might be required for SSL communication to the Leap server, the LDAP server, the database, or other services.
-   **[Open Liberty server customizations](helm_open_liberty_custom.md)**  
The configOverrideFiles parameter allows configuration snippets to be passed to the Leap server.
-   **[Service Catalog](helm_service_catalog.md)**  
The serviceCatalog parameter can be used to pass service descriptions to Leap, which will be picked up by Leap automatically.
-   **[Leap properties](helm_leap_properties.md)**  
The leapProperties parameter can be used to add or modify properties to Leap.
-   **[JVM options](helm_jvm_options.md)**  
JVM options can be specified by passing them as environment variables.
-   **[Changing the log level](helm_changing_log_level.md)**  
Sometimes you may need to increase the log level to troubleshoot unexpected behavior.
-   **[Enabling additional Open Liberty features](helm_extending_image.md)**  
Learn how to install additional Open Liberty server features by extending the Leap image.

**Parent topic: **[Kubernetes Helm deployment](kubernetes_helm_deployment.md)

