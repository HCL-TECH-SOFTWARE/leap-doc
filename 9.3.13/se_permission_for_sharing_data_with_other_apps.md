# Defining permissions to share data with other applications { #definingpermissionstosharedatawithotherapplications .task}

{{fullProductName}} applications can share data through services with other {{shortProductName}} applications. To allow other applications access to the data from the application you are designing, you must define the security permissions.

When setting permissions, you are defining access to the data based on the application, and user, that calls the service. For example, you create an application called “Product Names”. You want your “Purchase Order” application to read the data stored in the “Product Names” application, and use the data to populate a drop-down list. In the “Product Names” application, create a “Purchase Order” user group in Roles, then give that **Read** access. You can also allow other applications to write data to the “Product Names” application. For another application to write data, it must have **Write** access.

For more information about creating roles, see [Defining basic security roles for users](as_define_security_roles.md#). For more information on using other {{shortProductName}} applications as services, see [Integrating your application with existing {{shortProductName}} applications](cr_using_other_apps_as_services.md).

1.  Go to the **Access** tab.

2.  Select **Design Settings**.

3.  For a specific role, click the **Read**, **Write**, or both check boxes.


**Parent topic:** [Securing](se_security_toc.md)

