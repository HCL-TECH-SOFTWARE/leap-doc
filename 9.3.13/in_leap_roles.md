# Understanding Leap roles

Leap usage is separated into 4 roles: UseApplicationsUsers, EditApplicationUsers, SuperAdminUsers, AdministrativeUsers.

## AdministrativeUsers

Administrative users are able to set up the Leap server. You must have an administrative user to complete the installation process as described in [Completing the installation](in_setting_up_environment.md).

A sample setting is: “Special subject: None, Mapped users, admin\_user\_name ”. 

Users in this role, automatically inherit the abilities of all other roles. 

Users in this role have access to the Admin configuration page and admin dashboard.

!!!note
    You must map **AdministrativeUsers** to an appropriate realm.

## SuperAdminUsers

Super Administrative Users are users, or groups, that may edit all Leap applications without explicit security settings. They do not have access to application data. To access the data, a user must be added to a role within the application and the application must be redeployed.  

Users in this role also have access to the Admin dashboard.

## EditApplicationUsers

Authenticated users that can design, deploy, and use Leap applications. 

A sample setting is: “Special subject: All authenticated in Application's Realms”.

!!!note
    You must map **EditApplicationUsers** to an appropriate realm.

## UseApplicationsUsers

Authenticated users that can use deployed Leap applications. 

All users in the **AdministrativeUsers**, **SuperAdminUsers**, and **EditApplicationUsers** automatically have access to use deployed applications. 

Only adjust this setting if you want to allow a broader set of users than those listed in the **AdministrativeUsers**, **SuperAdminUsers**, and **EditApplicationUsers** roles. Otherwise, leave this role unmapped. 

A sample setting, if you must map the role, is: “Special subject: All authenticated in Trusted Realms”.

**Parent topic:** [Preparing to deploy](in_prep.md)