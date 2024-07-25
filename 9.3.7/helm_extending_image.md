# Enabling additional Open Liberty features {#helm_extending_image .concept}

Learn how to install additional Open Liberty server features by extending the Leap image.

The Leap image is shipped with the following server features:

-   adminCenter-1.0
-   appSecurity-3.0
-   federatedRegistry-1.0
-   javaMail-1.6
-   jdbc-4.2
-   jndi-1.0
-   jpa-2.2
-   jwtSso-1.0
-   ldapRegistry-3.0
-   localConnector-1.0
-   mpJwt-2.1
-   openidConnectClient-1.0
-   passwordUtilities-1.0
-   restConnector-2.0
-   servlet-4.0
-   transportSecurity-1.0

Open Liberty has many features that can be enabled. Some features have dependencies on other features, which will be installed automatically. For more information, see the [Open Liberty documentation](https://openliberty.io/docs/latest/reference/feature/feature-overview.html).

If you require a different feature to be installed, you may extend our image. This can be accomplished by creating a Dockerfile. See the following example:

``` {#codeblock_ldv_1gk_d1c}
FROM <image-repo>

RUN /opt/openliberty/wlp/bin/featureUtility installFeature <feature-to-install>
```

After creating a Dockerfile, build the new docker image:

1.  With docker engine running, open command prompt.
2.  Execute the following command: `cd <to-path-of-docker-file>`
3.  Execute the following command: `docker build .`

A new image with the specified feature is installed. Use this extended image when running helm.

**Note:** This is the only supported mechanism for enabling Open Liberty features. There are many features that can be added that have not been tested by HCL and you do so at your own risk. HCL will provide best-effort support for added features as it pertains to Leap.

**Parent topic:** [Preparation](helm_preparation.md)