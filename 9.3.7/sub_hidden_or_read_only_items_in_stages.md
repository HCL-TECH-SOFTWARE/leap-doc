# Scenario: hidden or read-only form items in Stages {#hiddenreadonlyitems .concept}

This scenario uses a Vacation Request application to describe how to use multiple Stages to make sections of a form that is either hidden, or read-only.

The Vacation Request application is built with two sections: the top section contains fields the employee fills out to schedule vacation time. The bottom section of the form contains information for the manager's approval or rejection. When the users complete the form, they do not need to see the manager's portion. When managers review the submitted form, they must not modify the employee's submitted portion. In both parts of this example, marking items as hidden, or read-only is valuable.

**Tip:** By building the user's and manager's portions of the form inside a Section, you can apply the hidden or read-only values to the entire section. Without using Sections, you must set the property for each individual form item.

The Vacation Request form has three Stages:

-   **Start**: The beginning phase where users view and complete the form for submission
-   **Approval**: This stage was created by the form designer. When the user submits the form, it moves to the Approval stage and is processed by a manager.
-   **Completed**: When the manager approves, or denies the request, the submitter is notified, and the form is considered closed.

When the form is viewed in the **Workflow** tab, it is identical to how it appears the design environment. The main differences are the icon buttons on the upper right of each form item, and the addition of workflow buttons at the bottom of the form. You automatically view the section in the **Start** stage. For each form item, the following icons are available:

-   ![The Visibility icon is a small square with lines across it, representing text.](graphics/visible%20icon.jpg): The **Visibility** icon. When clicked, this icon hides form items or a section on a particular Stage.
-   ![The Read-Only icon is a small square with a picture of a pencil.](graphics/read-only%20icon.jpg): The **Read-Only** icon. When clicked, this icon makes a form item or section Read-Only in a Stage.

To make the Vacation Request form hide the Manager's section of the form: In the **Start** stage, scroll down to the Manager's section and click the **Visibility** icon. A red line appears diagonally through the icon, representing that the section is now hidden from view in this stage. If you save and preview the form, the Manager's section is not visible.

To make the user's portion of the form read-only: In the **Approval** stage, go to the top of the user's portion of the form. Click the **Read-Only** icon. A red line appears diagonally through the icon, representing that the section is now read-only.

Using a basic example, this scenario described how to set properties on form items within Stages. Setting items or sections as hidden or read-only simplifies form design, yet allows for complex processes to be built into one form.

**Parent topic:** [Adding stages to an application](sub_adding_stages_toc.md)

