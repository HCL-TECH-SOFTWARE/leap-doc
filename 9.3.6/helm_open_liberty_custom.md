# Open Liberty server customizations 

The configOverrideFiles parameter allows configuration snippets to be passed to the Leap server.

The snippets are merged into the Open Liberty server.xml. After making changes to the .yaml, apply them using the `helm upgrade ...` command. Changes are picked up by Open Liberty and applied at runtime - this does not require a restart.

**Note:** The name of the customization \(myCustomOverride1 in the following snippet\) can be any string, but you may want it to be descriptive of what is being provided.

``` {#codeblock_t2s_pts_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      myCustomOverride1: | 
        <server description="leapServer"> 
          <basicregistry id="leapRegistry" realm="basicRealm"> 
            <user name="newuser1" password="passw0rd" 
          </basicRegistry> 
        </server>
```
There are several configuration changes that leverage this mechanism: [SMTP](helm_configure_smtp.md), [Database](helm_configure_db.md), [LDAP](helm_configure_ldap.md).

**Parent topic:** [Preparation](helm_preparation.md)

