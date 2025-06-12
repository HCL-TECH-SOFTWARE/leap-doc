# Data Widgets vs Display Widgets { #datawidgets_displaywidgets .concept }

Some widgets are for collecting data \(ie. "data widgets"\) and others are presentational in nature \(ie. "display widgets"\).

A data widget is required to:

-   Declare a `datatype` property \(described below\).
-   Provide `setValue()` and `getValue()` functions.
-   Publish an `onChange` event when its value is changed by the user. This will trigger a call to the widget's `getValue()` function, and `validateValue()` function if supplied.

Some display widgets are still expected to trigger events \(for example, `onClick`\), which can be used by the app author to invoke an action, by custom JavaScript or other techniques.

**Parent topic:** [Custom Widget API](customwidgetapi_landing.md)

