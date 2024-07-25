# Uninstall Helm deployment {#helm_uninstall .concept}

To remove your HCL Leap deployment from your server deployed using Helm, it is recommended that you use Helm uninstall.

## Uninstall command {#section_m4v_cp4_hzb .section}

To run the uninstall, use the following command as shown in this example:

``` {#codeblock_rd5_dp4_hzb}
# Helm uninstall command 
    helm uninstall your-release-name -n my-namespace 
```

Where `my-namespace` is the namespace where your HCL Leap deployment is installed to and your-release-name is the Helm release name you selected during installation.



After a successful deployment, Helm responds with the following message:

``` {#codeblock_m55_fp4_hzb}
release "your-release-name" uninstalled
```

**Parent topic: **[Kubernetes Helm deployment](kubernetes_helm_deployment.md)

