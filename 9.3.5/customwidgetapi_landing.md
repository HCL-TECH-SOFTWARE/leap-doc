# Custom Widget API {#customwidgetapi_landing .concept}

This API provides a mechanism to incorporate custom widgets into the HCL Leap product.

## Getting started {#section_m5p_4cn_jyb .section}

**Product Configuration**

Additional resources can be loaded into Leap UI's by adding `ibm.nitro.NitroConfig.runtimeResources` properties to `Leap_config.properties`. These additional resources are expected to include definitions of your custom widgets and any auxiliary styles or libraries that are required to support them.

For example:

``` {#codeblock_isb_pdn_jyb}
ibm.nitro.NitroConfig.runtimeResources.1 = \
  <link rel='stylesheet' type='text/css' media='screen' href='https://mywidgets.example.com/common.css'>; \n\
  <link rel='stylesheet' type='text/css' media='screen' href='https://mywidgets.example.com/MyYesNoWidget.css'>; \n\
  <script src='https://myWidgets.example.com/common.js'></script> \n\
  <script src='https://myWidgets.example.com/MyYesNoWidget.js'></script> \n
```

**Registering a Widget**

As your custom .js is loaded into the page, it is expected to register one or more widget definitions:

``` {#codeblock_gcn_z3n_jyb}
const myWidgetDefinition = {...};
nitro.registerWidget(myWidgetDefintion);
```

Full descriptions and examples are provided in the following topics. The following example is the basic skeleton of a custom widget:

``` {#codeblock_omy_y3n_jyb}
const myWidgetDefinition = {
    id: 'example.YesNo', // uniquely identifies this widget
    version: '2.0.0', // the widget's version
    apiVersion: '1.0.0', // the version of this API
    label: 'Yes/No',
    description: 'Allows user to choose "Yes" or "No"',
    datatype: {
        type: 'string' // must be one of 'string', 'date', 'number', 'boolean', 'time', 'timestamp'
    },
    // for placement in the palette
    category: {
        id: 'example.choice.widgets',
        label: 'Choice Components'
    },
    iconClassName: 'myYesNoIcon', // styling of this class expected in custom .css
    builtInProperties: [...], // use existing properties: 'title', 'required', etc
    properties: [...], // custom properties, of prescribed types

    // called by Leap to initialize widget in the DOM with initial properties, and set-up event handling
    instantiate: function (context, domNode, initialProps, eventManager) {
        return {
             // (optional) for display in various parts of the UI
            getDisplayTitle: function () {
                return ...
            },

            // (required) for Leap to get widget's data value
            getValue: function () {
                return ...
            },

            // (required) for Leap to set widget's data value
            setValue: function (val) {
                ...
            },

            // (optional) for additional validation of value
            validateValue: function (val) {
                // return true, false, or custom error message
            },

            // (required) called when properties change in the authoring environment, or via JavaScript API
            setProperty: function (propName, propValue) {
                ...
            },

            // (optional) method to enable/disable widget
	        setDisabled: function (isDisabled) {
                ...
            },

            // (optional) determines what the author can do with the widget via custom JavaScript
            getJSAPIFacade: function () {
                return {
                    ...
                 };
            }
        };
    }
};
```

-   **[Data Widgets vs Display Widgets](datawidgets_displaywidgets.md)**  
Some widgets are for collecting data \(ie. "data widgets"\) and others are presentational in nature \(ie. "display widgets"\).
-   **[Data Types](datatypes_widgets.md)**  
Data widgets can declare one of the listed data types, each with additional optional constraints.
-   **[Rules](rules_widgets.md)**  
App authors will be able to incorporate custom widgets in rules.
-   **[Built-In Properties](builtin_properties_widgets.md)**  
Some properties that already exist in the product are general purpose, or, are integral to the proper functioning of a widget.
-   **[Custom Properties](custom_properties_widgets.md)**  
The custom widget can define an array of custom properties for the app author to modify.
-   **[Widgets with Options](widgets_options.md)**  
Widgets that allow the end-user to select from a set of options require specific treatment. This includes widgets such as dropdowns, radio groups, or checkbox groups. These options could be hardcoded in the custom widget, or defined by the app author.
-   **[Widget Instantiation](widget_instantiation.md)**  
The widget `instantiate()` function is called when an instance of the custom widget needs to be created. The function is expected to return an `object` that allows Leap to interact with the instantiated widget.
-   **[Validation](widget_validation.md)**  
Some intrinsic validation will be done according to the `type` and `constraints` declared in the widget's `datatype` property; however, it might be necessary for a widget to supply its own custom validation logic.
-   **[Internationalization](widget_internationalization.md)**  
Certain attributes of the widget definition can be displayed to app authors working in different locales. To support multiple languages during authoring, some properties can be specified as "multi-string" objects rather than a plain `string` values.
-   **[Usage of JavaScript API](widget_javaapi.md)**  
Custom widgets can use Leap's JavaScript API to help achieve their objectives.
-   **[Versioning](widget_versioning.md)**  
This topic describes the widget's `version`.
-   **[Upgrading](widget_upgrade.md)**  
The exact techniques for upgrading widgets from one major version to the next has not yet been established.
-   **[Security Considerations](widgets_security.md)**  
This topic describes security considerations for Custom Widget API.
-   **[Incorporating third-party libraries](widgets_thirdpartylibraries.md)**  
This topic describes incorporating third-party libraries.
-   **[Known limitations](widgets_limitations.md)**  

-   **[Examples](widgets_examples.md)**  


**Parent topic:**[Reference](reference_toc.md)

