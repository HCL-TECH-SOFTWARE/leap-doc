# Mapping form items to PDF fields and storing the filled PDF { #mappingformitemstopdffields .task }

NEW - The following instructions describe how to create a Service Configuration to map {{shortProductName}} fields to fields in an existing PDF and, when triggered, stores the filled PDF as an attachment to the record.

-   You must have your PDF uploaded in the **Settings** \> **Files** section.
-   If you did not save your application after you uploaded the PDF, click **Save** before you use the following instructions.
-   You must create a {{shortProductName}} form containing fields that are similar to the fields in the PDF.
-   You must have added an attachment item to your application.

1.  Go to the **Settings** tab.

    -   If you only have one form, click **Services** from the menu on the left side of the page.
    -   If there are multiple forms, click **Services** \> **<form\_name \>**.
2.  Click **Add Service Configuration**.

    The Service Configuration window opens.

3.  From the **Service Catalog** menu, select **Documents**.

    A list of available documents is displayed.

4.  Select the PDF from the list and click **Next**.

    The **Inputs** tab is activated.

5.  Select a form item from the **Select source** window, and a corresponding item from the **Select target** window.

    For example, you would map your {{shortProductName}} First Name form item to the First Name field in the PDF.

6.  Click the **Assign input** button that is located between the two windows.

    When valid mapping is done, a check mark appears to the right of the item name in the **Select source**, and **Select target** windows. The mapped value also appears in the list of **Assigned Inputs**.

7.  In the **Select Source** window, switch from **Basic** view to **Constant** view.

8.  In the Event Value field type **True**. In the Select target window, select **Create As Attachment** and click the assign input button located between the two windows. The mapped value will appear in the list of **Assigned Input**.

9.  Click **Next**. The **Outputs** tab is active.

10. Select **Filled PDF** from the **Select Source** window and select an attachment form item from the **Select Target** window.

11. Click **Assign Outputs** button that is located between the two windows. The mapped value will appear in the list of **Assigned Outputs**.

12. Click **Ok**.


**Parent topic:** [{{shortProductName}} document integration](di_pop_doc_with_app_data.md)

