# Known limitations {#widgets_limitations .concept}

-   **Complex Data**: Widgets that need to store complex data are expected to use a "parsable" `string` value \(ex. `JSON`\). There is no mechanism to handle customized rendering of this value in some parts of the product \(ex. Print View\), or to customize searching/filtering based on the intricacies of the complex value.
-   **Containers**: There is no support for custom container widgets, those being widgets that contain other widgets, such as a collapsible section.
-   **Full Custom Properties**: There is no mechanism to supply 100% custom properties. Properties of the custom widget will be from a set of common prescribed types.
-   **In-line Editing**: There is no mechanism to support the app author in direct in-line editing of a widget's properties on the canvas.
-   **Multilingual Apps**: There is no mechanism \(beyond an app author's custom JavaScript\) to allow app authors to supply property values for an application that is to be used by end-users who speak different languages.
-   **Author-Defined Data Constraints** - There are limited mechanisms for app authors to define data constraints on the values supplied by end-users. Values can be constrained in the UI by the custom widget itself, or by the author's custom JavaScript.

**Parent topic:**[Custom Widget API](customwidgetapi_landing.md)

