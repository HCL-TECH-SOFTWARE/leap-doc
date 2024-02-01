# Defining basic security roles for users 

Create roles for users in your organization so they can work with data that is relevant to them.

HCL Leap uses a customizable role-based model to define who can access data and who can modify the application. Roles allow the assignment of data access, and application maintenance permissions.Individuals or groups are then assigned to the roles with the access component, or programmatically through web services. There are three predefined roles:

#### Administrator

A role that includes users, or groups, with administrator privileges for an application.

#### Initiator

A role that includes any user, or group, who can submit a form or initiate an application. For example, if the application was for Vacation Requests, you can allow all users in your organization to initiate, or submit, a Vacation Request.

#### Record Owner
A role that contains the user, or group, who submitted the form dynamically at run time.

Each role can be Open \(dynamic\) or Closed \(static\).

-   Open roles – where assignments are done either statically, or dynamically with a web service call defined on a stage action within stages. Users are assigned based on data that is gathered during the form submission. For example, a web service looks up a manager for each user who submits a form, and assigns the manager a role.
-   Closed roles – where assignments of users and groups to the roles must be done explicitly from within the Access tab. Closed roles do not assign users dynamically with a web service.

To add a role:

1.  In the design environment, click the **Access** tab.

    The **Define Roles** window opens.

2.  Click the **Add role** green plus sign to add a role.

    For example, you can name the new role, “Manager”.

3.  Click the **Add role** plus sign to define another role.

    For example, your form also requires a “Shift Supervisor”.

4.  Use the radio buttons to select whether the role is **Open** or **Closed**.


**Parent topic:**[Securing](se_security_toc.md)

