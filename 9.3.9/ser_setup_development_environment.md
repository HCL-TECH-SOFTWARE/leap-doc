# Setting up your development environment { #ser_setup_development_environment .task}

The HCL Leap runs within an OSGi framework environment. Code that extends the Leap needs to be packaged within OSGi bundles to run. Any Java™ development environment can be used to create custom bundles, but using the Eclipse IDE built-in OSGi tooling is recommended to minimize effort and errors.

1.  Gather Leap JAR files

    Use the following script, or a similar script, to extract appropriate .jar files from the Leap .ear file. If you use the following script, update the variables to match your system.

    The extracted JAR files are placed in the %EXTRACT\_DIR%\\Leap\_bundles\\ directory.

    ```bat
    SET EXTRACT_DIR=C:\temp\Builder_extract
    SET JAVA_BIN=C:\hcl-java-sdk-60-win-i386\bin
    SET LEAP_INSTALL_DIR=C:\Program Files\HCL\Leap Server\8.0\Leap
    SET LEAP_VERSION=8.0.0.1013
    SET FSP_VERSION=8.0.0.494
    
    mkdir "%EXTRACT_DIR%"
    mkdir "%EXTRACT_DIR%\fsp"
    mkdir "%EXTRACT_DIR%\core"
    mkdir "%EXTRACT_DIR%\Leap_bundles"
    
    copy "%LEAP_INSTALL_DIR%\deploy\hcl-leap.ear" "%EXTRACT_DIR%"
    cd "%EXTRACT_DIR%"
    "%JAVA_BIN%\jar" xvf hcl-leap.ear
    "%JAVA_BIN%\jar" xvf leap.war
    
    copy "WEB-INF\lib\ibm.nitro.packaging.onejar.fsp-%LEAP_VERSION%.jar" "%EXTRACT_DIR%\fsp"
    copy "WEB-INF\lib\ibm.nitro.packaging.onejar.core-%LEAP_VERSION%.jar" "%EXTRACT_DIR%\core"
    
    cd "%EXTRACT_DIR%\fsp"
    "%JAVA_BIN%\jar" xvf ibm.nitro.packaging.onejar.fsp-%LEAP_VERSION%.jar
    "%JAVA_BIN%\jar" xvf FSPJARS.jar
    copy ibm.fsp.core.service.framework-%FSP_VERSION%.jar ..\Leap_bundles
    
    cd "%EXTRACT_DIR%\core"
    "%JAVA_BIN%\jar" xvf ibm.nitro.packaging.onejar.core-%LEAP_VERSION%.jar
    "%JAVA_BIN%\jar" xvf FSPBUNDLES.jar
    copy ibm.nitro.services-%LEAP_VERSION%.jar ..\Leap_bundles
    ```

2.  Create a **Plug-in Project**

    In the Eclipse IDE, an OSGi bundle is also referred to as a plug-in. Start a new **Plug-in Project** to create an OSGi bundle:

    1.  Select **File** \> **New** \> **Project...** \> **Plug-in Development** \> **Plug-in Project**.
    2.  In the **Target Platform**section, select **an OSGi framework:**, and select **Equinox**.
3.  Add Leap Jars to the Build Path

    To compile your custom bundle against the Leapjars extracted in Step 1, add them to the build path by changing the **Target Platform** that your plug-in builds against:

    1.  Select **Window** \> **Preferences** \> **Plug-in Development** \> **Target Platform**.
    2.  Select **Running Platform \(Active\)** \> **Edit** \> **Locations** \> **Add...** \> ****.
    3.  Enter the complete path of the Leap\_bundles directory from Step 1.
    4.  Select **Finish**.
4.  Implement any classes and supporting files as needed.

    Refer to other documents and JavaDocs.

5.  Package your Plug-In and Deploy

    1.  Package your code as a .jar file.

        The typical structure for an OSGi bundle is shown here:

        ```
        /
           META-INF/
              MANIFEST.MF
           OSGI-INF/
              Service1.xml
              Service2.xml
           com/
              mycompany/
                 services/
                    hclLeap
                       Service1.class
                       Service2.class
               
        ```

        If you are using the Eclipse IDE, you can package your bundle with the **Export** feature:

        1.  Make sure the build.properties file for the project, which is created automatically for a Plug-in Project, includes all the resources you want included in your bundle. For example, make sure the OSGI-INF directory and its contents are included.
        2.  Right-click your Plug-in project.
        3.  Select **Export** \> **Plug-in Development** \> **Deployable plug-ins and fragments**.
        4.  Select your Plug-in project.
        5.  Specify an output directory.
        6.  Click **Finish**.
    2.  On the Leap server, put the exported .jar file in one the following directories or in a subdirectory of one of the following directories:

        -   Windows™:

            any drive:\\HCL\\Leap\\extensions\\

        -   Non-Windows:

            /opt/HCL/Leap/extensions/

        Important notes on directories:

        -   If the extensions directory does not exist, then the Leap server must be restarted after the directory is created.
        -   /opt/HCL/Leap/ is not case sensitive.
6.  Debugging

    1.  If you start the Leap server in debug mode, you can attach your debugger to the running JVM and step through your own code.

    2.  Also, you can enable debug logging or finer logging for the com.ibm.form.nitro.service.services package to get more information from the Leap code.

    Refer to the documentation for WebSphere® Application Server for more details.

    Do not run a production system in debug mode or with debug logging enabled. Enabling these options degrades performance.


**Parent topic:** [Adding services](services_toc.md)

