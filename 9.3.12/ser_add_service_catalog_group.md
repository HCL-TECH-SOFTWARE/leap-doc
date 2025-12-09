# Adding a Service Catalog Group { #ser_provide_groups_of_dynamic_services .task}

A Service Catalog Group provides a way to group web services in HCL Leap.

Refer to [Development process](ser_setup_development_environment.md) before starting.

A new Service Catalog Group can be added toLeap by creating and deploying an appropriate OSGi .jar bundle.

To the application designer, Service Catalog Groups are listed in the **Service Catalog** dropdown in the Leap **Service Configuration** dialog. This dropdown allows the application designer to filter services by the Service Catalog Group to which they belong. By default, there are two predefined groups: General and HCL Leap Applications. Providing a new implementation of a Service Catalog Group creates a group as an option in the **Service Catalog** dropdown. Services can be added to a particular Service Catalog Group by implementing a Service Catalog that belongs to that group.

1.  Create a Java class

    Create a Java class that implements the com.ibm.form.nitro.service.services.IServiceCatalogGroup interface to return a unique group identifier and a readable group name. The following example adds the **My Services** group to the Leap.

    ```java
    package com.mycompany.services;
    
    import com.ibm.form.nitro.service.services.IServiceCatalogGroup;
    import com.ibm.form.platform.service.framework.i18n.LocaleUtils;
    import java.util.Locale;
    
    public class MyServiceCatalogGroup
        implements IServiceCatalogGroup
    {
    
        public String getGroupId()
        {
            return "com.company.services.MyServiceCatalogGroup.id"; 
        }
    
        public String getGroupName()
        {
            Locale requestLocale = LocaleUtils.getRequestLocale();
            /* use request locale to determine a translated group name */
            return "My Services";
        }
    }
    ```

    In this example, the locale used by the user can be retrieved by using com.ibm.form.platform.service.framework.i18n.LocaleUtils.getRequestLocale\(. If you are using the Eclipse IDE, its Externalize Strings wizard can extract strings for your OSGi bundle.

2.  Create an OSGi Service Description

    You must create an .xml file to declare your Java class as an OSGi service. For example, create a MyServiceCatalogGroup.xml file with the following content:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <scr:component xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0" 
     configuration-policy="optional" 
     enabled="true"  
     immediate="true" 
     name="com.mycompany.services.MyServiceCatalogGroup.service">
       <implementation class="com.mycompany.services.MyServiceCatalogGroup" />  
    	<service>
         <provide interface="com.ibm.form.nitro.service.services.IServiceCatalogGroup"/>
       </service>
    </scr:component>
    ```

    For the class attribute of the implementation element, use the fully qualified name of the Java class you created in Step 1. Ensure that the name attribute of the component element is unique. Although not required, you can make the name attribute the same as the fully qualified name of the Java class that you created in Step 1.

3.  Create a MANIFEST.MF file

    Sample content:

    ```
    Manifest-Version: 1.0
    Bundle-ManifestVersion: 2
    Bundle-Name: My Company Services
    Bundle-SymbolicName: com.mycompany.services
    Bundle-Version: 1.0.0.b1
    Bundle-Vendor: My Company
    Bundle-RequiredExecutionEnvironment: JavaSE-1.6
    Service-Component: OSGI-INF/*.xml
    Import-Package: com.ibm.form.nitro.service.model,
     com.ibm.form.nitro.service.services,
     com.ibm.form.platform.service.framework.i18n
    ```

4.  Deploy the Service Catalog Group.

    Create a .jar file that contains all the files listed in the previous steps in an OSGi bundle structure. For example:

    ```
    /
       META-INF/
          MANIFEST.MF
       OSGI-INF/
          MyServiceCatalogGroup.xml
       com/
          mycompany/
             services/
                MyServiceCatalogGroup.classn
    ```

    On the Leap server, put the .jar file in one the following directories or in a subdirectory of one of the following directories:

    -   Windows™:

        any drive:\\HCL\\Leap\\extensions\\

    -   Non Windows:

        /opt/HCL/Leap/extensions/

    !!! note
        -   If the extensions directory does not exist, you must restart the Leap server after the directory is created.
        -   /opt/HCL/Leap/ is not case-sensitive.

**Parent topic:** [Providing Groups of Dynamic Services](ser_provide_groups_of_dynamic_services.md)

