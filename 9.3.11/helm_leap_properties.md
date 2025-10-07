# Leap properties { #helm_leap_properties .concept }

!!!note
      The following properties must be added: 
      - **[ibm.nitro.SetupAll.setupStatus](co_configuration_properties.md#setupallsetupstatus)=start**
      - **[ibm.nitro.NitroConfig.loginIdIsEmail](co_configuration_properties.md#loginidisemail)=true**
      - **[ibm.nitro.NitroConfig.userLookup](co_configuration_properties.md#userlookup)=false**
      - **[ibm.nitro.NitroConfig.userGroups](co_configuration_properties.md#usergroups)=false**  
      
      If this does not suit your organizational needs, contact HCL Support for a possible workaround.

Below is an example snippet of setting leap-specific properties:

```yaml
configuration:
   leap:
      . . .
     leapProperties: | 
        ibm.nitro.SetupAll.setupStatus = start
        ibm.nitro.InfoEntryPoint.dailyInfo = <div>Welcome to <b>HCL Leap {{currentVersion}}</b> in Kubernetes!</div> 
        ibm.nitro.NitroConfig.serverURI=http://myleapserver.example.com
        ibm.nitro.NitroConfig.loginIdIsEmail = true
        ibm.nitro.NitroConfig.userLookup=false
        ibm.nitro.NitroConfig.userGroups=false
```

For more information, see [Configuration properties](co_configuration_properties.md).

**Parent topic:** [Preparation](helm_preparation.md)

