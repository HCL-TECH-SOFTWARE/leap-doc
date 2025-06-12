# Development process { #ser_setup_development_environment .task}

The HCL Leap runs within an OSGi framework environment. Code that extends the Leap needs to be packaged within OSGi bundles to run. Any Java™ development environment can be used to create custom bundles, but using the Eclipse IDE built-in OSGi tooling is recommended to minimize effort and errors.

To extend HCL Leap functionality, follow these instructions for creating and packaging custom code as OSGi bundles.


1. Gather Leap JAR files

    Use the following script, or a similar script, to extract appropriate .jar files from the Leap .ear file. If you use the following script, update the variables to match your system.

    The extracted JAR files are placed in the `%EXTRACT\_DIR%\Leap_bundles\` directory.

    **Windows™**:
      ```bat
      SET EXTRACT_DIR=C:\temp\Leap_jars_extracted
      SET JAVA_BIN=C:\java-sdk-80-win\bin
      SET LEAP_DOWNLOAD_DIR=C:\Downloads\hcl.leap-9.3.10.23
      SET LEAP_VERSION=9.3.10.23
      SET FSP_VERSION=8.0.1.89
      SET LEAP_EAR=hcl.leap.packaging.ear-9.3.10.23.ear

      mkdir "%EXTRACT_DIR%"
      mkdir "%EXTRACT_DIR%\fsp"
      mkdir "%EXTRACT_DIR%\core"
      mkdir "%EXTRACT_DIR%\Leap_bundles"

      copy "%LEAP_DOWNLOAD_DIR%\%LEAP_EAR%" "%EXTRACT_DIR%"
      cd "%EXTRACT_DIR%"
      "%JAVA_BIN%\jar" xvf %LEAP_EAR%
      "%JAVA_BIN%\jar" xvf builder.war

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

    **Linux**: 
      ```bash
      #!/bin/bash

      EXTRACT_DIR="/tmp/Leap_jars_extracted"
      JAVA_BIN="/opt/java-sdk-80-linux/bin"
      LEAP_DOWNLOAD_DIR="/tmp/hcl.leap-9.3.10.23"
      LEAP_VERSION="9.3.10.23"
      FSP_VERSION="8.0.1.89"
      LEAP_EAR=hcl.leap.packaging.ear-9.3.10.23.ear

      mkdir -p "$EXTRACT_DIR/fsp"
      mkdir -p "$EXTRACT_DIR/core"
      mkdir -p "$EXTRACT_DIR/Leap_bundles"

      cp "$LEAP_DOWNLOAD_DIR/$LEAP_EAR" "$EXTRACT_DIR/"
      cd "$EXTRACT_DIR"
      "$JAVA_BIN/jar" xvf $LEAP_EAR
      "$JAVA_BIN/jar" xvf builder.war

      cp "WEB-INF/lib/ibm.nitro.packaging.onejar.fsp-$LEAP_VERSION.jar" "$EXTRACT_DIR/fsp/"
      cp "WEB-INF/lib/ibm.nitro.packaging.onejar.core-$LEAP_VERSION.jar" "$EXTRACT_DIR/core/"

      cd "$EXTRACT_DIR/fsp"
      "$JAVA_BIN/jar" xvf "ibm.nitro.packaging.onejar.fsp-$LEAP_VERSION.jar"
      "$JAVA_BIN/jar" xvf FSPJARS.jar
      cp ibm.fsp.core.service.framework-"$FSP_VERSION".jar ../Leap_bundles/

      cd "$EXTRACT_DIR/core"
      "$JAVA_BIN/jar" xvf "ibm.nitro.packaging.onejar.core-$LEAP_VERSION.jar"
      "$JAVA_BIN/jar" xvf FSPBUNDLES.jar
      cp ibm.nitro.services-"$LEAP_VERSION".jar ../Leap_bundles/
      ```

2. Create a **Plug-in Project**

    In the Eclipse IDE, an OSGi bundle is also referred to as a plug-in. Start a new **Plug-in Project** to create an OSGi bundle:

    1.  Select **File** \> **New** \> **Project...** \> **Plug-in Development** \> **Plug-in Project**.
    2.  In the **Target Platform** section, select **an OSGi framework:**, and select **Equinox**.

    !!!note
        Code should be compiled to 1.8 level of Java to work with the 1.8 JVM of IBM WebSphere Application server or the Leap image.

3. Add Leap Jars to the Build Path

    To compile your custom bundle against the Leap jars extracted in Step 1, add them to the build path by changing the **Target Platform** that your plug-in builds against:

      1.  Select **Window** \> **Preferences** \> **Plug-in Development** \> **Target Platform**.
      2.  Select **Running Platform \(Active\)** \> **Edit** \> **Locations** \> **Add...** \> ****.
      3.  Enter the complete path of the Leap\_bundles directory from Step 1.
      4.  Select **Finish**.

4. Implement any interfaces and supporting files as needed.

    Refer to other documents and JavaDocs.

5. Add OSGi constructs to you project

    Create a `META-INF/MANIFEST.MF` file in your project. It will needs specific entries to make it an OSGi bundle.  

    For example:  
    *MANIFEST.MF*
    ```
    Manifest-Version: 1.0
    Build-Jdk-Spec: 1.8
    Bundle-ManifestVersion: 2
    Bundle-Name: MyBundle
    Bundle-SymbolicName: hcl.leap.sample.MyBundle
    Bundle-Vendor: My Company
    Bundle-Version: 0.9.0.0
    Import-Package: com.ibm.form.nitro.service
    Service-Component: OSGI-INF/*.xml
    ```

    Declare the implementation as an OSGi service by using OSGI's declarative service capabilities.  
    For example: 

    *MyFooBarService.xml*
    ```xml
    <scr:component
      xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.osgi.org/xmlns/scr/v1.1.0 https://docs.osgi.org/xmlns/scr/v1.1.0/scr.xsd"
      configuration-policy="optional" 
      enabled="true"
      name="hcl.leap.sample.MyFooBarService">
    <implementation class="hcl.leap.sample.MyFooBarService" />
    <service>
      <provide interface="com.ibm.form.nitro.service.IFooBarService" />
    </service>
    </scr:component>
    ```

6. Package your bundle

    Package your code as a .jar file.

    The typical structure for an OSGi bundle is shown here:

      ```
      /
        META-INF/
          MANIFEST.MF
        OSGI-INF/
          MyService1.xml
          MyService2.xml
        com/
          mycompany/
            services/
              hclLeap
                MyService1.class
                MyService2.class
      ```

    If you are using the Eclipse IDE, you can package your bundle with the **Export** feature:

      1.  Make sure the build.properties file for the project, which is created automatically for a Plug-in Project, includes all the resources you want included in your bundle. For example, make sure the OSGI-INF directory and its contents are included.
      2.  Right-click your Plug-in project.
      3.  Select **Export** \> **Plug-in Development** \> **Deployable plug-ins and fragments**.
      4.  Select your Plug-in project.
      5.  Specify an output directory.
      6.  Click **Finish**.

7. Deploy your bundle

    1. **IBM WebSphere® Application Server deployment**
    
        On the Leap server, put the exported .jar file in one the following directories or in a subdirectory of one of the following directories:

        - Windows™:
          `[any drive]:\HCL\Leap\extensions\`

        - Non-Windows:
          `/opt/HCL/Leap/extensions/`

        Important notes on directories:

        -   If the extensions directory does not exist, then the Leap server must be restarted after the directory is created.
        -   `/opt/HCL/Leap/` is not case sensitive.

    2. **Kubernetes deployment**

        Refer to [Deploy custom extensions](helm_deploy_custom_extension.md) for more information.
  
8. Debugging

    1. Attaching a debugger

        Start the server in debug mode to be able to attach a debugger and step through your own code.

        1. **IBM WebSphere® Application Server Server deployment** 
      
            Refer to IBM WebSphere® Application Server documentation for enabling debug mode

        2. **Kubernetes deployment**
      
            To start the Leap container in debug mode, add the following to your values.yaml:

            ```yaml
            # Environment variables 
              environment:
                pod:
                leap:
                  - name: "LEAP_DEBUG"
                    value: "debug"
            ```
            If you want the JVM to wait for you to attach your debugger to it:
      
            ```yaml
            # Environment variables 
              environment:
                pod:
                leap:
                  - name: "LEAP_DEBUG"
                    value: "debug"
                  - name: "WLP_DEBUG_SUSPEND"
                    value: "y"
            ```
            You will need expose port 7777 of the container to attach a debugger to it. 
            For example, in a development environment you could simply enable port forwarding:

            ```bash
            kubectl port-forward statefulset/hcl-leap-9310-leap 7777:7777
            ```

    2. Debug Logging

        You can enable debug logging or finer logging for the com.ibm.form.nitro.service.services package and other packages to get more information from the Leap code.

          1. **IBM WebSphere® Application Server Server deployment**

              Refer to IBM WebSphere® Application Server documentation for more details on changing log levels.

          2. **Kubernetes deployment**

              Refer to [Changing the log level](helm_changing_log_level.md) for more information.
            !!!note
                Do not run a production system in debug mode or with debug logging enabled. Enabling these options degrades performance.


**Parent topic:** [Extending](extending_toc.md)

