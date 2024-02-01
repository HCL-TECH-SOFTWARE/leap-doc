# Security Considerations {#widgets_security .concept}

This topic describes security considerations for Custom Widget API.

1.  It is the responsibility of the widget creator to avoid script injection attacks by ensuring that values are sanitized or escaped properly before placing them into the DOM. In general, the widget creator is responsible for following secure engineering practices.
2.  The custom widget code has full access to the page, but it should not call product functions, manipulate the product's JavaScript values, or interact with the product's DOM nodes in any way that is not prescribed by this API. Doing so could jeporadize the security of the product and break your custom widgets in future product releases.
3.  As stated above, special care must be taken when supplying a `getJSAPIFacade()` function to expose additional widget capabilities for app authors to leverage in their custom JavaScript. These functions should provide tightly constrained interactions with the custom widget, with no possibility for script injection or access to the widget's internal objects or its DOM, or those of the product. The "facade" naming is a reminder that the app author's code should only get references to values and objects that are necessary and "safe".
4.  It is the responsibility of widget creators and Leap administrators to ensure that only trusted stable resources are loaded into Leap's pages. The specified additional resources will be loaded directly into the user's browser \(by injecting them as-written into the `<head>` of the page\). There will be no additional vetting or sanitizing of resources by Leap. It is not recommended for a customer to rely on resources that they do not tightly control \(ie. avoid usage of libraries from a 3rd-party CDN\).
5.  Strict CSP support requires a special `nonce='#!#cspNonce!#!'` attribute on `<script>` tags. For example:

    ``` {#codeblock_xw1_ssm_jyb}
    ibm.nitro.NitroConfig.runtimeResources.4 = <script nonce='#!#cspNonce!#!'
            src='https://myWidgets.example.com/MyYesNoWidget.js'></script>
    ```


**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

