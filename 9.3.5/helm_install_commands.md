# Install commads to deploy {#helm_install_commands .concept}

This topic details install commands that are used to deploy HCL Leap Helm Charts.

## Install commands {#section_ogm_n44_hzb .section}

**Important:** Modification to any files \(chart.yaml, templates, etc\) in hcl-leap-deployment-vX.X.X\_XXXXXXXX-XXXX.tar.gz is not supported.

To run the installation of your prepared configurations using Helm, use the following command:

``` {#codeblock_x15_444_hzb}
# Helm install command 
helm install -n my-namespace -f path/to/your/custom-values.yaml your-release-name path/to/hcl-leap-
deployment-vX.X.X_XXXXXXXX-XXXX.tar.gz 
```

-   The `my-namespace` is the namespace where your HCL Leap deployment is installed to.

-   The `-f path/to/your/custom-values.yaml` must point to the custom-values.yaml you have created, which contains all deployment configuration.

-   `your-release-name` is the Helm release name and prefixes all resources created in that installation, such as Pods, Services, and others.

-   `path/to/hcl-leap-deployment-vX.X.X_XXXXXXXX-XXXX.tar.gz` is the HCL Leap Helm Chart that you have extracted as described earlier in the planning and preparation steps.


After a successful deployment, Helm responds with the following message:

``` {#codeblock_b3m_v44_hzb}
NAME: leap 
    LAST DEPLOYED: Thu Jun 17 14:27:58 2023 
    NAMESPACE: my-namespace 
    STATUS: deployed 
    REVISION: 1 
    TEST SUITE: None 
```

## Default URLs post installation {#section_hyj_w44_hzb .section}

During the configuration process, you might need the following URLs to access different user interfaces.

Use the following default URLs to access HCL Leap and OpenLiberty Console:

**HCL Leap**

``` {#codeblock_jb4_y44_hzb}
http://yourserver/apps
```

**HCL Leap Rest API**

``` {#codeblock_mkv_y44_hzb}
http://yourserver/apps-basic
```

There are a few endpoints that can be helpful for identifying and debugging datasource connections:

**View DataSource Configuration**

``` {#codeblock_pqc_z44_hzb}
https://yourserver/ibm/api/config/dataSource/<datasourceId>
```

The result is an html page that shows a json output of the configuration that is known by the server.

**Validate DataSource Connection**

``` {#codeblock_ftt_z44_hzb}
https://yourserver/ibm/api/validation/dataSource/<dataSourceId>
```

Endpoint attempts to make a database connection, the result is a json output that shows the result. If the connection fails, the output may contain more detail to assist in the troubleshooting.

**Parent topic:**[Kubernetes Helm deployment](kubernetes_helm_deployment.md)

