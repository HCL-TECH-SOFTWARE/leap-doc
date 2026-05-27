# Deploy custom extensions { #helm_deploy_custom_extension .concept }

A custom extension, which historically was a .jar file located in the .../Leap/extensions directory, may also be deployed into your Leap Kubernetes deployment.

1. The container must have a RWX persistent volume, see [Persistent Volume Claims](helm_persistent_volume.md).

2. Create an 'extensions' directory in the RWX persistent volume.

3. Copy your custom extensions into the 'extensions' directory in the persistent volume.  When the pod is started, any files in this directory will be copied into the 'customerExtensions' directory (within the pod).  Leap will automatically register any extension in the 'customerExtensions' directory.

!!! note
    If files are added to this directory while the system is running then it will need to be restarted.


## Verify the custom extension deployment

1. On pod startup there will be a message to indicate the status. Check the logs to locate this message:

```
[...]$ kubectl -n dxns logs leap-deployment-leap-0

...
Found mounted extension files in '/mnt/rwx/extensions'. Copying files to '/opt/openliberty/wlp/usr/servers/defaultServer/customerExtensions'
...
```

2. You can also open a shell to the Leap server to verify that the files were copied.

```
[...]$ kubectl -n dxns exec --stdin --tty leap-deployment-leap-0 -- /bin/bash
[...]$ ls -al /opt/openliberty/wlp/usr/servers/defaultServer/customerExtensions/
```

3. Leap will also show, in the logs, that the extension was registered successfully.

```
[4/18/24 16:33:29:454 PDT] 000000c2 id=00000000 com.ibm.form.platform.service.framework.DirectoryWatcher     I processArtifact FSPDI5: The Bundle, sampleExtension.jar loaded successfully.
```

**Parent topic:** [Preparation](helm_preparation.md)

