# Examples { #widgets_examples .concept}

!!! note
    The 'Acme' examples mentioned here are deployed with {{shortProductName}}.

Each 'Acme' widget requires the Acme_Widgets.css and Acme_common.js, these files only need to be defined once.
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.1=/custom-widgets/samples/acme/Acme_Widgets.css
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.2=/custom-widgets/samples/acme/Acme_common.js
```

## Display Widget Examples

- Navigation Header
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_PageNavHeader_Widget.js
    ```
- [Notification Widget](https://github.com/HCL-TECH-SOFTWARE/leap-custom-widgets/tree/main/samples/notification-widget) (at github.com)


## Data Widget Examples

### Yes/No Widget
    ```    
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_YesNo_Widget.js
    ```
### Boolean Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Boolean_Widget.js
    ```
### Date Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Date_Widget.js
    ```
### Date Time Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_DateTime_Widget.js
    ```
### Decimal Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Decimal_Widget.js
    ```
### Dynamic Select Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Select_Widget_Dynamic.js
    ```
### Email Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Email_Widget.js
    ```
### Number Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Number_Widget.js
    ```
### Radio Group Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_RadioGroup_Widget.js
    ```
### Repeating Section Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Repeating_Section_Widget.js
    ```
### Select Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_Select_Widget.js
    ```
### String Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_String_Widget.js
    ```
### Zip Code Widget
    ```
    {% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.N=/custom-widgets/samples/acme/Acme_ZipCode_Widget.js
    ```

To include all the Acme widgets the configuration would look like:
```
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.1 = <link rel='stylesheet' type='text/css' media='screen' href='/custom-widgets/samples/acme/Acme_Widgets.css' />
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.2 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_common.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.3 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Boolean_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.4 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Number_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.5 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Date_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.6 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Decimal_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.7 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Email_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.8 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_String_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.9 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_RadioGroup_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.10 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_YesNo_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.11 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_ZipCode_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.12 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_DateTime_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.13 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_PageNavHeader_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.14 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Select_Widget.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.15 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Select_Widget_Dynamic.js'></script>
{% if isLeap %}ibm.nitro.NitroConfig.{% endif %}runtimeResources.16 = <script nonce='#!#cspNonce!#!' type='text/javascript' src='/custom-widgets/samples/acme/Acme_Repeating_Section_Widget.js'></script>
```

### [Scribble Signature Widget](https://github.com/HCL-TECH-SOFTWARE/leap-custom-widgets/tree/main/samples/signature-widget)


### [MUI - Star Rating and Switch Widgets](https://github.com/HCL-TECH-SOFTWARE/leap-custom-widgets/tree/main/samples/mui-widgets)


**Parent topic:** [Custom Widget API](customwidgetapi_landing.md)

