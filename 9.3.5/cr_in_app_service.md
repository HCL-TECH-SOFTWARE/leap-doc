# Adding and configuring a service {#task_kgx_11y_mv .task}

The following instructions describe how to add and configure a service so you can map it within your application.

These instructions provide a general overview of adding and configuring services. They are used whenever you want to add a service to your application.

1.  Click "Add/Edit Service Configuration"

2.  The Service Configuration window opens.

    -   Enter the URL of your service
    -   **Or, select a service** to select a service from a list.
3.  To specify options for the URL, click the Properties icon located to the right of **URL** field.

    Use the **Service Details** dialog to configure how Leap should call the service.

    -   You can add details to the URL in the **URL** field.
    -   Specify the HTTP method for the service
    -   Make URL parameters and segments available for input mapping by selecting **Assignable**. The display name specified is used in the input mapping interface.

        -   URL parameters are query parameters within a URL. The first parameter follows the question mark in the URL. Additional parameters follow an ampersand. For example: https://server.com?this=1&that=2, where **this** is the first parameter, and **that** is the second parameter.

            When you make a parameter assignable, the parameter value is replaced at runtime. In the example https://server.com?this=1&that=2, if **this** is assignable, the value of **this** is replaced with the mapped input value from the form. For example:https://server.com?this=AAAAA&that=2, where **AAAAA** is the value from the form.

        -   URL segments are path elements within a URL. For example https://server.com/resources/identifier, where **resources** is the first segment, and **identifier** is the second segment.

            When you make a segment assignable, the segment is replaced at runtime. In the example https://server.com/resources/identifier, assigning **identifier** a value of 1234 results in a URL that reads: https://server.com/resources/1234.

        **Note:** To add or remove URL parameters or segments, you must modify the URL and tab out of the **URL** field.

    -   Specify authentication options in the **Authentication** section.
    -   If you want to add request headers, expand the **Request header** section and click **Add a required request header**. You can also make request headers assignable for input mapping.
    -   In the Sample Response JSON section, you can **Fetch** a sample JSON response, or insert your own. Elements in the provided JSON are automatically added as assignable outputs in the **Outputs** mapping tab. When you click **Fetch**, the **Fetch a response** window opens. You can modify the URL as required to connect to the service. Click **Submit** to fetch the response.

        **Note:** For **Post** and **Put** HTTP methods, you can enter Sample Request JSON. Elements in the provided JSON are automatically added as assignable inputs in the **Inputs** mapping tab.

    -   If you want to add response headers, expand the **Response header** section and click **Add a required response header**. Response headers are automatically assignable for output mapping.
4.  When you have finished making configuration changes click **OK**.

5.  Click the **Inputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

        The connected source and target are shown in the **Assigned Inputs** section of the page.

    **Note:** If you need to make changes to the service, or configure service details, click the Properties icon located to the right of URL.

6.  Click the **Outputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

    The connected source and target are displayed in the **Assigned Outputs** section of the page.

7.  Click **OK** to exit the **Service Configuration** window.


**Parent topic:**[Incorporating web services into your applications](cr_using_apps_as_services_toc.md)

