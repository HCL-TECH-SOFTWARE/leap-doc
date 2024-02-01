# Load images {#helm_load_images .concept}

This section presents how to load the Leap Container or later images into your container image repository, tag them to fit your repository structure, and push them to your repository, so that all Nodes in your Kubernetes or OpenShift cluster can deploy HCL Leap Pods.

To use HCL Leap in your Kubernetes or OpenShift cluster, you have to make the container images available to all nodes of your cluster. Usually this is done by providing them through a container image repository.

Depending on your cloud provider, there may be different types of default container image repositories already configured. Refer to the documentation of your cloud provider for setup and use of such platform container image repository.

It is assumed that you have a repository configured and running, and is reachable from all your Kubernetes or OpenShift cluster nodes.

In the following guidance, the docker CLI is used as a command reference. Tools like Podman may also be used, but are not described in this documentation. The procedure for the use of such tools are the same.

## Retrieving container images {#section_gnq_z34_hzb .section}

The HCL Leap Container package is provided in a compressed .zip file, that can easily be unzipped using a utility of your choice. Download the HCL Leap package from FlexNet, unpack it locally and load the image into your container registry.

To load the image file, you may use the following command:

``` {#codeblock_b43_bj4_hzb}
# Command to load container image into local repository 
# docker load < image-file-name.tar.gz 
docker load < hcl-leap-image_vXXX_XXX_XXXXXXXX-XXXX.tar.gz
```

The custom-values.yaml must then reference the image tag:

``` {#codeblock_tpv_dj4_hzb}
images: 
  # Image tag for each application 
  tags: 
    leap: v1.0.0_20231010-0638_Leap_v9.3.3.40_pjs_release_leap-9.3.3 
```

**Parent topic: **[Preparation](helm_preparation.md)

