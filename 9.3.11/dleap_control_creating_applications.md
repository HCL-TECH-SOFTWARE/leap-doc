# Controlling who creates HCL Domino Leap applications

To configure who can create and delete applications, you need to modify the Access Control List (ACL) for VoltBuilder.nsf.

Users with Editor access and permission to delete documents are able to create and delete Domino Leap applications.

By default, the ACL of VoltBuilder.nsf allows any authenticated user Editor access and the ability to create a Domino Leap application:

![image shows the default acl for the VoltBuilder.nsf](C:\HCL\Dev\repos\leap-mkdocs\9.3.8\graphics\dleap\volt_builder_default_acl.png)

As an administrator, you might want to restrict who can create applications. To restrict who can create and delete applications, complete the following steps:

1. Create a "Volt App Authors" group in the Domino directory. You can use any group name. "Volt App Authors" is an example.

2. Add an entry to the ACL entry in VoltBuilder.nsf. Use "Volt App Authors" as the entry name. Set the user type to **Group**. Give the group **Editor** access and select **Delete documents**.

3. Change the Default ACL entry in VoltBuilder.nsf to have **Reader** access.

!!! note
    By default, a user can only read and modify the applications they own. It may be useful to give at least one person in your organization permission to read and modify all applications. To do this, give a user Editor access and assign them the **VoltAppsManager** role. They will then be able to help other application authors with design and/or deployment issues.

For more information on VoltBuilder.nsf, see [Post-installation tasks](dleap_post_install_tasks.md).

**Parent topic:** [Administering](administering_leap.md)