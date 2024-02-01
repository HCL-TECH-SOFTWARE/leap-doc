# Validation {#widget_validation .concept}

Some intrinsic validation will be done according to the `type` and `constraints` declared in the widget's `datatype` property; however, it might be necessary for a widget to supply its own custom validation logic.

This can be done by supplying a `validateValue()` function, which returns one of the following values:

-   `null` : indicates the value is valid
-   An error message : the returned error message will be displayed to the app user in some contexts \(ex. when attempting to go the next page\).

It is responsibility of the custom widget to render itself appropriately based on its state of validity.

**Note:** The widget's `setErrorMessage` function will be triggered whenever the validity changes, due to contraints on the `datatype` or custom validation from the `validateValue()` function.

**Note:** Any additional validation provided by the custom widget via a `validateValue()` function will not be enforced on the server; however, it will prevent the form from being submitted by the user in the browser.

**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

