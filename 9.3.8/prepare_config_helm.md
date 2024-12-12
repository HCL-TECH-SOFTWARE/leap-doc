# Prepare a custom configuration file { #prepare_config_helm .concept }

Create a configuration file that fits the needs of your target HCL Leap Container deployment. The configuration file is the heart of your deployment using Helm. It defines how HCL Leap is deployed to supported platforms, and how it behaves during runtime operations.

This section explains how to create your own configuration file and how to leverage the existing values.yaml inside the Helm Chart. It also explains how to optionally overwrite settings in case the default set may not be sufficient.

!!! note
    Modification to any files \(chart.yaml, templates\) in hcl-leap-deployment-vX.X.X\_XXXXXXXX-XXXX.tar.tgz is not supported.

## The configuration flow { #section_imf_zh4_hzb .section }

Helm provides multiple ways to define values that can be processed to run an installation. Processing involves a three-step approach, that is ordered sequentially within a hierarchy.

## Helm Chart values.yaml { #section_mkj_134_hzb .section }

Provided with the Leap installation is a TGZ bundle (hcl-leap-deployment-vX.X.X_XXXXXXXX-XXXX.tar.tgz) which contains the helm chart for Leap.  Within the TGZ bundle is a values.yaml file. Do not modify the values.yaml file inside the helm chart. It defines all configurable parameters that a Helm Chart accepts and the default values that are used during an installation. If you do not provide any other configuration during an installation, Helm extracts all deployment information from the values.yaml file inside the Helm Chart.

All parameters that were not overwritten using any other configuration methods return to their default values from the values.yaml file inside the Helm Chart.

To preview these default settings, use the ```helm show values``` command and specify the TGZ bundle name. For example:

```
helm show values hcl-leap-deployment-vX.X.X_XXXXXXXX-XXXX.tar.tgz
```

The output of the command contains the configurable parameters and their default values. 

!!! note
    Do not decompress the helm chart bundle (file ending in .tar.tgz).


## Custom configuration file { #section_rmd_d34_hzb .section }

When you install Leap using Helm, you will specify a custom values file that overrides the default settings. This file contains important details such as information to connect to the container registry, information about the database, authenticating, etc.  This is referred to as the custom-values.yaml file in the product documentation. You may choose a different file name if desired. 

When you follow this product documentation, you will be copying values into this custom-values.yaml file.

!!! note
    There is no need to have the same complete set of parameters inside your custom values file; they are defined by default in the Helm chart. 

For details on creating your custom-values.yaml file, see the topic [Creating and formatting the custom-values.yaml](helm_creating_custom_values_file.md).

## Override parameters { #section_e5x_h34_hzb .section }

It is possible to define values using a --set parameter in the Helm CLI during the installation of a Helm Chart.

Since there are many values that can be configured in the HCL Leap deployment, we do not recommend this technique, since it makes installation commands very large and confusing.


## Additional Topics

-   **[Creating and formatting the custom-values.yaml](helm_creating_custom_values_file.md)**  

**Parent topic:** [Preparation](helm_preparation.md)

