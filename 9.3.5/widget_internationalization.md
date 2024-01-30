# Internationalization {#widget_internationalization .concept}

Certain attributes of the widget definition can be displayed to app authors working in different locales. To support multiple languages during authoring, some properties can be specified as "multi-string" objects rather than a plain `string` values.

For example:

``` {#codeblock_bvb_ygn_jyb}
label: 'Yes/No',
```

can be written as

``` {#codeblock_m4g_2ym_jyb}
  label: {
    "default": 'Yes/No',
    "fr": 'Oui/No',
    "de": 'Ja/Nein'
  },
```

The property names are expected to match the `lang` attribute of the current HTML page. For example, `"fr": 'Oui/No'` matches `<html lang="fr">`.

If there is no match, then the `"default"` property will be used as a fallback.

The following widget attributes are globalizable:

-   `label`
-   `description`
-   `category > label`
-   `properties > (property) > label`
-   `properties > (property) > defaultValue`
-   `properties > (property) > options > (option) > title`

**Parent topic:**[Custom Widget API](customwidgetapi_landing.md)

