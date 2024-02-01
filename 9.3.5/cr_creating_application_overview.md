# Creating an application {#creatinganapplication .task}

This topic gives a general overview of the application creation process, from opening the HCL Leap interface to launching a completed application.

The following steps are a general overview of the lifecycle of an application.

1.  Log on to Leap. By default you see the **Manage** window which displays the **New Application** button, any previously created applications, and any applications to which you have edit permissions.

2.  Click **New Application**.

    A dialog will open, which provides a choice to create an application from a blank canvas or from an Excel spreadsheet. The rest of this topic describes how to create an application from a blank canvas. For a topic covering creating applications from spreadsheets, see [Creating an application from an excel spreadsheet](cr_creating_application_excel.md).

3.  Click **From Blank**. Enter the name of the new application, and \(optional\) a description or tags for the application. Click **Create**.

    An application opens. A blank grid appears with a Palette of form items.

4.  Add items from the Palette to build the form.

    -   The grid automatically expands as you add form items, and automatically aligns items in the cells.
    -   You can change the size of columns or rows in the grid. Right-click on the edge of the grid to reveal row or column properties.
    -   You can insert additional pages to a form in the Outline view. Page order is flexible, and you can reorder the pages in your form by dragging dropping them to your preferred order.
    -   Many form items can be edited directly on the grid. Click the title of a form item to edit it.
    -   You can modify the properties of each form item by using the Properties side panel. The panel contains tabs that allows the creation of rules, web service calls, or event triggers.
    -   You can save and preview the form at any time by using the **Save** and **Preview** icons.
5.  Click the **Style** tab to customize the appearance of your application. Select or customize a theme or add your own custom CSS to change the style of your application.

6.  Use the **Access** tab to define user roles, such as “Administrator”, “Supervisor”, or “Record Owner”.

    You can add as many users as required for your application to function. For example, when a user completes a vacation request form, the form is sent only to the user’s supervisor. You can also add groups of users to specific roles. For example, you might have a time sheet application that is sent to a group of supervisors upon submission. For more information, see [Security overview](se_security_toc.md).

7.  Use the **Workflow** tab to define stages within a form.

    You can create as many stages as required for your form or workflow. For example, an employee completes a vacation request form. The employee does not see the part of the form where the supervisor approves or rejects the request. When the supervisor receives the form, the next stage is visible, and the request is granted, or refused. You can also use stages to set buttons at specific points in your form. For example, you might want to allow a user to save a draft copy of the form after they reach a specific stage. For more information, see [Adding Stages to an application](sub_adding_stages_toc.md).

8.  Use the **Events** tab to review any custom Javascript added to the application.

9.  Click the **Validation** tab to check your application for errors.

10. After an application is built, click the **Manage** tab. You must now deploy the application. Click **Deploy**.

    Adjust the Deployment Settings and click **Start**.

11. Click **Launch** to view the live application in a web browser.

    The link URL is what is sent to users so they can access the application.

    **Note:** As an application creator, you can edit an application at any time. If you edit a live application, you must redeploy and relaunch it after your changes are saved. If a user is entering data into an application as you redeploy, their work is not saved.


**Parent topic: **[Creating and managing applications](cr_creating_and_managing_toc.md)

