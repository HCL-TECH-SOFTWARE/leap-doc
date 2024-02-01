# Setting rules on pages in an application {#settingrulesonpagesinanapplication .task}

You can set rules that govern how pages are shown or hidden in a form.

Before using the following steps, create an application with two pages.

Rules in the HCL Leap can help you administer a form so different groups of users are asked for different information. You can add multiple Boolean conditions, such as AND, or OR, for each rule. The following example hides form pages from users whose salary does not meet the rule qualification of $30,000. To use the following steps, you must have multiple pages in your form.

1.  On Page 1 of your form, add a **Currency** item to your form and title it **Salary**.

2.  Click the **Rules** button on Page 2 of your form.

3.  Click **Add Rule**.

4.  In **Perform this action:** make no changes.

    The default value is “hide”.

5.  In **When the following condition is true**, select **Show items on all pages**, and select **Salary**.

6.  Select **Less than** from the menu.

7.  Leave **A fixed value** in the next menu and type **30000** in the blank field.

8.  Click **Apply and Close** to save your changes and close the Rules window.

    The rule is now set so when a user enters less than $30,000, they are not shown the second page of the form.


**Parent topic: **[Creating rules in your application](ru_creating_rules_in_your_form.md)

