# Setting up security for anonymous access {#settingupsecurityforanonymyousorguestaccess .task}

Using the correct permissions, you can allow anonymous users to access a form.

To allow anyone to complete a form anonymously, without asking for authentication, use the following steps. No data about the user is captured or stored.

**Note:** Administrators must allow anonymous access first.

1.  Start a new application. Enter an application name. From the dashboard in the design environment, click **Access**.

2.  Click the **Initiator** role in the Access navigation.

3.  In the Add Users window, click the **Add group** icon next to the predefined “Anonymous Users” group.

    Once selected, the group appears in the Role Members window.

4.  In the Stage Settings section of the **Access** tab, select the **Start** stage for your form. Confirm that the Initiator has the **Create** permission selected.

    This setting allows anonymous users to submit responses. If a registered user is identified, they can either create a form anonymously or log in using their credentials.

    **Note:** If a user logs on using their credentials, they are no longer anonymous and their user data will be stored.

5.  In the Stage Settings section of the **Access** tab, select the **Submitted** stage for your form. Confirm that the Initiator has the **Read** permission selected.

    This setting allows anonymous users to view responses. You can now send users the View Data URL from the **Manage** tab. For more information on the View Data URL, see [Viewing submitted responses](cr_viewing_submitted_responses.md).


**Parent topic:**[Securing](se_security_toc.md)

