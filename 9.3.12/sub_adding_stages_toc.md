# Adding stages to an application { #configuringwhatusersseeaftersubmittingaform .concept}

It is often desirable to have an application, or form, transition through a set of phases or stages. At each stage the form might be used by different people in different roles. The form also might be presented in a slightly different manner in each stage, such as having some items or pages hidden, or in a read-only state.

Each form in a {{shortProductName}} application can have multiple stages. By default, a newly created form has two stages:

-   **Start** – The initial state of every form. Once the form transitions away from the **Start** stage it cannot return.
-   **Submitted** – A submitted form is stored in this stage. Forms in this stage may be updated by users with permission.

Additional stages can be added and configured by clicking the plus **\(+\)** icon that appears when hovering over a Stage box or by clicking the **Add Stage** button in the Properties panel; however, the **Start** stage is always required and is unique.

## Actions { #section_gcf_vqw_rvb .section}

Each stage can have multiple stage actions. Each stage action presents itself as a button in the form's footer area and therefore the terms “stage action”, and “stage button” are used interchangeably. There are three types of stage actions:

-   **Submit** – Submits the form data, and transitions the form to the next stage. A single stage can have multiple Submit buttons. Each Submit button may have different settings, and may transition the form to a different next stage. A stage that does not have any Submit buttons will be depicted as an "End" stage with a red square icon, however stage buttons may be added at any time.
-   **Save Draft** – Temporarily stores the form's data so the user can return later to complete the rest of the form. A single stage can have multiple Save Draft buttons. Each button may have different settings, such as a unique message for the user. A stage is not required to have a Save Draft button. For more information, see [Saving work as Draft](sad_allowing_users_to_save.md).
-   **Cancel** – Returns the form to its original state before the end-user started making modifications. The form remains within the same stage. A single stage can have only one Cancel button. A stage is not required to have a Cancel button.

Every newly created stage, including the Start stage, is given by default a single **Submit** button and **Cancel** button as a starting point.

## Activities { #section_rjf_wqw_rvb .section}

During the transition from one stage to the next, there are several activities that can take place: **Send an Email**, **Call a Service**, and **Assign Users**.  

The **Call a Service** activity can invoke an external service or another Leap application. It can be executed either before or after the form data is saved. If configured to trigger before save, return values can be mapped to fields in the form. If configured to trigger after save, return values are not saved in the form, regardless of any output mappings defined in the service configuration.


Refer to [Incorporating web services into your applications](cr_using_apps_as_services_toc.md) for more details.


## Controlling item visibility by stage

The **Visibility** tab also allows the application designer to disable or hide individual form items or entire pages within a specific stage of a form. {{shortProductName}} provides control over which users can access or modify form data at each stage. Permissions can be configured by selecting a stage and navigating to **Permissions**, or by using the **Visibility** tab. For more information, see [Application and Security overview](se_security_toc.md).

## Branching { #section_hjd_3rw_rvb .section}

Each stage action may define one \(or more\) conditional branch by clicking on the diamond icon below the stage object in the workflow diagram, or with the action selected by clicking on **+ Add conditional branch**. A branch defines an alternate path the form takes when submitted. A branch must define a condition that determines when it will be followed. Branch conditions may be based on a user in/not in a role or the value of an item on the form. Each branch may have its own distinct activities that are executed when followed.

{% if isDominoLeap %}
## Reminders

Each stage may also enable **Reminders**. Reminders is an automated mechanism for notifying users that they have a form awaiting their action. Reminders may be triggered in three ways: in days after the record arrives into a stage, based on the value of a date field in the form, or a specific hard-coded date. The application owner may customize the To, Subject, and Body of the notification. The app owner may also specify different notification content for submissions that have passed the due date.

!!! note
    For this feature to function properly, the administrator must configure the serverURI config setting.

### Config Properties
The following properties in the VoltConfig affect how and when the reminders are sent.

#### reminders.cadence

For workflow reminders, indicates the days on which reminders should be sent. Positive numbers indicate number of days before due date. Negative numbers indicate number of days after due date. Zero indicates the same day as the due date. 

The default values are: 10, 5, 2, 1, 0, -1 

!!!note
    Changes to this setting are implemented the next time the server is restarted.   Since these changes may require a high volume of document updates on the server, potentially impacting performance, administrators should consider making them during off-peak hours.

#### reminders.scheduledTimeOfDay

The time of day for workflow reminders to be sent by the server. If not set, the time set in the application will be used.

This should be in the format "HH:MM" and use the 24 hour clock notation. (e.g. 17:00 for 5:00 PM) 

The time zone is set using "reminders.scheduledTimeZone" 

!!!note
    Changes to this setting are implemented the next time the server is restarted.   Since these changes may require a high volume of document updates on the server, potentially impacting performance, administrators should consider making them during off-peak hours.

#### reminders.scheduledTimeZone

The time zone that should be used by the workflow reminder system to send reminders. 

If "reminders.scheduledTimeOfDay" is not set, this setting will have no effect.

Please use the [IANA zone description format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).  Example: America/New_York
Do not use the "offset" style format.

!!!note
    Changes to this setting are implemented the next time the server is restarted.   Since these changes may require a high volume of document updates on the server, potentially impacting performance, administrators should consider making them during off-peak hours.

#### reminders.serverName

If the Domino Server is part of a Domino cluster, then this setting declares only one of the servers to run the background tasks that compute and send reminder emails. 

!!!important
    If this property is not set in a clustered environment, every server in the cluster will run reminder background tasks which will likely cause unexpected behaviors such as sending duplicate reminder emails. 

For example, if the following three servers are part of a cluster: LeapServer1, LeapServer2, LeapServer3 
Then, reminder.serverName can be set to a value of CN=LeapServer2/O=ORG 

Rules: 
For any server, if 

1. reminder.serverName is not set or disabled or blank, background tasks will run 
2. reminder.serverName has some value and matches the server name, background tasks will run 
3. reminder.serverName has some value and does not match the server name, background tasks will not run

#### reminders.workingDays

For workflow reminders, indicate which days of the week are considered working days.  Multiple days should be separated by a comma.  The full name of the weekday is required.

The default values are: Monday, Tuesday, Wednesday, Thursday, Friday

Valid day names are: 

Monday 
Tuesday 
Wednesday 
Thursday
Friday
Saturday 
Sunday 

!!!note
    Changes to this setting are implemented the next time the server is restarted.   Since these changes may require a high volume of document updates on the server, potentially impacting performance, administrators should consider making them during off-peak hours.


For more details, review each setting in the VoltConfig database.
{% endif %}


## Designating a Primary Assignee

Designating a primary assignee adds the record to their task list, meaning they are solely responsible for advancing it to the next stage.  The user will be granted view and edit permissions. 

To designate a primary assignee, select a stage on the **Workflow** tab, click the **Permissions** tab, and then toggle **Designate Primary Assignee**.

You can define the assignee by a user lookup (defined at design time) or a field value (evaluated at run time).

When **User Lookup** is selected the author can use the search field to identify the primary assignee. The field is connected to the configured user repository and will only return valid users.

!!!note
    Groups many not be designated as the primary assignee.

When **Value in Form** is selected the author can select a form field that will contain the user-identifying value to assign as the primary assignee.  The value of the field must match the login id attribute (the default is uid) of the configured user repository.

### My Tasks

The **My Tasks** page is accessible from the main page. This page shows records that are assigned to the logged in user as tasks in the list, if  designated as the primary assignee. The user is intended to take action on each task. Tasks are removed from the list when the record is moved to the next stage.


## Additional Topics

The following topics describe scenarios related to stages and workflow in your HCL Leap application.

-   **[Editing the message a user sees upon form submission](sub_editing_the_message_a_user_sees.md)**  
The administrator of a {{shortProductName}} application can edit the completion message a user sees when submitting a form.
-   **[Redirecting users after form submission](sub_editing_the_url_a_user_sees.md)**  
The administrator of a {{shortProductName}} application can add a URL that is triggered when a form is submitted.
-   **[Sending an email after a user submits a form](sub_sending_an_email.md)**  
You can send email notifications to managers or other users by adding an activity to the Submit button in a form.
-   **[Populating information upon form submission using a web service](sub_use_service_to_populate_on_form_submission.md)**  
Web services can perform many functions, such as sending data to other forms or applications. The following instructions describe how to use a web service to add information to a form automatically after it is submitted.
-   **[Assigning users to a role after submission](sub_assigning_a_user.md)**  
You can dynamically assign roles to a form after form submission.
-   **[Configuring behavior of a form on submission](sub_sending_a_user_to_another_url.md)**  
Once a user completes a {{shortProductName}} form, you can send them to another stage of that form.
-   **[Saving work as a draft](sad_allowing_users_to_save.md)**  
Some applications cannot be completed by the user in one session. If your application is very large or complicated, you can allow users to save their work as a draft before submitting it.
-   **[Scenario: hidden or read-only form items in Stages](sub_hidden_or_read_only_items_in_stages.md)**  
This scenario uses a Vacation Request application to describe how to use multiple Stages to make sections of a form that is either hidden, or read-only.
-   **[Saving a PDF to a file location](sub_saving_pdf.md)**  
Determining where you want to save your filled PDF is useful considering how many processes "pick up" documents from watched folders. Designers have the option of saving the file to a specific location, as an attachment to the {{shortProductName}} submission record, or both.

**Parent topic:** [Adding dynamic behavior](cr_adding_dynamic_behavior.md)

