# Embedding items in an iframe {#embeddingitemsinaniframe .reference}

You can use iFrames to embed charts and applications in a web page.

## Embedded Chart Rendering { .section}

To embed the summary charts in a web page, use the following URL as a guide. Change the `host`, `port`, `app_uid` and `form_id` variables to suit your host, port, application ID and form ID.

```
<iframe  src="http://host:port/apps/secure/org/app/app\_uid/results/index.html?form=form\_id&narrow=true&hideLabels=true&legend=true"></iframe>
```

The parameters in this URL are:

hideLabels=true
:   Hides labels on pie charts.

narrow=true
:   Renders charts in narrow mode, which is suitable for charts embedded in narrow spaces. In narrow mode, pie charts render at a size to fit the available space and bar charts are hidden. Narrow mode works best in combination with hideLabels=true and legend=true.

    **Note:** Narrow mode is automatically engaged when the available space for charts is less than 500 pixels wide regardless of the narrow URL parameter.

legend=true
:   Displays a legend with the pie chart. Use in combination with narrow=true and hideLabels=true.

When the charts are embedded, the banner is hidden and there are simple messages when no charts are available.

## Embedded Form Rendering { .section}

To embed a form in a web page, use the following URL as a guide. Change the `host`, `port`, `app_uid` and `form_id` variables to suit your host, port, application ID and form ID.

```
<iframe style="width:600px;height:600px"  src="http://host:port/apps/secure/org/app/app\_uid/launch/index.html?form=form\_id&width=600px">
</iframe>
```

The parameters in this URL are:

width=value
:   Value can be a percentage or a fixed number of pixels.

    **Note:** URL encoding is required for the `%` character. It should be represented as `%25`. For example `99%` would become `&width=99%25`

When the forms are embedded, the banner is hidden and when form is shown, the first item does not initially grab focus

**Parent topic: **[Reference](reference_toc.md)

