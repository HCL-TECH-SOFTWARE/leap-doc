# Assigning users to a role after submission { #assigningausertoaformaftersubmission .task}

You can dynamically assign roles to a form after form submission.

You can assign users to roles dynamically using a web service with data, or metadata captured from the form. Assign an approver or reviewer by creating rules based on the data from the form, or by who submitted the form. For example, you can create a workflow application with rules to determine who can send notification by email. To use the following instructions, you must have user Roles, such as “Manager”, set to **Open**. For more information on setting roles, see [Application and Security overview](se_security_toc.md).

1.  Click the **Workflow** tab.

2.  Select a "Submit" stage in the diagram.

3.  Select the **Activities** tab. Click **Add Activity**.

4.  In the **Activity Settings** panel, select **Assign Users**.

    -   **Assign By Service Call:**

        To assign users via a service call, select **Service Call**. The Assign Users \(by Service Call\) window opens. If there are no existing activities, you see: There are no activities. Click here to create one.

        1.  Select a service from the list in the **Service** tab. Services in the Service tab are populated by your administrator. To use these instructions, you require a service that is able to search for a user’s manager.
        2.  Click the **Inputs** tab. Map form fields to the input parameters of the service. For example, if your application asks for the user’s name:
            1.  Select **Name** from the **Select source:** window.
            2.  Select **Search Name** from the **Select target:** window.
            3.  Click the connector icon located between the two windows. The connected source and target are displayed in the **Assigned Inputs** section of the page.
        3.  Click the Outputs tab. For example, you can map the outputs of the service to the Manager role:
            1.  Select Manager Name from the Select source: window.
            2.  Expand the directory so you see **Member** \> **Members**. Select **Members** from the **Select target**: window.
            3.  Click the connector icon located between the two windows.
        The connected source and target are displayed in the **Assigned Inputs** section of the page. Now, the manager of the user who created the form can approve the form, but no other manager can do so.

    -   **Assign By Value in Form:**

        You can also assign users using the Value in Form option, such as a Single Line Entry. This option allows for more flexibility in determining what qualifies a user's assigned role. To assign a user a role from a form field, complete the following steps.

        1.  Follow steps 1-4 in the task above.
        2.  Select **Value in Form**.
        3.  The applicable fields on the form appear in the "Value in Form" dropdown. Select the field that contains the value that represents the user to assign.
        4.  Select the Role from the dropdown to which the user will be assigned.

**Parent topic:** [Adding stages to an application](sub_adding_stages_toc.md)

