# Removing users from a role after submission

You can remove a user from a role dynamically using a web service with data or metadata captured from the form. Change an approver or reviewer by creating rules based on the data from the form, or by who submitted the form. 

!!!note
    This is useful for dynamically reassigning role members while keeping the record in the same stage and permissions.

For example, you can create a workflow application with rules that enable a task to a different person and remove the original user.

To use the following instructions, you must set user roles, such as “Manager,” to **Open**. For more information about setting roles, see [Application and Security overview](se_security_toc.md).

1.  Click the **Workflow** tab.

2.  Select a "Submit" stage in the diagram.

3.  Select the **Activities** tab. Click **Add Activity**.

4.  In the **Activity Settings** panel, select **Remove users from role**.

    -   **Remove via Service Call:**

        To remove a user via a service call, select **Call a service**. The Remove users from role\(by Service Call\) window is displayed. If there are no existing activities, the following message appears: "There are no activities. Click here to create one."

        1.  Select a service from the list in the **Service** tab. Services in the Service tab are populated by your administrator. To use these instructions, you must use a service that can search for a user’s manager.
        2.  Click the **Inputs** tab. Map form fields to the input parameters of the service. For example, if your application asks for the user’s name:
            1.  Select **Name** from the **Select source:** window.
            2.  Select **Search Name** from the **Select target:** window.
            3.  Click the connector icon located between the two windows. The connected source and target are displayed in the **Assigned Inputs** section of the page.
        3.  Click the Outputs tab. For example, you can map the outputs of the service to the Manager role:
            1.  Select Manager Name from the Select source: window.
            2.  Expand the directory so you see **Member** \> **Members**. Select **Members** from the **Select target**: window.
            3.  Click the connector icon located between the two windows.
        
        The connected source and target appear in the **Assigned Inputs** section. The system removes the manager of the user who created the form from the role and that manager no longer has access to the form.  Follow this action with an activity to [add a user to the role](sub_assigning_a_user.md) to define the delegate.

    -   **Assign By Value in Form:**

        You can also remove users using the **Value in Form** option, such as a Single Line Entry. This option allows for more flexibility in determining what qualifies a user's assigned role. To remove a user from a role using a form field, complete the following steps.

        1.  Follow steps 1-4 in the task above.
        2.  Select **Value in Form**.
        3.  The applicable fields on the form appear in the **Value in Form** dropdown. Select the field that contains the value that represents the user to assign.
        4.  Select the Role from the dropdown for which the user will be removed.

**Parent topic:** [Adding stages to an application](sub_adding_stages_toc.md)

