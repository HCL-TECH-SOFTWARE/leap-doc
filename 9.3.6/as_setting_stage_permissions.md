# Setting Stage permissions {#settingstagepermissions .task}

Setting Stage permissions defines the “Create”, “Read”, “Update”, and “Delete” permissions for each role in a stage.

A Stage is a step in the life of a form. By default, each form has a Start and Submitted stage. The Start stage is activated when a user begins a form. The Submitted stage is the end of the workflow. You can define different permissions for each role on different stages. There are four actions users can take in the **Access** tab:

#### Create

By default, an initiator can create a form when the application is deployed.

#### Read

By default, only record owners and administrators can read the form when it is submitted.

#### Update
By default, no one can change the form after it is submitted. However, you can authorize users to update the form in the **View Data** section.

#### Delete

By default, only administrators can delete a form from the database.

For example, you can add a custom stage for manager approval by adding a stage, and giving a manager permission to modify the form. The following steps describe how to set the permission for a stage. Before using the following instructions, you must create a Stage between the Start and Submitted stages.

1.  Click the **Access** tab. In the **Stage Settings** parent, select the new stage that you created.

2.  Check the permissions for the stage for each role.

    Permissions must be set for each stage of a form. The permissions that are set on one stage do not carry forward to another stage.


**Parent topic: **[Securing](se_security_toc.md)

