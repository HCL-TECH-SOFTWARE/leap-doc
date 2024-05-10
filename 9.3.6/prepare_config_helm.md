# Prepare configuration {#prepare_config_helm .concept}

Create a configuration file that fits the needs of your target HCL Leap Container deployment. The configuration file is the heart of your deployment using Helm. It defines how HCL Leap is deployed to supported platforms, and how it behaves during runtime operations.

This section explains how to create your own configuration file and how to leverage the existing values.yaml inside the Helm Chart. It also explains how to optionally overwrite settings in case the default set may not be sufficient.

**Note:** Modification to any files \(chart.yaml, templates\) in hcl-leap-deployment-vX.X.X\_XXXXXXXX-XXXX.tar.gz is not supported.

## The configuration flow {#section_imf_zh4_hzb .section}

Helm provides multiple ways to define values that can be processed to run an installation. Processing involves a three-step approach, that is ordered sequentially within a hierarchy.

## Helm Chart values.yaml {#section_mkj_134_hzb .section}

Every Helm Chart contains a values.yaml file. It defines all configurable parameters that a Helm Chart accepts and the default values that are used during an installation. If you do not provide any other configuration during an installation, Helm extracts all deployment information from the values.yaml file inside the Helm Chart.

All parameters that were not overwritten using any other configuration methods return to their default values from the values.yaml file inside the Helm Chart.

## Custom value file {#section_rmd_d34_hzb .section}

Helm provides you with a way to maintain your own custom values files. You can specify a custom values file you want to use when running an installation.

This custom values file only needs to contain the parameters that you want to overwrite with your preferred settings.

**Note:** There is no need to have the same complete set of parameters inside your custom values file, as there are available by default in the Helm Chart values.yaml. As outlined previously in this section, everything that is not defined in your custom values file are applied using the defaults from values.yaml inside the Helm Charts.

Be aware that the parameters you can configure using your custom values file need to exactly align with those provided by the Helm Charts own values.yaml. You cannot configure anything that is not exposed in the values.yaml definition.

## Override parameters {#section_e5x_h34_hzb .section}

It is possible to define values using a --set parameter in the Helm CLI during the installation of a Helm Chart.

Since there are many values that can be configured in the HCL Leap deployment, we do not recommend this technique, since it makes installation commands very large and confusing.

## The default HCL Leap Container values.yaml file {#section_ftl_k34_hzb .section}

HCL Leap Helm Chart provides a default values.yaml, which contains all possible configuration parameters.

To access this file, you may use the following command when you have the HCL Leap or later Helm Chart tar.gz file on hand:

``` {#codeblock_r5s_m34_hzb}
# Command to show values from Helm Chart 
helm show values hcl-leap-deployment.tar.gz  
```

What appears in the console is all the configurable parameters and their default values.

## A custom configuration file {#section_z5g_434_hzb .section}

Helm allows you to provide a custom configuration file during the installation or upgrade process.

That file only overwrites settings that are defined within it. For parts of the configuration that are not defined in your custom configuration file, Helm returns to the default values in the values.yaml file inside the Leap Helm Chart. This allows you to keep the overall size of your configuration file small and the maintainability high.

This documentation refers to the custom configuration file as custom-values.yaml. You may name your custom configuration file as preferred.

**Note:** Including all of the parameters from the values.yaml is not necessary and may bloat your configuration file with values that are already present in the Leap Helm Chart. Only specify what you want to change from its default value.

**Parent topic: **[Preparation](helm_preparation.md)

