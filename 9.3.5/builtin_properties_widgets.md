# Built-In Properties {#builtin_properties_widgets .concept}

Some properties that already exist in the product are general purpose, or, are integral to the proper functioning of a widget.

The following built-in properties are supported for custom widgets:

-   `'required'`: for data widgets, allows the app author to ensure that a value is collected. Requiredness will be enforced beyond the UI; the integrity of the data will be enforced when it is submitted to the server.
-   `'title'`: this is used in various contexts to allow for editing and display of the name of a widget instance.
-   `'seenInOverview'`: allows the app author to decide if the widget's data should be displayed in the *View Data* page.
-   `'range'`: this adds a Range with minimum and maximum properties to the property panel and allows an app author to specify minimum and maximum value. This property can be used with widgets with datatype of number, time, date and timestamp.
-   `'format'`: this adds a Format property to the property panel and allows an app author to specify a format for the string. This property can be used by widgets with datatype of string only.

Example:

``` {#codeblock_ngp_vcn_jyb}
const myWidgetDefinition = {
    ...
    builtInProperties : [{ id: 'required'}, {id: 'title'}, {id: 'seenInOverview', defaultValue: true}],
    ...
}
```

**Note:** All widgets will be implicitly given an `ID` property. The default value of this property will be auto-incrementing unique value based on the last substring of the widget definition's id. For example, a widget with an id of `'example.YesNo'` will result in a default ID of '`F_YesNo1'.` Similar to Leap's built-in widgets, the app author is free to alter the ID to suit their needs.

**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

