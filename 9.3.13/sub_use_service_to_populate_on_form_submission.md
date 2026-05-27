# Populating information upon form submission using a web service { #sendingamessagetoauserusingaservice .task}

Web services can perform many functions, such as sending data to other forms or applications. The following instructions describe how to use a web service to add information to a form automatically after it is submitted.

{{fullProductName}} can look up user information for you using a web service call. For example, you can connect a manager with a user submitted form using an intranet directory search.

1.  Click the **Workflow** tab.

2.  Click the **Add Activity** button in a submit button on the diagram, or select the button and click **Add Activity** in the side panel.

3.  **In Activity Settings**, select **Call a Service**.

    For this example, select the directory for your company intranet.

4.  Click **Configure Service**.

5.  Click the **Inputs** tab. Map the form fields to the input parameters of the service.

    1.  Select **Current User** from the **Select source:** window.

    2.  Select **Search Name** from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

    The connected source and target are displayed in the **Assigned Inputs** section of the page.

6.  Click the **Outputs** tab. Map the outputs of the service to the Manager role.

    1.  Select **Manager Name** from the **Select source:** window.

    2.  In the**Select target:** window, choose a form item from the list.

    3.  Click the connector icon located between the two windows to link the source and the target.

    After the source and target are linked, they appear in the **Assigned Outputs** area of the screen.

7.  Click **OK** to exit the **Call a Service** window.

    When the user clicks **Submit**, {{shortProductName}} calls a service to populate the manager’s name into the selected form item.


**Parent topic:** [Adding stages to an application](sub_adding_stages_toc.md)

