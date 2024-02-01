# Using a service to populate form items {#callingaservicefromadropdownmenu .task}

You can use a web service to populate to a Drop Down, Select One, and Select Many form item.

The following instructions describe how to populate a Drop Down, however the same instructions apply for populating the Select One and Select Many form items.

1.  Select **Drop Down** from the Palette and drop it onto your form.

2.  Select the newly added dropdown.

    The Properties side panel opens.

3.  Click the **Events** tab.

4.  From the **Client Side:** list, select an action to associate with the service.

    A window for the web service opens. From this window, you can:

    -   Select a predefined action, such as **Run a Formula**, **Call a Service**, or both.
    -   Insert your own custom code in the **Custom Actions** area.
5.  Select **Call a Service**.

    From this menu, you can:

    -   Select an existing web service from the menu. If you select an existing service from the menu, go to step 9.
    -   Create a web service call by clicking **Add/Edit Service Configuration**. To configure a web service, go to step 6.
6.  Cick **Add/Edit Service Configuration**, to open the **Service Configuration** window.

    -   Enter the URL of your service
    -   Select **Or, select a service** and select a URL from a list of available services
7.  Click the **Inputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

        The connected source and target are shown in the **Assigned Inputs** section of the page.

8.  Click the **Outputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

    The connected source and target are shown in the **Assigned Outputs** section of the page.

9.  Click **OK** to exit the **Service Configuration**.

10. All form item data is stored in database columns. For Drop Down, Select One, Select Many, and Survey items, the data column must be large enough to accommodate the largest value a user can select. The amount of space that is allocated to a database column is based on the larger of either the Storage Size parameter \(50 characters\), or the largest defined static value. As it is possible to pull information from a web service or from JavaScript™ into the previously listed form items, Leap cannot calculate the largest size needed. To set larger database columns, modify the **Saved Value character limit** field to ensure that it is large enough to hold the largest value expected.

11. Change the size of the **Saved Value character limit** field to the required number of characters.


**Parent topic: **[Incorporating web services into your applications](cr_using_apps_as_services_toc.md)

