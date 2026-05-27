# Update the settings of an existing installation { #helm_update_install .concept }

This section describes how to update the configuration of an HCL Leap or later deployment to Kubernetes or OpenShift installed using Helm.

This section assumes that you prepared your cluster and your custom-values.yaml file, using guidance provided in the Preparation before installing Leap and using Helm topic, and then installed your deployment using the instructions in the Install topic.

## Overview of Helm configuration updates { #section_vrr_mp4_hzb .section }

Once an HCL Leap deployment is installed, it is possible to update its configuration directly using the standard Kubernetes or OpenShift commands \(for example, by updating values in the various config maps\). However, this is NOT the recommended approach. Some of the configuration parameters have interdependencies, as outlined in the Preparation before installing Leap using Helm topic. These require knowledgeable management to make changes that are compatible with interdependency requirements.

The recommended approach for configuration changes is to update the custom-values.yaml file used to install the deployment, and then run a Helm upgrade. This has the added benefit that your custom-values.yaml file remains an up-to-date description of the configuration of your environment.

## Helm upgrade configuration command { #helm-upgrade-configuration-command .section }

After making the needed changes to your custom-values.yaml file, use the following command:

```
# Helm upgrade command 
helm upgrade -n your-namespace -f path/to/your/custom-values.yaml your-release-name path/to/hcl
-leap-deployment-vX.X.X_XXXXXXXX-XXXX.tar.gz 
```

The `your-namespace` is the namespace in which your HCL Leap deployment is installed and `your-release-name` is the Helm release name you used when installing.

The `-f path/to/your/custom-values.yaml` parameter must point to the custom-values.yaml you have updated.

The `path/to/hcl-leap-deployment-vX.X.X_XXXXXXXX-XXXX.tar.gz` is the HCL Leap Helm Chart that you extracted in the preparation steps.

**Parent topic:** [Kubernetes Helm deployment](kubernetes_helm_deployment.md)

