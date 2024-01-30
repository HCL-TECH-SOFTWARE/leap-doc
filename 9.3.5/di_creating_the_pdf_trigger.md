# Creating the PDF trigger {#creatingthepdfbutton .task}

The following instructions describe how to create a trigger that calls the PDF service, and triggers the service when the user clicks the button.

When the user clicks the button, the service that maps information from the form to the PDF is triggered. The PDF is displayed, or stored as an attachment, with user supplied information in the PDF fields.

1.  Add a **Button** to your form from the Palette.

2.  Change the **Caption** of the button so users know that clicking it populates a PDF.

    For example, change the caption of the button to Create PDF.

3.  In the Properties side panel, select **Call a service when clicked**. Select the Service Configuration you created from the menu.

4.  **Save** your application.


When the application is deployed, you can click the **Create PDF** button and a PDF is populated containing the values that are entered in the Leap application.

**Note:** You can use other common form events as triggers, including **validateButtonPressed**. Stage action buttons cannot be used as triggers.

**Parent topic:**[Leap document integration](di_pop_doc_with_app_data.md)

