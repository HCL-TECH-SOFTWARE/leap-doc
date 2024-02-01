# Setting rules on form items {#makingawidgetconditionalinanapplication .task}

You can set rules that govern how form items appear in a form.

The following steps describe how to add form items to your application and to create a sample rule on a form item. The rule will show a field if a user selects a specific input. For example, if the employee is full-time, fields appear requesting additional information. If the employee is not full-time, the fields remain hidden.

1.  Add a **Select One** item to your form.

2.  Click the item’s title to change it to “Are you a full-time worker?”. Click the check box beside **Required** to indicate that the user must fill in this form item to submit the form.

3.  In the properties side panel, under **Options**:

    1.  Change the Displayed Value of the first row to **Yes**.

    2.  Click the **Add option** button to insert a second option row.

    3.  Change the Displayed Value of the second row to **No**.

4.  Add a **Single Line entry** to the form. Click the box to the left of the title.

    A red asterisk appears to indicate the item is mandatory and must be completed for the user to submit the form.

5.  Change the title to “Where is your work site located?”

6.  Click the **Edit Rules** icon for “Where is your work site located?”

    The Rules window opens.

    1.  Click **Add Rule**.

        If you intend to have several rules on a form, you should give each rule a unique name so it is easy to find. For this example, leave the name as Rule 1

    2.  In the **Perform this action:** section, the name of the form item is automatically inserted as the item on which you want to set the rule. Select **Show** from the action menu.

    3.  In the **When the following condition is true:** section, select **Are you a full time employee?** from the first menu, and then **Equals** in the second menu.

    4.  To the right of **A fixed value**, select the **Yes** radio button.

    5.  Click **Apply and Close**.

7.  Add a **Single Line entry** to the form. Click the box to the left of the title.

    A red asterisk appears to indicate the item is mandatory and must be completed for the user to submit the form.

8.  Change the title to “What is your job title?”

9.  Click the **Edit Rules** icon for “Where is your work site located?”

    The Rules window opens.

    1.  Click **Add Rule**.

        Note that this rule is named Rule 2.

    2.  In the **Perform this action:** section, the name of the form item is automatically inserted. Select **Show** from the action menu.

    3.  In the **When the following condition is true:** menu, select **Are you a full time employee?** from the first menu, and then **Equals** in the second menu.

    4.  To the right of **A fixed value**, select the **Yes** radio button.

    5.  Click **Apply and Close**

    The rule is set so that if the user states they are a full-time worker, the additional fields appear and request information on the work location and job title.


**Parent topic: **[Creating rules in your application](ru_creating_rules_in_your_form.md)

