# Configuring Leap properties { #configuringleapproperties .concept }

There are several properties that change different aspects of Leap’s behavior. For the complete list of properties, refer to [Configuration properties](co_configuration_properties.md).

How you define the properties depends on the Leap deployment:


- In Kubernetes, properties are defined in the Helm yaml file.


- In WebSphere, properties are defined in a ```Leap_config.properties``` file deployed to the file system.


## Kubernetes Deployment

Refer to [Leap properties](helm_leap_properties.md) for more information on setting properties for Leap running on Kubernetes.


## WebSphere Application Server Deployment

A sample configuration properties file is included in the product package. You can modify these properties to optimize performance for your system.

To use the provided properties file, you must move it to the extensions folder, then adjust the settings to match your system.

!!! note
    In a horizontally clustered environment, the Leap\_config.properties must be configured for each node.

### Define extensions directory

The extensions directory is the location that Leap uses for loading customized properties, service descriptions, and custom extensions.

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

Add the option `-Dfsp.extensions.dirs` to the jvm where Leap is deployed. The value is the path\(s\) to the extensions directory.

**AIX**, **Linux**:

```
-Dfsp.extensions.dirs=/customFolder/extensions,/customFolder2/extensions
```

**Windows**

```
-Dfsp.extensions.dirs=c:/customFolder/extensions,c:/customFolder2/extensions
```

### Deploy properties file

1.  Go to the **directory where you unpacked the Leap zip file**, locate ```Leap\_config.properties``` in the **deploy** folder. If you have a properties file from a previous deployment, use that properties file instead.
2.  Copy the file and paste it to the location you defined above.
3.  Open the ```Leap\_config.properties``` file and configure the settings to match your system.

### Validate which directory is loaded { #section_h25_tt5_jzb .section }

Check the **Leap SystemOut.log**. There is an entry that indicates which directory is recognized and loaded. For example:

```
[5/21/14 22:51:37:095 PDT] 0000001b IntegratorSta I com.ibm.form.platform.service.startup.IntegratorStartup phase1Start Extensions folder: /usr/HCL/Leap/extensions
```

!!! note
    Some configuration properties require a restart of the Leap server. If you do not see your changes applied within a few minutes of modifying the properties file, restart the server.

**Parent topic:** [Configuring](co_config_toc.md)

