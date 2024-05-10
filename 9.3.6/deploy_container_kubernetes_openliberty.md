# Deploying to a Container \(Kubernetes\) Platform - Open Liberty {#deploy_container_kubernetes_openliberty .concept}

The following sections describe how to deploy Leap to a Kubernetes-friendly container platform.

All of the possible configuration parameters may be found in the values.yaml which is part of the deployment package.

## Prerequisite - Specifying persistant volumes {#section_f4f_24s_gxb .section}

Kubernetes must have:

-   A volume specified as “ReadWriteMany”. This will be used to pass database drivers or LTPA key files to be used by Leap. When the container is started, any files in this directory are copied into /opt/openliberty/wlp/usr/servers/defaultServer/misc. To reference files in this directory within your configuration snippets, use $\{SERVER\_CONFIG\_DIR\}/misc.

    **Note:** If files are added to these volumes while the system is running then it will need to be restarted.

-   A volume specified as “ReadWriteOnce”. This will be used for log storage.
-   A volume specified as “ReadWriteOnce”. This will be used for the derby database.  If not using derby, this volume is optional.

These volumes can be directories in your Kubernetes operating system or a location supplied by a cloud provider.

