# Adding a Service Catalog {#ser_add_service_catalog .task}

A Service Catalog serves two purposes. First, a Service Catalog is a programmatic mechanism to dynamically provide Service Descriptions to HCL Leap instead of using static XML files. Second, a Service Catalog is linked to a Service Catalog Group and provides a mechanism to assign Service Descriptions to a specific Service Catalog Group.

A Service Catalog is implemented in much the same manner as a Service Catalog Group. You first create an implementation of the IServiceCatalog interface. The recommended approach is to extend the AbstractServiceCatalog class. Your implementation and supporting files are then packaged into an OSGi bundle and deployed to the extensions directory on the Leap server. Refer to [Setting up your development environment](ser_setup_development_environment.md) before using the following instructions.

1.  Create a Java class

    The following example of a custom Service Catalog provides the description of a single sample service called Hello Service. This service has one input parameter and one output parameter. This custom Service Catalog is linked with the sample Service Catalog Group described in the [Service Catalog Group](ser_add_service_catalog_group.md) help topic by returning the com.mycompany.services.MyServiceCatalogGroup.id from the getGroupId\(\) method. The Hello Service service is started when My Services is selected by the application designer from the **Service Catalog** dropdown in the **Service Configuration** dialog.

    ```
    package com.mycompany.services;
    
    import com.ibm.form.nitro.service.model.*;
    import com.ibm.form.nitro.service.services.*;
    import java.util.*;
    
    public class MyServiceCatalog
        extends AbstractServiceCatalog
        implements IServiceCatalog
    {
        private Collection<IServiceDescription> mServiceDescriptions = null;
        
        public String getGroupId()
        {
            return "com.mycompany.services.MyServiceCatalogGroup.id";
        }
        
        public void setServiceDescriptionBuilderFactory(IServiceDescriptionBuilderFactory pServiceDescriptionBuilderFactory)
        {
            if (this.mServiceDescriptions == null)
            {
                this.mServiceDescriptions = new ArrayList<IServiceDescription>();
                try
                {
                    IServiceDescriptionBuilder builder1 =
                        pServiceDescriptionBuilderFactory.newDescriptionBuilder();
                    builder1.setId("com.mycompany.services.Hello").setDefaultLocale(Locale.ENGLISH);
                    builder1.setName(Locale.ENGLISH, "Hello Service");
                    builder1.setDescription(Locale.ENGLISH, "This service says 'Hello' to a given person");
                    builder1.setTransportId("com.mycompany.services.HelloServiceTransport.id");
    
                    // service inputs
                    IServiceBindingBuilder inboundBindingBuilder = builder1.newBindingBuilder();
                    IServiceParameterBuilder inParamBuilder1 = inboundBindingBuilder.newParameterBuilder();
                    inParamBuilder1.setName(Locale.ENGLISH, "Person");
                    inParamBuilder1.setDescription(Locale.ENGLISH, "The person to say 'Hello' to");
                    inParamBuilder1.setId("person").setMandatory(true).setType(ServiceParameterType.STRING);
                    inboundBindingBuilder.addParameter(inParamBuilder1.getServiceParameter());
                    builder1.setInbound(inboundBindingBuilder.getServiceBinding());
    
                    // service outputs
                    IServiceBindingBuilder outboundBindingBuilder = builder1.newBindingBuilder();
                    IServiceParameterBuilder outParamBuilder1 = outboundBindingBuilder.newParameterBuilder();
                    outParamBuilder1.setName(Locale.ENGLISH, "Greeting");
                    outParamBuilder1.setDescription(Locale.ENGLISH, "The 'Hello' greeting");
                    outParamBuilder1.setId("greeting").setType(ServiceParameterType.STRING);
                    outboundBindingBuilder.addParameter(outParamBuilder1.getServiceParameter());
                    builder1.setOutbound(outboundBindingBuilder.getServiceBinding());
    
                    IServiceDescription serviceDescription1 = builder1.getServiceDescription();
                    this.mServiceDescriptions.add(serviceDescription1);
                }
                catch (ServiceException ex)
                {
                    throw new RuntimeException(ex);
                }
            }
        }
    
        public Collection<IServiceDescription> getServiceDescriptions(IServiceManager pManager, IOrg pOrg,
                                                                      IUser pUser, String pFilterCatalog,
                                                                      String pFilterStatus, String pFilterText,
                                                                      boolean pFilterIncludesDesc,
                                                                      Locale pFilterLocale)
        {
            this.filterServiceDescriptions(pManager, this.mServiceDescriptions, pFilterStatus, pFilterText,
                                           pFilterIncludesDesc, pFilterLocale);
            return Collections.unmodifiableCollection(this.mServiceDescriptions);
        }
    
        public IServiceDescription getServiceDescription(IServiceManager pManager, IOrg pOrg, IUser pUser,
                                                         String pServiceDescriptionId)
        {
            for (IServiceDescription description : this.mServiceDescriptions)
            {
                if (description.getId().equals(pServiceDescriptionId))
                    return description;
            }
            return null;
        }
    }
    ```

    In this example, an IserviceDescriptionBuilder is used to build up a Service Description programmatically. However, IserviceDescriptionBuilder also provides methods to parse Service Descriptions from XML files.

2.  Create an OSGi Service Description

    You must create an .xml file to declare your Java class as an OSGi service. For example, create a MyServiceCatalog.xml file with the following content:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <scr:component xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0" 
     configuration-policy="optional" 
     enabled="true"  
     immediate="true" 
     name="com.mycompany.services.MyServiceCatalog.service">
       <implementation class="com.mycompany.services.MyServiceCatalog" />  
       <reference bind="setServiceDescriptionBuilderFactory" 
         cardinality="1..1" 
         interface="com.ibm.form.nitro.service.services.IServiceDescriptionBuilderFactory"
         name="ServiceDescriptionBuilderFactory" 
         policy="static"/>
       <service>
         <provide interface="com.ibm.form.nitro.service.services.IServiceCatalog"/>
       </service>
    </scr:component>
    ```

    For the class attribute of the implementation element, use the fully qualified name of the Java class you created in [Step 1](ser_add_service_catalog.md#add_service_catalog_step_1). Ensure that the name attribute of the component element is unique. Although not required, you can make the name attribute the same as the fully qualified name of the Java class that you created in Step 1.

    Notice the inclusion of the <reference\> element in this example. This ensures that your custom Service Catalog has access to an IServiceDescriptionBuilderFactory for programmatically building up Service Descriptions.

3.  Create a MANIFEST.MF file

    Create a MANIFEST.MF file similar to [Step 3 in the Service Catalog Group](ser_add_service_catalog_group.md) help topic. Multiple OSGi services can be packaged within the same OSGi bundle. Therefore, the same MANIFEST.MF file can be used for a custom Service Catalog Group and a custom Service Catalog.

4.  Deploy the Service Catalog.

    Deployment of your Service Catalog is similar to [Step 4 in the Service Catalog Group](ser_add_service_catalog_group.md) help topic.

    Multiple OSGi services can be packaged within the same OSGi bundle, so the same .jar file can be used for your custom Service Catalog Group and custom Service Catalog.


**Parent topic: **[Providing Groups of Dynamic Services](ser_provide_groups_of_dynamic_services.md)

