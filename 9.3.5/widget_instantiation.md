# Widget Instantiation {#widget_instantiation .concept}

The widget `instantiate()` function is called when an instance of the custom widget needs to be created. The function is expected to return an `object` that allows Leap to interact with the instantiated widget.

`instantiate()` is called with the following arguments:

-   `context`: an `object` containing useful meta-data, including:
    -   `locale`: the locale of current page. This is useful for displaying messages in the correct language or for dealing with locale preferences \(ex. number formatting\).
    -   `mode`: one of `'design'` \(authoring\), `'preview'` \(previewing\), or `'run'` \(running app\). The widget's behaviour may need to be tailored based on the context, for example disabling some behaviours in `'design'` mode.
-   `domNode`: the parent DOM node into which the widget's DOM must be placed. The custom widget code must not manipulate the parent node or anything outside of it.
-   `initialProps`: these will be the initial set of property values as chosen by the app author.
-   `eventManager`: for triggering events. For example, `eventManager.fireEvent('onChange')`.

The returned `object` is expected to supply the following functions:

-   `getValue()`: required for data widgets.
-   `setValue(value)`: required for data widgets.
-   `setProperty(propName, propValue)`: required for all widgets.
-   `getDisplayTitle()`: \(optional\) for display widget's title in various parts of the UI.
-   `setDisabled(isDisabled)`: \(optional\) to tailor the widget's behaviour when disabled and enabled.
-   `setErrorMessage(errorMessage)`: \(optional\) for the widget to report validation errors. `errorMessage` will be `null` if the data is valid.
-   `setRequired(isRequired)`: \(optional\) to tailor the widget's behaviour when the data is required, or not required.
-   `getOptions()`: \(optional\) see [Widgets with Options](widgets_options.md).
-   `validateValue(value)`: \(optional\) - see [Validation](widget_validation.md).
-   `getJSAPIFacade()`: \(optional\) returns an object that supplies additional custom functions that will be available to app authors to use in their custom JavaScript. Special care must be taken to ensure that app authors have a limited range of possibilities and cannot take over the whole page with their custom JavaScript. When Leap's secure sandbox mode is enabled \(`secureJS=true`\), an author's custom JavaScript cannot access any variables prefixed with a double-underscore.

The widget creator is free to decide how they want to code and manage the widget instance internally.

**Parent topic:**[Custom Widget API](customwidgetapi_landing.md)

