# Adding custom data integrity logic

{{fullProductName}} includes built-in server-side validation and sanitization of incoming data, detecting issues such as missing required fields or values that violate constraints like data type, length, format, or range.

{{shortProductName}} can be extended with additional business logic that is meaningful to your organization.

To extend HCL Leap with custom business logic tailored to your organization, review its built-in server-side validation capabilities and the [Development process](ser_setup_development_environment.md) before starting. Then follow the instructions below: 



## General Usage

1. Implement the `IDataIntegrityService` interface

    See [Javadoc](./javadoc/index.html) for more information.

    *MyValidator.java*
    ```java
    package hcl.leap.sample;

    import com.ibm.form.nitro.service.data.integrity.*;

    public class MyValidator
      implements
      IDataIntegrityService
    {

      @Override
      public void processIncomingData(IMetaData metadata, List<IDataField> dataFields, LifecycleStep step, Logger logger)
          throws DataIntegrityException
      {
        // implementation here
      }
    }
    ```


2. Add OSGi constructs

    *MANIFEST.MF*
    ```manifest.mf
    Manifest-Version: 1.0
    Build-Jdk-Spec: 1.8
    Bundle-ManifestVersion: 2
    Bundle-Name: My impls of IDataIntegrityService
    Bundle-SymbolicName: hcl.leap.sample.dataIntegrity
    Bundle-Vendor: My Company
    Bundle-Version: 0.9.0.0
    Import-Package: com.ibm.form.nitro.service.data.integrity
    Service-Component: OSGI-INF/*.xml
    ```

    *MyFooBarService.xml*
    ```xml
    <scr:component
      xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.osgi.org/xmlns/scr/v1.1.0 https://docs.osgi.org/xmlns/scr/v1.1.0/scr.xsd"
      configuration-policy="optional" 
      enabled="true"
      name="hcl.leap.sample.MyValidator">
      <implementation class="hcl.leap.sample.MyValidator" />
      <service>
        <provide interface="com.ibm.form.nitro.service.data.integrity.IDataIntegrityService" />
      </service>
    </scr:component>
    ```

    !!!note 
        Multiple implementations of IDataIntegrityService are permitted, either in separate OSGi bundles or within a single OSGi bundle. The order in which implementations are invoked is non-deterministic. 

## Aligning with custom widgets

Custom validation rules can work in lock-step with custom widgets. For details on creating custom widgets for {{shortProductName}}, see [Custom Widget API](customwidgetapi_landing.md).

Specifically, a custom widget can define a `customDataType` property which can be utilized by custom validation code. 

For example, if a custom widget is defined as:

*YesNoWidget.js*
```javascript
acme.yesNoWidget = {
  id: "acme.YesNo",
  version: "1.0.0",
  ...
  datatype: {
    type: "string",
    length: 3,
    customDataType: "yes-no"
  },
  ...
}
```
A custom validation rule can then enforce that the value received for this field type is either "yes", "no", or empty. For example:
```java
public class YesNoValidator
  implements
  IDataIntegrityService
{
  @Override
  public void processIncomingData(IMetaData metadata, List<IDataField> dataFields, LifecycleStep step, Logger logger)
      throws DataIntegrityException
  {       
    for (IDataField dataField : dataFields)
    {
      if ("yes-no".equals(dataField.getCustomDataType()))
      {
        if (dataField.getValue() != null && !((String) dataField.getValue()).isEmpty())
        {
          String val = (String) dataField.getValue();
          if (!"yes".equals(val) && !"no".equals(val))
          {
            String msg = String
                .format("Yes/No field \"%s\" must have a value of \"yes\" or \"no\". The received value is \"%s\"",
                        dataField.getId(), val);
            throw new DataIntegrityException(msg);
          }
        }
      }
    }
  }
}
```

## Custom sanitization

Your organization might require additional data sanitization before the information is stored in the Leap database or used in downstream processing.
  
A custom integrity service can modify field values. For example:
```java
public class StringSanitizer
    implements
    IDataIntegrityService
{

  @Override
  public void processIncomingData(IMetaData metadata, List<IDataField> dataFields, LifecycleStep step, Logger logger)
      throws DataIntegrityException
  {
    for (IDataField dataField : dataFields)
    {
      if (dataField.getDataType().equals("string"))
      {
        String currentValue = (String) dataField.getValue();
        if (currentValue != null)
        {
            String newValue = sanitize(currentValue);
            dataField.setValue(newValue);
        }
      }
    }
  }

  /**
   * Custom sanitization
   * 
   * @param input
   * @return
   */
  private String sanitize(String input)
  {
    // insert custom sanization code here
  }
}
```

**Parent topic:** [Extending](extending_toc.md)