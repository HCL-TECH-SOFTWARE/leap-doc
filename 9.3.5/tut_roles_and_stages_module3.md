# Applying access control through Roles {#addingworkflowtoaform .learningContent}

Access control defines who is able to view and modify the form in different stages. For example, only the form administrator can change the layout of the form, while user access is restricted to opening and submitting the form. Creating this access control is done with Roles.

In this lesson, learn how to:

-   Open to the Access tab.
-   Know the difference between Closed and Open role types.
-   Add a user type to the list of defined Roles.
-   Assign users to the various Roles.
-   Assign users to Stages.

Estimated time that is required to complete this module: 20 minutes

## Applying access control through Roles {#applyingaccesscontrolthroughroles}

Access control defines who is able to view and modify the form in different stages. For example, only the form administrator can change the layout of the form, while user access is restricted to opening and submitting the form. Creating this access control is done with Roles.

By default, the Access tab, three roles are already defined for you:

-   Administrator – Users, or groups, with administrator privileges for an application.
-   Initiator – Any user, or group, who can submit a form or initiate an application. You can set some applications to be available to all users, and some to be available to specific users, or groups.
-   Record Owner – The user who submits the form. After a user initiates and submits a form, they become the Record Owner.

Each role can be either Open or Closed. When a role is Open, it dynamically assigns users at run time. When a role is Closed, the users must be set on the Access screen, and are static. For example, in a form, you might have employees sign in and enter their names and employee numbers. If the role is Open, the application can pull information about the employees’ superior from a company database and populate the form. For this tutorial, all roles must remain Closed.

The users who submit Expense Reports are Initiators, and for this scenario the users who review the Expense Reports are Human Resources. As the Initiator role is already created, you must create the Human Resources role.

1.  Click the Access tab.

2.  Click the Add Role icon for the Record Owner role.

    A new role is created.

3.  Rename the new role Human Resources.

4.  Now that the roles are created, add members to the roles. Adding members to the roles determines who can access the application. There are four predefined user groups:

    All Authenticated Users
    :   Any user who is authenticated with your organization. Users must sign in with a user ID and password to access the application.

    Anonymous Users
    :   Any user who you want to work anonymously with the application. Anyone who has the link to the application can submit it, without signing in.

    Invited Users
    :   Any anonymous user who receives a unique URL generated from within stages when an application changes from one stage to another. A user who is not normally given access to the form in that stage can use that URL to participate in the workflow in that instance.

    Instance Creator
    :   The user who submitted a form.

    You can also add your own Groups or Individual users to a role.

5.  In the Assign Users menu, select Initiator.

    The Initiator role automatically has All Authenticated Users added. Access for this role is complete.

6.  Select Human Resources from the Assign Users menu.

    1.  In the Individual Users field, add your own name.

        As you manually enter Individual Users or Groups, Leap provides you with predictive matches based on your entry. These predictive matches are taken from your company LDAP, users that are configured in your IBM® WebSphere® Application Server, or IBM WebSphere Portal Server. By adding your name to the Human Resources Group, you are able to enter sample data into the form, and review all submitted responses.

    2.  Click Add User icon.

7.  Now that access to submit and review a form is set, edit the properties of the individual roles. For example, you want Human Resources to review and approve the form, but the form must be read-only unless it is returned to the user.

    Remember the order of the workflow for our form: When the user submits the form, it moves from the Start stage to the Awaiting Approval stage. If a form is rejected because of errors, it is sent to the Approval Request stage, so the submitter can correct the errors and submit the form again.

8.  Go to Stage SettingsExpense Report, and select Start.

    You see that the Initiator has permission to Create and submit the form.

9.  Go to Stage SettingsExpense Report, and select Approval Request.

    1.  For the Administrator, make Read and Delete are selected.

        These permissions give the Administrator the ability to see and delete submitted forms in this stage, but not to change the submitted data.

    2.  For Record Owner, ensure Read and Update are selected.

        These permissions allow the person who submitted the form to edit the form in the case of errors, and submit it again for approval.

    3.  For Human Resources, ensure the Read is enabled.

10. Go to Stage SettingsExpense Report, and select Awaiting Approval .

    1.  For the Administrator, make Read and Delete are selected.

    2.  For Record Owner, ensure Read is selected.

        This permission allows the person who submitted the form to see it, but not change any data.

    3.  For Human Resources, select Read, and Update.

        Although the information submitted by the user is read-only for the approver in Human Resources, the word Update is used to manage access settings. In this instance, the word Update means that an approver can use the Submit and Cancel buttons on the form. Update does NOT mean that the approver can update or manipulate the submitted data.

11. Save the application.

12. Click the Manage tab and deploy the application and enter sample data into the form.

13. After you submit sample data, return to the form and click View Data from the Manage tab.

    Accept or reject the sample data to test the workflow elements you built into the form.


**Parent topic: **[Adding tables and workflow elements to a HCL Leap form](tut_roles_and_stages_OV.md)

