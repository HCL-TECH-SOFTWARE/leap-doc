# Adding stages to an application {#configuringwhatusersseeaftersubmittingaform .concept}

It is often desirable to have an application, or form, transition through a set of phases or stages. At each stage the form might be used by different people in different roles. The form also might be presented in a slightly different manner in each stage, such as having some items or pages hidden, or in a read-only state.

Each form in an HCL Leap application can have multiple stages. By default, a newly created form has two stages:

-   **Start** – The initial state of every form. Once the form transitions away from the **Start** stage it cannot return.
-   **Submitted** – A submitted form is stored in this stage. Forms in this stage may be updated by users with permission.

Additional stages can be added and configured by clicking the plus **\(+\)** icon that appears when hovering over a Stage box or by clicking the **Add Stage** button in the Properties panel; however, the **Start** stage is always required and is unique.

## Actions {#section_gcf_vqw_rvb .section}

Each stage can have multiple stage actions. Each stage action presents itself as a button in the form's footer area and therefore the terms “stage action”, and “stage button” are used interchangeably. There are three types of stage actions:

-   **Submit** – Submits the form data, and transitions the form to the next stage. A single stage can have multiple Submit buttons. Each Submit button may have different settings, and may transition the form to a different next stage. A stage that does not have any Submit buttons will be depicted as an "End" stage with a red square icon, however stage buttons may be added at any time.
-   **Save Draft** – Temporarily stores the form's data so the user can return later to complete the rest of the form. A single stage can have multiple Save Draft buttons. Each button may have different settings, such as a unique message for the user. A stage is not required to have a Save Draft button. For more information, see [Saving work as Draft](sad_allowing_users_to_save.md).
-   **Cancel** – Returns the form to its original state before the end-user started making modifications. The form remains within the same stage. A single stage can have only one Cancel button. A stage is not required to have a Cancel button.

Every newly created stage, including the Start stage, is given by default a single **Submit** button and **Cancel** button as a starting point.

## Activities {#section_rjf_wqw_rvb .section}

During the transition from one stage to the next, there are several activities that can take place: Send an Email, Call a Service, and Assign Users. The **Visibility** tab also allows the application designer to disable or hide any form item, or entire page, within a specific stage for a particular form. Leap provides control over which users can access or modify the Form's data at any particular stage. The setting of these permissions is done by clicking on a stage and navigating to **Permissions**, or by clicking the **Visibility** tab. For more information, see [Application and Security overview](se_security_toc.md).

## Branching {#section_hjd_3rw_rvb .section}

Each stage action may define one \(or more\) conditional branch by clicking on the diamond icon below the stage object in the workflow diagram, or with the action selected by clicking on **+ Add conditional branch**. A branch defines an alternate path the form takes when submitted. A branch must define a condition that determines when it will be followed. Branch conditions may be based on a user in/not in a role or the value of an item on the form. Each branch may have its own distinct activities that are executed when followed.

-   **[Editing the message a user sees upon form submission](sub_editing_the_message_a_user_sees.md)**  
The administrator of an HCL Leap application can edit the completion message a user sees when submitting a form.
-   **[Redirecting users after form submission](sub_editing_the_url_a_user_sees.md)**  
The administrator of an HCL Leap application can add a URL that is triggered when a form is submitted.
-   **[Sending an email after a user submits a form](sub_sending_an_email.md)**  
You can send email notifications to managers or other users by adding an activity to the Submit button in a form.
-   **[Populating information upon form submission using a web service](sub_use_service_to_populate_on_form_submission.md)**  
Web services can perform many functions, such as sending data to other forms or applications. The following instructions describe how to use a web service to add information to a form automatically after it is submitted.
-   **[Assigning users to a role after submission](sub_assigning_a_user.md)**  
You can dynamically assign roles to a form after form submission.
-   **[Configuring behavior of a form on submission](sub_sending_a_user_to_another_url.md)**  
Once a user completes an HCL Leap form, you can send them to another stage of that form.
-   **[Saving work as a draft](sad_allowing_users_to_save.md)**  
Some applications cannot be completed by the user in one session. If your application is very large or complicated, you can allow users to save their work as a draft before submitting it.
-   **[Scenario: hidden or read-only form items in Stages](sub_hidden_or_read_only_items_in_stages.md)**  
This scenario uses a Vacation Request application to describe how to use multiple Stages to make sections of a form that is either hidden, or read-only.
-   **[Saving a PDF to a file location](sub_saving_pdf.md)**  
Determining where you want to save your filled PDF is useful considering how many processes "pick up" documents from watched folders. Designers have the option of saving the file to a specific location, as an attachment to the Leap submission record, or both.

**Parent topic:** [Adding dynamic behavior](cr_adding_dynamic_behavior.md)

