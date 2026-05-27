# Configuration Sharing for co-deployments

This guide explains how to use the standardized Configuration Sharing feature between HCL products such as HCL Leap and HCL Digital Experience (DX) when they are deployed within the same Kubernetes namespace. The feature simplifies integration, reduces manual configuration, and establishes a single source of truth for common settings.

## Prerequisites
    
This feature requires HCL Digital Experience (DX) CF233 or later.
If HCL DX is running an earlier version, is in a different namespace, or the shared Secret is missing, the system falls back to the local configuration.

## Overview and key benefits

Configuration sharing is an opt-in mechanism that allows one product (the producer) to securely share configuration data with other products (the consumers) using native Kubernetes Secrets. The feature provides  the following benefits:

- Automatically configures integrations, such as Single Sign-On (SSO), between co-deployed HCL products without manual configuration.
- Shared configuration is optional, ensuring that consumer products start successfully and remain functional even if the producer product is not deployed or the shared Secret is missing.
- Minimizes configuration effort and operational overhead by using a single shared source for common settings.
- Relies on core Kubernetes features (Secrets), ensuring that no additional complex components or single points of failure are introduced into the cluster.

## Configuration Sharing process

Once enabled, the process is automatically managed by the products' Helm charts.

1. The producer creates the shared Secret.

    When configuration sharing is enabled on a product (the producer, such as Leap), its Helm chart automatically creates a Kubernetes Secret that stores the shared settings.

    - The Secret follows a strict naming convention: `<product-name>-shared-config-v<major-version>`.
    - For example, HCL Leap creates a Secret named `leap-shared-config-v1`.
    - The major version (`v1`) increments only when there are breaking changes to the configuration schema.
    - The Secret contains integration-related settings, such as Lightweight Third-Party Authentication (LTPA) keys provided by Leap
    - The shared Secret is recreated during a Helm upgrade if the values used to generate the configuration have changed (for example, a password update).

2. The consumer uses the shared Secret.

    You can configure other co-deployed HCL products (the consumer, such as DX) to look for and use this shared Secret.

    - The consumer's pod is configured to mount the Secret as a volume.
    - At runtime, the consumer application reads the configuration files from the mounted volume and applies the settings to enable seamless integration.
    - The volume mount is set as `optional: true` in the Kubernetes deployment. This critical feature ensures the consumer product starts successfully even if the producer product is not deployed or the shared Secret is missing.
    - Consumers use the shared configuration when available, but fall back to their default configuration if it is missing.

## Enabling and configuring Configuration Sharing

The entire mechanism is controlled using the feature flags in the Helm `values.yaml` file of your product.

1. Enable the Producer by sharing the product's configuration.

    Set the primary feature flag to `true` in the product's `values.yaml` file:

    ```yaml
    # values.yaml
    # enableConfigurationSharing: Enables the creation of the <chart-name>-shared-config-v1 secret
    # to share configuration with other HCL products in the same namespace.
    enableConfigurationSharing: false  # Change this to true
    ```

    !!! note
        For the LTPA keys to be shared, ensure that LTPA is enabled and properly configured in the producer product (for example, DX). Refer to [LTPA Configuration](helm_optional_configure_ltpa_key.md) for more information.

2. Configure the consumer product to look for a specific shared Secret by specifying the version of the shared configuration to use, providing greater control over the integration.

    Set the `name`, `minVersion`, and `maxVersion` of the `consumeSharedConfigs` parameter in the `values.yaml` file:

    ```yaml
    consumeSharedConfigs:
      - name: leap-shared-config
        minVersion: 1
        maxVersion: 2
    ```

    This explicit configuration helps prevent unintended integration issues when new products that also share configurations are deployed in the future.

3. Once the consumer pod is running, you can access the shared configuration data inside the container.

    The Secret is mounted to a path inside the container, such as `/mnt/shared-config/`. Each key from the shared Secret is exposed as a separate file at that mount path. For example, if the producer's shared Secret contains the key `ltpa.key`, the consumer application will read its contents from the file path: `/mnt/shared-config/leap-shared-config-v1/ltpa.key`.

**Parent topic:** [Kubernetes Helm deployment](kubernetes_helm_deployment.md)
