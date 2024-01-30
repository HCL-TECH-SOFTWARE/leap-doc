# Assigning users or groups to roles 

Give the users in your organization permission to work with the data relevant to them by assigning them roles.

After you establish roles for the users in your organization, you can start assigning users to those roles by adding them individually, or in groups using the **Access** tab in HCL Leap. For example, you can assign users or groups as defined in your LDAP to **Roles**. You can use the search to find users and groups within your company directory, or database. There are several predefined groups from which to choose:

#### All Authenticated Users

Any user who is authenticated with your organization.

#### Anonymous Users

Any user who you want to work anonymously with the application.

#### Invited Users

Any anonymous user who receives a unique URL generated from within stages when an application changes from one stage to another. A user who is not normally given access to the form in that stage can use that URL to participate in the workflow in that instance.

**Note:** Requires allowed anonymous access.

#### Instance Creator

The user who submitted a form.

**Note:** You cannot add **All Authenticated Users** to any role that has application **Edit** permissions. This prevents the applications from all other users from appearing in your **Manage** tab, making your applications easier to find. This also prevents your application from appearing on the **Manage** page for every other authenticated user.

To add users from predefined groups:

1.  In the **Access** tab, go to the navigation tree and click the role you want to assign in the **Assign Users** menu.

    The Assign Users window opens.

2.  Add new usersor groups, or select from a predefined group:

    -   To create new usersor groups, enter the name of an individual useror group. Select it, then click the **Add user** plus sign.

        **Note:** There is a limit to the length of a single user name, or ID. The limit varies by language and character set. For example, the English limit is 256 characters. If you exceed the character limit, you are shown an error message when you attempt to save the form.

    -   To use an existing group, select the group and click the **Add group** plus sign.
    The **Role Members** window shows the members that are assigned to the role.

3.  You can remove members from a role by clicking **Delete user** for the name of the member., or run a test to see whether Leap can find the member.

    -   To remove a member from a group, click **Delete group** for the name of the member.
    -   To test if Leap can find a group member, click **Validate**.

**Parent topic:**[Securing](se_security_toc.md)

