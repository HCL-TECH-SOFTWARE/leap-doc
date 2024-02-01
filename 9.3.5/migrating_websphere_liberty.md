# Migrating From WebSphere to Liberty {#migrating_websphere_liberty .concept}

It is possible to migrate from Leap on a WebSphere platform to Leap on Open Liberty.

The most common parts of a Leap deployment are the following:

-   Database
-   LDAP
-   Mail server

Each of these three parts are external to Leap and will be configured in the deploy-values.yaml file as described in [Customized deployment](openliberty_customized_deploy.md). Since the database contains all the Leap applications, once it is connected to Leap 9.3.2 on Open Liberty they will be accessible.

**Note:** Once the database has been connected to version 9.3.2, it will no longer work for Leap 9.3.1.

1.  Leap on Open Liberty works best if the login attribute is set to the 'mail' attribute. If your existing WebSphere deployment is using a different login attribute then some additional steps will need to be taken. All of the Leap users are identified by their login id, if the attribute for that login id changes then when a user authenticates with Leap on Open Liberty for the first time \(using their mail attribute\) they would be seen as a new user and not automatically associated with their previous account. In this case you will need to manually update all the users in the FREEDOM.USERS table \(before allowing them to access the system\), changing their LOGIN\_ID value to the value of their email address.

    The SQL statement looks like the following:

    ``` {#codeblock_ryg_npb_hxb}
    UPDATE FREEDOM.USERS SET LOGIN_ID = '<email of user>' WHERE LOGIN_ID = '<old login attribute>';
    ```

2.  The new Open Liberty image and associated Helm charts for Leap 9.3.2 are not backward-compatible with Leap 9.3.1. Do not use the same values.yaml file for Helm that you may have used with Leap 9.3.1.
3.  Customizations applied through the WebSphere Application Server admin console, may need to be reapplied using snippets of XML according to Open Liberty's configuration technique \(see [https://openliberty.io/docs/latest/reference/config/server-configuration-overview.html](https://openliberty.io/docs/latest/reference/config/server-configuration-overview.html).)\). This additional configuration can be supplied as "overrides" in Leap 9.3.2's Helm charts. For more information, see [Customized deployment](openliberty_customized_deploy.md).
4.  The persistent volumes defined for use with the Leap 9.3.1 container are not the same for Leap 9.3.2. When upgrading to Leap 9.3.2, create new persistent volumes. For more information, see [Prerequisite - Specifying persistant volumes](deploy_container_kubernetes_openliberty.md#section_f4f_24s_gxb).

**Parent topic: **[Kubernetes Helm deployment](kubernetes_helm_deployment.md)

