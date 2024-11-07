# Configuring the properties file {#configuringthepropertiesfile .concept}

When you install HCL Leap, a file containing sample configuration properties is also installed. You can configure the properties for optimal performance with your system.

To use the provided properties file, you must move it to the extensions folder, then adjust the settings to match your system.

**Note:** In a horizontally clustered environment, the Leap\_config.properties must be configured for each node.

## Define extensions directory in the fsp.properties {#section_xfj_ds5_jzb .section}

1.  Go to **<install location\>**/deploy, and locate Leap\_config.properties.
2.  Copy the file and paste it to:
    -   **Windows** – C:\\HCL\\Leap\\extensions
    -   **Linux**, **AIX** – /opt/HCL/Leap/extensions
3.  Open the Leap\_config.properties file and configure the settings to match your system.

## Customizing the location of the extensions directory {#section_nmd_q4f_zzb .section}

There are two ways to define a customized location for the extensions directory. You can modify the fsp.properties or add a jvm property.

### Using the fsp.properties file

1.  To customize the location of the Leap\_config.properties file, you must edit the fsp.properties file.

2.  Go to the fsp.properties file. The default location of the fsp.properties file is: \\AppServer\\profiles\\AppSrv01\\installedApps\\\\Experience Builder.ear\\builder.war\\WEB-INF\\classes.
3.  Open the properties file in a text editor and add a valid extensions= parameter. For example, extensions = /usr/HCL/Leap/extensions.

### Using a jvm property {#section_fjf_4t5_jzb .section}

Add the option `-Dfsp.extensions.dirs` to the jvm where Leap is deployed. The value is the path\(s\) to the extensions directory.

**AIX**:

``` {#codeblock_vyz_qt5_jzb}
-Dfsp.extensions.dirs=/customFolder/extensions,/customFolder2/extensions
```

**Windows**

``` {#codeblock_ug5_st5_jzb}
-Dfsp.extensions.dirs=c:\customFolder\extensions,c:\customFolder2\extensions
```

## **Validate which directory is loaded** {#section_h25_tt5_jzb .section}

Check the **Leap SystemOut.log**. There is an entry that indicates which directory is recognized and loaded. For example:

``` {#codeblock_omz_wt5_jzb}
[5/21/14 22:51:37:095 PDT] 0000001b IntegratorSta I com.ibm.form.platform.service.startup.IntegratorStartup phase1Start Extensions folder: /usr/HCL/Leap/extensions
```

**Note:** Some configuration properties require a restart of the Leap server. If you do not see your changes applied within a few minutes of modifying the properties file, restart the server.

-   **[Configuration properties](co_configuration_properties.md)**  
The following table contains a list of properties in the HCL Leap Leap\_config.properties file. You can adjust the settings listed in the file, or add your own for a custom configuration.

**Parent topic: **[Configuring](co_config_toc.md)

