# Creating a container registry secret

## About this task

This is an optional task for environments that require authentication with your container registry.

The steps to create the secret will vary depending on the type of authentication used. It is recommended to refer to your cloud provider’s documentation for complete steps on creating the Kubernetes secret. 

Some general guidance:
- The secret type is ```docker-registry```
- You must know the name of the registry.
- You must include the namespace argument -n, followed by the namespace where you are installing Leap.

There are several methods of authenticating, this guidance will provide some examples in different scenarios.

### Scenario 1: You are authenticating with a service key file

In this example a service account has been created that contains the required permissions to access your container registry. In this example, the following names are used:

- ***secret_name***: the name of the secret you are creating. For example ```registry-secret```
- ***namespace***: the Leap namespace. For example, “leap”.
- ***repo_name***: the repository you are authenticating with. For example us-docker.pkg.dev
- ***_json_key***: If you are using a key file, leave this at _json_key.
- ***example_key.json***: Enter the full path to your key file.
- ***example@example.com***: Enter an email address for your Kubernetes administrator.

Run the command to create the secret:
```
kubectl create secret -n <YOUR_NAMESPACE> docker-registry <secret_name> -n <YOUR_NAMESPACE> --docker-server=repo_name --docker-username=_json_key –docker-password=$(cat example_key.json) --docker-email=<YOUR_DOCKER_EMAIL>
```

For example:
```
kubectl create secret docker-registry registry-secret -n leap --docker-server=us-docker.pkg.dev --docker-username=_json_key --docker-password="$(cat  example_key.json)" --docker-email=example.admin@hcl-software.com
```


### Scenario 2: You are authenticating with user name and password

This is a less secure method of authenticating. In this example you have a user name and a password for the container repository. Execute the commands and ensure to replace the following elements with your environment details.

- ***secret_name***: the name of the secret you are creating. For example ```registry-secret```
- ***namespace***: the Leap namespace. For example, “leap”.
- ***repo_name***: the repository you are authenticating with. For example us-docker.pkg.dev
- ***the_username***: User name used to authenticate.
- ***the_password***: The password used to authenticate.
- ***example@example.com***: Enter an email address for your Kubernetes administrator.

```
kubectl create secret docker-registry <secret_name> -n <YOUR_NAMESPACE> --docker-server=repo_name --docker-username=<YOUR_DOCKER_USERNAME> –docker-password=<YOUR_DOCKER_PASSWORD> --docker-email=<YOUR_DOCKER_EMAIL>
```

For example:
```
kubectl create secret docker-registry registry_secret -n leap --docker-server= us-docker.pkg.dev --docker-username=exampleuser –docker-password=thepassword --docker-email=admin.example@example.com
```

Define the secret name in the custom-values.yaml file.

1. Open the ```custom-values.yaml``` file.
2. Locate the ```images:``` section of the file.
3. Add these new lines to the ```images:``` section. The first two lines should be indented with two spaces. The last line should be indented with 4 spaces. Substitute the secret name you created for this purpose where you see ```registry_secret```.

```yaml
  #secret used for container registry
  imagePullSecrets:
    - name: registry_secret
```

4. Save and close the values.yaml file.


**Parent topic:** [Helm load images](helm_load_images.md)