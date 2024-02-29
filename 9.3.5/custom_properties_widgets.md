# Custom Properties {#custom_properties_widgets .concept}

The custom widget can define an array of custom properties for the app author to modify.

Each property is an `object` with the following attributes:

-   `id`: \(required\) uniquely identifies this property for this widget.
-   `label`: \(required\) the property's label.
-   `propType`: \(required\) one of:
    -   `'string'`: rendered as a textbox.
    -   `'string-multiline'`: rendered as a textarea.
    -   `'enum'`: rendered as a dropdown. must be accompanied by a `values` attribute \(see example below\).
    -   `'boolean'`: rendered as a checkbox.
    -   `'number'` : rendered as a number input, for any number.
    -   `'integer'` : rendered as a number input, for integers only.
    -   `'customOptions'` : see the following listed items.
-   `values`: required if `propType` is `'enum'` \(see the following example\).
-   `defaultValue` : \(optional\) the property's default value.
-   `constraints` : \(optional\)
    -   `min`: \(optional\) minimum allowed property value for numbers.
    -   `max`: \(optional\) maximum allowed property value for numbers.

Example:

```javascript
const myWidgetDefintion = {
  ...
  properties: [
    ...
    {
      id: 'messageType',
      label:  'Message Type',
      propType: 'enum',
      values: [{title: 'Information', value: 'info'}, {title: 'Warning', value: 'warn'}, {title: 'Error', value: 'error'}],
      defaultValue: 'info'
    },
    ... 
  ],
  ...
};
```

**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

