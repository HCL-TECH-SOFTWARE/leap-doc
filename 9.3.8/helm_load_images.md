# Load images { #helm_load_images .concept }

## About this task

The Leap image must be in a container registry or repository that can be accessed by the Kubernetes or OpenShift cluster. 

## Before you begin

Depending on your cloud provider, there may be different types of default container image repositories already configured. Refer to the documentation of your cloud provider for setup and use of such platform container image repository.

It is assumed that you have a repository configured and running, and is reachable from all your Kubernetes or OpenShift cluster nodes. You must know the name of the repository in order to complete this task. If you are unsure what the name of the repository is, consult with your cloud provider documentation.

In the following guidance, the Docker CLI is used as a command reference. Tools like Podman may also be used, but are not described in this documentation. The procedure for the use of such tools are the same.

### Authentication

If your container registry requires authentication, you must configure the Docker CLI to authenticate prior to completing the procedure. If you are uncertain if you have configured authentication you can type in the command:
```
cat ~/.docker/config.json
```

If the docker CLI not authenticated, follow the instructions from your cloud provider to authenticate. The steps vary depending on the type of authentication used.

## Retrieve Leap Container Image

As of 9.3.8, the preferred method of retrieving the Leap container image is from the HCL Harbor container registry.

Older versions are still available from HCL Software portal.

### Procedure A - Load Image from HCL Harbor container registry

It is possible to pull images directly from the HCL Harbor container registry.

1. Login to the Harbor registry. You can obtain the CLI secret from harbor by navigating to your **User Profile** in [HCL Harbor](https://hclcr.io/harbor/projects/96/repositories). You can copy it from the field called **CLI secret**.

    ```
    helm registry login -u <YOUR_HARBOR_USERNAME> -p <YOUR_HARBOR_CLI_SECRET>  https://hclcr.io/
    ```

2. Retrieve the Leap charts from Harbor

    ```
    helm pull oci://hclcr.io/leap/hcl-leap-deployment --version <X.X.X>
    ```

3. Create a kubernetes secret with the name **leap-harbor** with your Harbor username and CLI secret

    !!!note
      The values.yaml is already configured with an **imagePullSecrets** that points to a secret with the name of **leap-harbor**.

    ```
    kubectl create secret -n <YOUR_NAMESPACE> docker-registry leap-harbor --docker-server="hclcr.io" --docker-email='<YOUR_HARBOR_EMAIL>' --docker-username='<YOUR_HARBOR_USERNAME>' --docker-password='<YOUR_HARBOR_CLI_SECRET>'
    ```
  After executing the command from the previous step, you should receive the following message:

    ```
    secret/dx-harbor created
    ```


### Procedure B - Load Image from HCL Software Portal

1. Download the Leap installation file labeled for Kubernetes from the [My HCL Software portal](https://support.hcltechsw.com/csm?id=kb_article&sysparm_article=KB0109011). 

2. Extract the downloaded zip file. The compressed file contains the Leap image as well as the helm chart that is used for the installation. The file labeled **image** is the container image that will be pushed to your container registry. (Do not further extract either of these two files).

3. Run the ```docker load``` command and reference the image file. For example, if the image file name is hcl-leap-image-v1.0.0_20240507-2050-9.3.6.31.tar.gz then use the command:
  ```
  docker load --input hcl-leap-image-v1.0.0_20240507-2050-9.3.6.31.tar.gz
  ```

4. Review the output from the screen, where you see “Loaded image” the part before the colon is the name of the source image. The version number is listed after. Note the source image name and version for a later step.

5. Run the ```docker tag``` command. You will need 3 pieces of information to run this command:
  a. **Source image name:**  This was retrieved from step 4.
  b. **Target image path:** The target image path is the hostname and port (if it is not 443) of your repository.
  c. **Tag name:** You can use the version of your Leap deployment, for example 9.3.8.15, or you can simply use the word “latest”. You will need to use this tag name in the custom-values.yaml file later.


  Now run the command:
  ```
  docker tag <source_image_name> <target_image_path>:<tag_name>
  ```

  For example:
  ```
  docker tag leap/hcl-leap:v1.0.0_20240507-2050 us-docker.pkg.dev/hclexample:latest
  ```

6. Run the ```docker push``` command to push the image into the repository. For this step you will need the target image path from step 5b and the tab name from step 5c.
  ```
  docker push <target_image_path>:<tag_name>.
  ```

  For example:
  ```
  docker push us-docker.pkg.dev/hclexample:latest
  ```

7. Open your custom-values.yaml file.  You will need the hostname and port of your repository and the tag that was selected in step 5c. Substitute your values and modify the below lines to fit your environment.

  ```yaml
  images: 
    # repository name
    repository: “docker.pkg.dev/hclexample”
    # Image tag for each application 
    tags: 
      leap: latest
  ```

8. Save and close the custom_values.yaml.


## What to do next

If your container registry requires authentication, complete the topic [Creating a Container Registry Secret](helm_container_registry_secret.md).

Proceed to [Persistent Volume Claims](helm_persistent_volume.md).

## Additional Topics

-   **[Creating a Container Registry Secret](helm_container_registry_secret.md)**

**Parent topic:** [Preparation](helm_preparation.md)

