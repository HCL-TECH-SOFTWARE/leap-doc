# Adding workflow Stages to a form {#addingworkflowtoaform .learningContent}

Leap uses Stages to add workflow to your form. Workflow describes various lifecycle steps that are associated with the form. Defining multiple connected Stages creates the workflow, where each stage defines its own form behavior, access rights, and navigation steps. In this tutorial, define the workflow steps that are required for the approval of the form.

A Stage describes:

-   The behavior of the form while it is in a stage, including what portions of the form are visible or read only.
-   The flow of the form, determining navigation between stages. For example, a form goes to a manager for general expense approval, but to another manager if the amount of the expense exceeds a predefined amount.
-   Who has access to the form while the form is in that stage.

By default, each form has a Start and a Submitted stage. The Start stage is the beginning of the workflow, and describes a form that has not been completed or submitted by the user. After a form leaves the Start stage, it can never return to the Start stage. The Submitted stage describes a form that has reached the next part of the workflow. You may add other stages to your workflow to fit your use case.

In this lesson, learn how to:

-   Go to the Workflow tab.
-   Add new stages and modify various stage properties.
-   Make form items read-only in a specific stage.
-   Make form pages read-only and hidden in specific stages.
-   Set navigation between stages to create a workflow.

Estimated time required to complete this module: 20 minutes

## Adding stages to your form {#lesson21}

The workflow for this form is summarized as follows: The user accesses the form in the Start stage. When the user submits the form, it goes to the Awaiting Approval stage, where an approver can either accept or reject the Expense Report. If the reviewer accepts the Expense Report, the form goes to the Accepted stage. If the reviewer rejects the Expense Report, the form goes to the Approval Request stage so the submitter can make corrections and resubmit.

1.  Click the Workflow tab.

    The view is made of the diagram canvas and the properties side panel.

2.  In the Start stage, the user who enters data into the form does not need to see the Approval page. To ensure that the user cannot find their way to that page, hide it from view. Click the Visibility button at the top of the screen, then in the side panel, click the Hide icon for the Approval page.

    ![Graphic displaying the Edit Properties, Hide, and Read-Only icons.](graphics/hide_and_read_only_icons.jpg)

    The Approval page is hidden from view when the form user first submits the form.

    **Note:** The hidden or read-only status applies to a form item in a particular stage. If you add another stage, the hidden or read-only status does not carry forward to the new stage.

3.  The user does not need to see the page navigation buttons to the Approval page. Hide them by clicking the Expenses page.

    1.  Go to the page navigation buttons. In the properties side panel, click the eye icon to hide in this stage.

        The page navigation buttons are now hidden from view when the user submits the form. The page navigation buttons are only hidden in this stage.

4.  Create a stage to add the Approval page that is created in the previous section. Click the Add a new stage icon while the Start stage is in focus.

    A new stage is inserted after the Start stage and before the Submitted stage.

5.  Click the label “Stage *n*” to change the name of the stage to “Approval Request”.

    This stage allows users to open the form again and edit the expense report if it is rejected by an approver.

6.  Click on the Visibility button at the top of the screen. Set the Approval page to read-only by clicking on the lock icon with the “Approval Request” stage selected.

    You want the user to see the comments that are written by the reviewer, but do not want the user to be able to modify the choices that are set by the reviewer.

7.  Add another stage, and title it Awaiting Approval.

    The form progresses to this stage after the user submits it.

    1.  In the Visibility View, set the Basic Information and Expenses pages to be read-only.

    2.  At the end of the form, Submit and Cancel buttons are automatically added. Click the Add Action icon, and add another Submit button.

8.  Click the Submit action on the diagram, or with the stage selected click the Edit Properties icon for the Submit button. Change the title to Accept.

    So users know whether their Expense Reports were accepted or rejected, send them an email.

    1.  In the Action Completion Message: field, set it to read You have approved the submitter’s expense report. They are notified by email of the approval.

        This message is shown to the approver every time they accept an expense report.

    2.  Click the Activities tab.

    3.  In the Activities section, click “+ Add Activity” to create one. Select “Send an email” as the Activity Type.

    4.  From the To: menu, click “Insert” and select Email.

    5.  In the Subject entry field, type Your Expense Report was accepted.

    6.  In the Contents of the Email: box, write your email. For example, enter: Thank you for submitting your expense report. It was accepted, and payment will be made shortly. To view the approved report, click the following link:

    7.  To insert a link to the form, click the Insert item: menu that is located in the text editor tools. From the menu, select Link to this form.

    8.  The changes are automatically saved. Click the X or click outside the settings panel to close it.

9.  When the reviewer approves the expense report, the user receives an email at the address they provided on the Basic Information page. Now configure the second Submit button to use if the approver rejects the submitted form.
10. With the stage selected, click the label for the second Submit button and change the title to “Decline”.

    1.  In the Action Completion Message: field set it to read: You have rejected the submitter’s request. They are notified to correct errors and resubmit the Expense Report.

    2.  In the Next Stage: menu, select Approval Request.

        If the Expense Report is rejected, the user can reopen it to correct errors. Now set the stage to send an email to notify the submitter of the rejection.

    3.  In the Activities section, click “+ Add Activity” to create one. Select “Send an email” as the Activity Type.

    4.  From the To: menu, click “Insert” and select Email.

    5.  In the Subject: entry field, type Your Expense Report was rejected.

    6.  In the Contents of the Email: box, write your email. For example, enter: Your submitted expense report was rejected.Click the following link to review the report, make corrections and resubmit:

    7.  To insert a link to the form, click the Insert item: menu in the text editor tools. From the menu, select Link to this form.

    8.  The changes are automatically saved. Click the X or click outside the settings panel to close it.

11. Go to the Approval Request stage. Set which stage the button activates by clicking on the submit button on the diagram and in the Properties side panel change the Next Stage to “Awaiting Approval”.

12. When the approver receives the form to review, it is best if the submitted information is read-only. This way the reviewer cannot modify any data that the user submitted. When you set pages and form items as read-only in the Start stage, and must do so again in Approval Request stage.
13. In the Visibility view, click the “Approval Request” stage and then click the lock icon next to the page to make it read-only in this stage.

14. Now that the Approval Request stage is created, you must modify the Start stage so the form is routed to the Approval Request stage.
15. Click the Start stage. Click the Edit Properties icon for Submit.

    1.  Change the Action Completion Message: to read: Your data was submitted and will be reviewed soon.

    2.  Change the Next Stage to “Approval Request”.

16. Save your application.

    When the user completes and submits the form, it is sent to an approver for review.


When the user submits the form, it goes from the Start to the Awaiting Approval stage. If the approver accepts, the form is sent to the Submitted stage, and the workflow is complete. If the approver rejects the Expense Report, it is sent to the Approval Request stage so the user can fix errors and resubmit.

If the approver rejects the Expense Report, the form is sent to this stage so the user can open the form, change it, and resubmit. When the user submits the corrected form, it goes to the Awaiting Approval stage again.

## Optional: Applying conditional workflow to the form {#applyingconditionallogictoastage}

There is a rule on the form that states any expense reimbursement must be approved by a reviewer. However, you can create a stage in the workflow to request special approval for amounts larger than $2000.

1.  In the Workflow tab, create a stage and title it Special Approval.

    1.  Create a second Submit button.

    2.  Click label for the first Submit button to change the title to Accept.

    3.  Set the Next stage: to Awaiting Approval.

        When the special request is approved, the form is sent to the main approver for review.

    4.  Click label for the second Submit button to change the title to Reject.

    5.  Set the Next stage: to Approval Request.

2.  Click “+ Add Action” in the properties side panel or hover over the stage card in the diagram and click the “+” to create a second submit button.

3.  Click the Edit Properties icon for new Submit button.

    1.  Click the Visibility button. Click on the Actions section where the submit buttons are shown.

    2.  Click the Rules icon for the new submit button.

    3.  Click Add Rule.

    4.  In the When this is true: section, click the menu. Select Show items on all pages.

    5.  Click the same menu again and select Expense Amount to Approve.

    6.  In the next menu, select Less than or equals.

    7.  In the blank field for A fixed value, enter $2000.

    8.  In the Perform this action section, select the second Submit button in the start stage.

        A number is appended to the action button ID when there are more than one instance of the same class.

        For example, the ID for this item is Start - Submit - S\_Submit2, but a different number can be appended if you create and delete more than one Submit button.

    9.  Select Hide from the next menu.

    10. Click Apply.

4.  The rule states that the button is hidden if the expense amount claimed is less than $2000. Now set the opposite rule on the first submit button.

5.  Click Add Rule.

    1.  In the When this is true: section, click the menu. Select Show items on all pages.

    2.  Click the same menu again and select Expense Amount to Approve.

    3.  In the next menu, select Greater than or equals.

    4.  In the blank field for A fixed value, enter $2000.

    5.  In the Perform this action section, select the second Submit button in the start stage.

        A number is appended to the action button ID when there are more than one instance of the same class.

        For example, the ID for this item is Start - Submit - S\_Submit, but a number can be appended to that string if you create and delete more than one Submit button.

    6.  Select Hide from the next menu.

    7.  Click Apply and Close.

6.  When the user opens the form, only one Submit button is visible. When the user clicks the Submit button, the form is sent to the appropriate stage based on the total amount of the expense.

    **Note:** Submit buttons are not available in Preview mode. You must deploy the form to test the rules that are set on the button. If you deploy the form, there is no difference in the appearance of the form because both buttons have the same name. When you click View Data, you see the additional workflow steps that are required for the form.

    The conditional workflow is set. In the next section, add access control to each stage so the Approval Request stage is set to one set of reviewers, while the Special Approval stage is set to another set of reviewers.

7.  Save the form.


**Parent topic: **[Adding tables and workflow elements to a HCL Leap form](tut_roles_and_stages_OV.md)

