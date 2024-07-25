# Adding tables to forms {#addingworkflowtoaform .learningContent}

Adding tables to your form is a useful way to gather information from users in a contained space. You can specify exactly what information you want the user to enter by selecting form items to use as the table headings. The user can add as many rows into the table as required to submit their data, but the table is contained within a predefined size on the page.

In this lesson, learn how to:

-   Add a Table to the form.
-   Add form items as column headings in the table.
-   Add page navigation buttons to the form.

Estimated time required to complete this module: 20 minutes

## Add a table to the Expenses page {#lesson11}

For this tutorial, add a table for the user to submit a list of expenses.

1.  In the Manage tab, open the Expense Report application by clicking Edit.

    The Outline view displays all the forms and pages within an application. You can change the default names of forms and pages to more specific names. You can also move between form pages by clicking them in the Outline view.

2.  In the Outline view, click the Expenses page.

    The blank Expenses page is displayed.

3.  Add a section to the Expenses page, and extend it to span all columns.

    1.  In the properties side panel, change the title of the section to “Itemized Expenses”.

    2.  Click the Display title bar check box so the title is displayed on the form.

4.  Expand the Specialized section of the Palette and add a Table to the form.

5.  To set the table headers, click the “here” link in the information window.

    A new child page is created for the table that stores the form items that are used as table column headers. A grid with one column and one row is displayed.

6.  Add the following form items to the Table page, either vertically, or horizontally.

    When the user enters data into the table, a window opens and displays the column headings as a list. If there are more column headings than space in the window, scroll bars are displayed to the user. You must decide whether you want users to scroll vertically, or horizontally, then build the column headers in that direction. Whether you build the list in the child page, the column headers are displayed horizontally in the table on the form.

    1.  Expand the Common section of the Palette.

    2.  Add a Date. Set the Hint to Date the expense was incurred.

    3.  Add a Dropdown. In the properties side panel: set the title to “Type” and set the hint to “Type of expense”. Click the Edit Properties icon. Then click the Edit button in the Options: section. Enter the following options into the displayed value column, create row with the Add option icon after each: Air Travel, Car rental, Food, Hotel, Postage, Other

    4.  Add a Single Line Entry. Set the Title to Description. Set the Width to Medium in the Properties side panel.

    5.  Add a Currency. Set the Title to Amount. Set the Width to Short.

7.  Make all form items in the Table required by clicking the required box for each item.

8.  In the Outline view, click the Expenses page to continue building the form.

    On the Expenses page notice that the table headings are displayed horizontally.

    1.  Expand the table to cover both columns in the grid.

    2.  In the Properties side panel set the title of the table to “Your Expenses”.

    3.  Enter a Hint.

        For example: Enter each itemized expense in the table.

9.  Save and preview the form.

    The Preview icon is located with the Save icon.

10. When the preview is displayed, click Next to get to the Expenses page. In the validation error message window, click Continue. The error is displayed because you are leaving the first page of the form without entering data into mandatory fields. The table is then displayed with no entries. Click the Add a new entry icon to add test information to the table. A window is displayed containing the column headers displayed vertically, and they all fit in the window. If the table headers were entered onto the Table page horizontally, the user must scroll to see all table fields.

    Close the preview form to return to building the form.

11. Set a formula on the table so the total of the submitted expenses is displayed in a separate Currency area. This total is supplied to the reviewer on the Approval page you create next. On the Expenses page, add a Currency form item beneath the table.

    1.  Click the newly added currency field to reveal the properties side panel.

    2.  Change the Title to Total Expense Amount.

    3.  Click the Formula tab.

    4.  From the Choose the function used to set the value of this item: select Table Sum.

    5.  Click the Column entry field.

        A window opens for you to select a form item. Expand the tree until Amount is available.

    6.  The formula is set.

12. Add Page Navigation buttons to the end of the form.

13. Save and preview the form. If you enter test data into the table, the numbers that are entered in the Amount columns are automatically added and displayed in the Total Expense Amount.


## Adding an approval page with more logic to the form {#approvalpagewithadditionallogic}

The following steps describe how to create an approval page where a supervisor approves or denies the expense report. A rule is set so that if the reviewer denies the expense claim, they can provide a reason why the expense was denied.

First, create a page in the form to use as the Approval page. It displays the Total Expense Amount from the Expenses page to the approver.

1.  In the Outline view, click the Add icon to add another page to the form.

2.  Change the name of the page to Approval.

3.  Add a Section and span the section across the two columns.

4.  In the properties side panel, change the title to “Expense Approval”, and select the Display title bar option.

5.  Add a Single Line Entry form item to the section. Change the name to Approver’s Name.

6.  Add a Currency form item next. Change the title to Expense Amount to Approve

7.  Click the currency form item to reveal the properties side panel.

    The following substeps describe how to pull the total from the Total Expense Amount on the Expenses page into the Expense Amount to Approve form item. A rule is then set to make the amount read-only to the approver if its value is greater than zero. This way, the approver can see the amount, but cannot change it.

    1.  In the properties side panel, select the Formula tab.

    2.  From the Choose the function used to set the value of this item menu, select Assign.

    3.  Select Total Expense Amount from the list of form items available.

    4.  Click the Edit Rules icon and add a rule.

    5.  In the When the following condition is true section, select Expense Amount to Approve from the first menu.

    6.  Select Greater than from the second menu.

    7.  Leave “A fixed value” selected and add the number 0 to the empty field.

    8.  In the Perform this action section, select Expense Amount to Approve from the first menu.

    9.  Select Disable from the second menu.

    10. Click Apply and Close.

8.  Add a Select One item in the section.

    1.  Click the newly added select one to reveal the properties side panel.

    2.  Set the Title to Do you approve this expense?

    3.  Click the check box to make this item Required.

    4.  Edit the Options: to Approve and Decline.

    5.  Set the Choice Layout to Horizontal.

9.  Add a Multi-Line Entry beneath Expense Amount to Approve. Title the Multi-Line Entry: Reason for Declining:

10. Click the Rules icon.

    This rule will hide this Multi-Line Entry item if the expense is approved.

    1.  Click Add Rule.

    2.  From the When this is true: section, select Do you approve this expense?

    3.  Select Does not equal.

    4.  Leave A fixed value selected and then select Approve from the next set of options.

    5.  Select Reason for declining: from the Perform this action section.

    6.  Select Hide from the next menu.

    7.  Click Apply and Close.

11. Add page navigation buttons to the end of the page.

    This set of buttons allows the user to see the comments of the approver if the Expense Report is rejected. In the next lesson, you will hide these navigation buttons, so they are displayed after the approver reviews the Expense Report.

12. Save the form.


The approval page is created, but is only used when a workflow is applied to the form. Creating a workflow with Stages is covered in the next section of the tutorial.

**Parent topic: **[Adding tables and workflow elements to a HCL Leap form](tut_roles_and_stages_OV.md)

