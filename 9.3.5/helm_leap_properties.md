# Leap properties {#helm_leap_properties .concept}

The leapProperties parameter can be used to add or modify properties to Leap.

**Note:** The property ibm.nitro.NitroConfig.loginIdIsEmail must be added and set to true.

Below is an example snippet of setting leap-specific properties:

``` {#codeblock_hd4_vjt_gxb}
configuration:
   leap:
     leapProperties: | 
        ibm.nitro.InfoEntryPoint.dailyInfo = <div>Welcome to <b>HCL Leap 9.3.2</b> in Kubernetes!</div> 
        ibm.nitro.NitroConfig.serverURI=http://myleapserver.example.com
        ibm.nitro.NitroConfig.loginIdIsEmail = true
```

For more information, see [Configuration properties](co_configuration_properties.md).

**Parent topic: **[Preparation](helm_preparation.md)

