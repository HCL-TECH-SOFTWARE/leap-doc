# Setting rules on Stages {#settingrulesonstageactions .task}

You can direct the workflow of an application by setting rules on buttons within Stages.

In a stage, you can build two approval buttons that appear identical, but send the user to a different page or stage. Which button appears to the user is determined by information the user enters, and the rules set on the form. To use the following instructions you must have stages created for your form. The instructions describe how to use rules and stages to create a button that provides multiple functionality for form designers away from the visual display to a user. The Submit button requests different information from users based on whether they make more or less than $30,000.

1.  Click the **Workflow** tab.

2.  Click the Visibility button at the top of the screen, select the desired stage \(i.e. Start\), and click anywhere in the section at the bottom of the page where the submit buttons are shown.

3.  Click the Edit Rules icon for the desired submit button.

4.  Open the Rules window for the **Submit** button of the Start stage.

5.  Click **Add Rule**.

6.  In the Perform this action section, leave the defaults of **Start - Submit** in the first menu, and **Hide** in the second menu.

7.  In When the following condition is true, select **Show items on all pages**, then select**Salary**.

8.  Set the operation to **Less than**.

9.  Leave **A fixed value** in the next menu and type **30000** in the blank field.

10. Click **Apply and Close** to save your changes and close the Rules window.

    The rule is now set so users will not see the Submit button if they makes less that $30,000.

11. Click the **Add Action** icon to add another Submit button.

    A duplicate Submit button appears.

12. Follow steps 2 through 9, but set the operation to **Greater than or equals**.


The form developer sees two different buttons that perform two different actions. When you preview the form, only one Submit button appears. You can now create stages and form pages specific to the user’s salary.

**Parent topic:**[Creating rules in your application](ru_creating_rules_in_your_form.md)

