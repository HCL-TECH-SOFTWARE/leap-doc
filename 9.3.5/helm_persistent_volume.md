# PersistentVolumeClaims {#helm_persistant_volume .concept}

Defining persistent volumes \(PVs\) for Leap is optional and dependent on your needs.

The 3 volumes that may be required to operate Leap:

-   A volume specified as “ReadWriteMany”. This will be used to pass database drivers or LTPA key files to be used by Leap. When the container is started, any files in this directory are copied into /opt/openliberty/wlp/usr/servers/defaultServer/misc. To reference files in this directory within your configuration snippets, use $\{SERVER\_CONFIG\_DIR\}/misc.

    In order to pass custom extensions to Leap, create an "extensions" directory in this volume. When the container is started, any files in this directory are copied into /opt/openliberty/wlp/usr/servers/defaultServer/extensions.

    **Note:** If files are added to this volume while the system is running then it will need to be restarted.

-   A volume specified as “ReadWriteOnce”. This will be used for log storage and is labeled “log” in the .yaml file.
-   A volume specified as “ReadWriteOnce”. This will be used for the derby database and is labelled “rwo” in the .yaml file. If not using derby, this volume is optional.

These volumes can be directories in your Kubernetes operating system, or a location supplied by a cloud provider.

## Persistent volume types {#section_bbh_5j4_hzb .section}

**Important:** Ensure that your PersistentVolumes \(PVs\) are created with the Reclaim Policy set to RETAIN. This allows for the reuse of PVs after a PersistentVolumeClaim \(PVC\) is deleted. This is important to keep data persisted, for example, between deployments or tests. Refrain from using the Reclaim Policy DELETE unless you have the experience in managing these operations successfully, to avoid unpredictable results. This is not recommended in production use, as deleting PVCs causes the Kubernetes or OpenShift cluster to delete the bound PV as well, thus, deleting all the data on it.

**ReadWriteOnce \(RWO\)**

ReadWriteOnce PVs allow only one pod per volume to perform reading and writing transactions. This means that the data on that PV cannot be shared with other pods and is linked to one pod at a time.

**ReadWriteMany \(RWX\)**

ReadWriteMany PVs support read and write operations by multiple pods. This means the data on that PV can be shared with other pods and can be linked to multiple pods at a time.

## Configuration parameters {#section_hpf_xj4_hzb .section}

To access the PersistentVolumes \(PVs\) on your cluster, the HCL Leap Kubernetes or OpenShift deployment using Helm creates PersistentVolumeClaims \(PVCs\) that binds the PVs to the corresponding pods.

Each PVC that Leap requires allows you to configure the following parameters, as shown below. For a PVC of the Leap application:

``` {#codeblock_ylv_yj4_hzb}
# Persistent Volume Setup 
volumes: 
  # Persistent Volumes for Leap 
  leap: 
    # RWX PVC shared by all Leap pods - RWX. Used to pass auxiliary binary files to all Pods on startup 
    rwx: 
      storageClassName: "manual" 
      requests: 
        storage: "50Mi" 
      # Optional volume name to specifically map to 
      volumeName: 
```

**StorageClassName**

Depending on your Cluster configuration, you may have configured a specific StorageClass that should be used for your PVs and the PVCs of HCL Leap.

This property allows you to enter the name of the StorageClass you want the deployment to use. PVCs then only accepts PVs that match the StorageClassName you have defined in the configuration. If there are no PVs that match, the pods remain pending and do not start until a fitting PV is provided by the cluster.

If you enter an empty StorageClassName, Kubernetes falls back to the default StorageClass configured in your Cluster. Refer to your cloud provider for additional information about your default StorageClass, since this depends on your Kubernetes or OpenShift environment.

Reference the original values.yaml file you have extracted as outlined in the Prepare configuration topic for all configurable PVCs.



**Requests**

Storage. Storage allows you to define the amount of space that is required by the PVC. Once defined, it only accepts PVs that have the same or more storage capacity as requested. If there are no PVs matching the definitions, the pods remain pending and do not start until a properly-sized PV is provided by the cluster.

**Selector**

If you want your deployment to pick up specific PVs that you have created, the selector option can be used to match PVs by their labels.

A detailed description on how to use the selector can be found in the official Kubernetes documentation.

A PVC will only match with a PV satisfying the selector and all the other requirements such as type \(RWO/RWX, as defined by the deployment itself\), storage capacity, and StorageClassName.



**VolumeName**

If you want your deployment to pick up a specific PV that you have created, use of the VolumeName can define that instruction. Ensure that the PV you created has a unique name. Then, add that name as a configuration parameter for the PVC.

The PVCs only matches with a PV of that name, matching the other requirements-like type \(RWO/RWX, as defined by the deployment itself\), storage capacity, and StorageClassName.

As a single persistent Volume is assigned using the volumeName, this should only be used for RWX claims or for Pods that are only ever scaled to one replica.

If a second PersistentVolumeClaim is created with the same volumeName, it can never be fulfilled as the names for Volumes are unique. Please refer to the Selector section to select specific PersistentVolumes for multiple claims.

## Sample PVC configurations {#section_i4t_hk4_hzb .section}

The following are some examples for configuration of the PersistentVolumeClaims \(PVCs\) using your custom-values.yaml:

**Specific volume names**

Specifying a name ensures that Kubernetes or OpenShift only assigns PVs with the matching name to the PVCs created for the applications:

``` {#codeblock_ot3_jk4_hzb}
# Persistent Volume Setup 
volumes: 
  leap: 
    rwx: 
      volumeName: “leap-binaries” 
```

**Adjusted volume size for PVCs**

You may override the default sizes for PVCs by adjusting the storage requests:

``` {#codeblock_fjc_lk4_hzb}
volumes: 
  leap: 
    rwx: 
      requests: 
        storage: "500Mi" 
   rwo: 
      requests: 
        storage: "50Mi" 
    log: 
      requests: 
        storage: "250Mi" 
```

**Parent topic:**[Preparation](helm_preparation.md)

