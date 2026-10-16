# Defining configuration properties { #configuringleapproperties .concept }

There are several properties that change different aspects of {{shortLeapProductName}} behavior. For the complete list of properties, refer to [Configuration properties](co_configuration_properties.md).

{% if isLeap %}
How you define the properties depends on the {{shortLeapProductName}} deployment:

- In Kubernetes, properties are defined in the Helm yaml file.
- In WebSphere, properties are defined in a ```Leap_config.properties``` file deployed to the file system.

## Kubernetes Deployment
{% endif %}
Refer to [Define configuration properties](helm_leap_properties.md) for more information on setting properties for {{shortLeapProductName}}{% if isLeap %} running on Kubernetes{% endif %}.

{% if isLeap %}
## WebSphere Application Server Deployment

A sample configuration properties file is included in the product package. You can modify these properties to optimize performance for your system.

To use the provided properties file, you must move it to the extensions folder, then adjust the settings to match your system.

!!! note
    In a horizontally clustered environment, the Leap\_config.properties must be configured for each node.

### Define extensions directory

The extensions directory is the location that {{shortLeapProductName}} uses for loading customized properties, service descriptions, and custom extensions.

There are 3 methods for defining the extensions directory:

- use default directory
- fsp.properties
- JVM property

#### Default

It is not mandatory to customize the location of the extensions directory.  The default directory is

- **Windows** – C:/HCL/Leap/extensions
- **Linux**, **AIX** – /opt/HCL/Leap/extensions


#### Define using fsp.properties { #section_xfj_ds5_jzb .section }

1.  To define the location of the ```Leap\_config.properties``` file, edit the ```fsp.properties``` file.

2.  Go to the ```fsp.properties``` file. The default location of the ```fsp.properties``` file is: 

```
{WebSphere Installation Directory}/AppServer/profiles/AppSrv01/installedApps/{cellName}/HCL Leap.ear/builder.war/WEB-INF/classes
```

3.  Open the properties file in a text editor and add a valid extensions= parameter. For example:

```
extensions=/usr/HCL/Leap/extensions
```

### Define using a jvm property { #section_fjf_4t5_jzb .section }

Add the option `-Dfsp.extensions.dirs` to the jvm where {{shortLeapProductName}} is deployed. The value is the path\(s\) to the extensions directory.

**AIX**, **Linux**:

```
-Dfsp.extensions.dirs=/customFolder/extensions,/customFolder2/extensions
```

**Windows**

```
-Dfsp.extensions.dirs=c:/customFolder/extensions,c:/customFolder2/extensions
```

### Deploy properties file

1.  Go to the **directory where you unpacked the {{shortLeapProductName}} zip file**, locate ```Leap\_config.properties``` in the **deploy** folder. If you have a properties file from a previous deployment, use that properties file instead.
2.  Copy the file and paste it to the location you defined above.
3.  Open the ```Leap\_config.properties``` file and configure the settings to match your system.

!!! note
    Only one file with an extension of `.properties` should exist in the extensions folder. Having more than one file in the same directory with the `.properties` extension will lead to confusion about which properties file is actually being loaded.  Check the server logs after restarting Leap, to confirm which file is being loaded.

### Validate which directory is loaded { #section_h25_tt5_jzb .section }

Check the **{{shortLeapProductName}} SystemOut.log**. There is an entry that indicates which directory is recognized and loaded. For example:

```
[5/21/14 22:51:37:095 PDT] 0000001b IntegratorSta I com.ibm.form.platform.service.startup.IntegratorStartup phase1Start Extensions folder: /usr/HCL/Leap/extensions
```

!!! note
    Some configuration properties require a restart of the {{shortLeapProductName}} server. If you do not see your changes applied within a few minutes of modifying the properties file, restart the server.
{% endif %}

**Parent topic:** [Configuring](co_config_toc.md)

