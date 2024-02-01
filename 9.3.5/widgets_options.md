# Widgets with Options {#widgets_options .concept}

Widgets that allow the end-user to select from a set of options require specific treatment. This includes widgets such as dropdowns, radio groups, or checkbox groups. These options could be hardcoded in the custom widget, or defined by the app author.

## Author-Defined Options {#section_gdf_tfn_jyb .section}

If a widget requires app authors to define their own options, define a property with both `id` and `propType` set to a value of `"customOptions"`.

Example:

``` {#codeblock_w13_vfn_jyb}
const myWidgetDefintion = {
    ...
    properties: [
        {
            id: "customOptions",
            propType: "customOptions",
            label: "Options"
        },
        ...
    ],
    ...
```

**Note:** An id of `'customOptions'` is meaningful to Leap. All other custom property id's are arbitrary.

## Hardcoded Options {#section_rnj_wfn_jyb .section}

If the widget's options are hardcoded, add a `getOptions()` function to your widget.

Example:

``` {#codeblock_xk3_xfn_jyb}
const myWidgetDefintion = {
    ...
    getOptions : function () {
	    return [{title: 'Yes', value: 'yes'}, {title: 'No', value: 'no'}];
    },
    ...
};
```

**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

