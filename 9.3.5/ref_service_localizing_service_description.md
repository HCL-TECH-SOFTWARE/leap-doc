# Localizing Service Descriptions {#ref_service_localizing_service_description .reference}

The name and description elements allow you to localize an HCL Leap Service Description in multiple languages using duplicate elements, each with a different xml:lang attribute and contents.

Service Descriptions can be localized in two ways: using the xml:lang attribute, or providing translations in a separate .properties file. However, these approaches can be cumbersome if the Service Description is to be localized into many languages. An alternative is to use the key attribute on the name, and description elements.

The value of the key attribute denotes the key in a Java™ style .properties file that maps the key to the value to display for the name or description element. When the Service Description is loaded, Leap loads the associated .properties files, and uses their contents as the messages to display for the name and description elements.

When a Service Description uses this approach, the .properties files and Service Description must be placed in the same deployment directory. Changes to the .properties files are not automatically reloaded if they are changed. In order to refresh with new strings, the Service Description XML file must be changed or its modification date changed.

Naming the .properties files is important because the Leap looks for .properties files with specific names. The name of the .properties file that contains the default strings, if none are specified for a specific locale, is the same as the base name of the Service Description XML file, but with a .properties extension. For the locale-specific .properties files, the name is similar but includes an underscore followed by a locale specifier after the base name but before the .properties extension.

For example, if the Service Description XML file is CurrencyConvService.xml, then the default .properties file is CurrencyConvService.properties and the French messages are in a file named CurrencyConvService\_fr.properties. For details on locale specifier formats, refer to the documentation of java.util.Locale.

**Parent topic:**[Service Description](ref_service_service_description.md)

