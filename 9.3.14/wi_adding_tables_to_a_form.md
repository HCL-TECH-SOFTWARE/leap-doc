# Adding tables to a form { #addinglinesdynamicallytoaform .task}

The **Table** form item enables the user to add complex entries to a form.

You can use the **Table** form item to create a section where a user can submit repeated data. For example, in a job application you can build a table that asks for work history. You can create columns such as the “Company Name”, “Job Title”, “Start Date”, and “End Date”. The user can add as many rows under these columns as required to provide their work history. In many cases, it is not feasible to add individual items for each repeating element as you cannot know in advance how many repeating elements the use requires. To achieve this functionality, the **Table** form item contains the following two complimentary elements:

-   **Child form** – The Child form is a supporting form that contains the form items that collect the repeated data. In the “work history” example, the child form contains a **Date** form item for collecting the “Start Date” of a previous job. A child form is similar to a regular form, however it is limited to a single page. When a user completes their job history, the child form is shown in a dialog box. The user can enter as many rows as required to submit a complete job history. In the Outline view, the child form is called "Table", and is listed as a subset of the parent page.
-   **Table display** – The Table display shows the data entries that are collected by the child form. The columns in the table represent the individual items from the child form. The visibility of specific columns in the table is configurable in the properties side panel.

1.  In the Palette, click **Specialized**.

    The list of specialized form items expands.

2.  Select **Table**, and drop it onto the form.

    Adding the table creates a **Table** child form in the Outline view.

3.  In the table, click the link to access the child form, and define the table columns by selecting form items from the **Common** Palette.

    Ensure that you give each form item a specific name as the items added to the **Table** child form become column titles for the table.

    For example, if you insert a **Single Line Entry** form item to record someone’s name, you must change the title of the item, or the table on the will display “Single Line Entry”. The title of the form item is not helpful to users. You will then have to manually adjust the item name using the Properties side panel.

4.  When you have built your table, go to the **Outline** view on the right side of the screen and click the parent **Page**.

    You are returned to the main form design area. The table appears on the form, and the titles of the table items are displayed as column headers.


**Parent topic:** [Adding specialized form items](wi_introduction_to_specialized_form_items.md)

