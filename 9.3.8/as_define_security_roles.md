# Defining basic security roles for users 

Create roles for users in your organization so they can work with data that is relevant to them.

{{fullProductName}} employs a customizable, role-based access control model to define who can access and modify the application. Roles are assigned to individuals or groups, granting specific permissions for data access and application maintenance. These roles can be assigned manually or programmatically through web services.

There are three predefined roles:

- **Administrator**: A role that grants administrative privileges to users or groups for an application.

- **Initiator**: A role which allows any user or group to submit forms or initiate applications. For instance, in a Vacation Request application, all users in an organization could be granted Initiator privileges allowing them to initiate and submit a Vacation Request.

- **Record Owner**: A role assigned to the user who submits a form.

Roles can be Open \(dynamic\) or Closed \(static\).

- **Open** roles – Assignments can be made statically or dynamically. Dynamic assignments are triggered by web service calls within stage actions, allowing for data-driven assignments. For example, a web service can look up a manager for each form submission and assign them a role.
- **Closed** roles – Closed roles require explicit assignment of users or groups within the Access tab. Dynamic assignment through web services is not supported for closed roles.

To add a role:

1.  In the design environment, click the **Access** tab.

    The **Define Roles** window opens.

2.  Click the **Add role** green plus sign to add a role.

    For example, you can name the new role, “Manager”.

3.  Click the **Add role** plus sign to define another role.

    For example, your form also requires a “Shift Supervisor”.

4.  Use the radio buttons to select whether the role is **Open** or **Closed**.


**Parent topic:** [Securing](se_security_toc.md)

