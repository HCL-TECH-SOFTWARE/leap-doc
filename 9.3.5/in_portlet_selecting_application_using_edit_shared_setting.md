# Selecting an application using Edit Shared Setting {#selectingapplicationsharedsetting .task}

You can add an HCL Leap application to a WebSphere® Portal page with the **Edit Shared Settings** menu option.

To permanently set which application is displayed in the Leap Portlet, use the following instructions. To dynamically set the application displayed at run time, see[Leap Portlet parameters](ref_portlet_parameters.md) .

To select an application for a WebSphere Portal page, you must have Edit privileges for both the WebSphere Portal page, and the Leap Portlet. Ensure the WebSphere Portal page is in **Edit** mode.

1.  Click the menu icon for the portlet name, and select **Edit Shared Settings**.

    The Shared Settings page opens.

2.  Update the values on the **Edit Shared Settings** page:

    -   **Application URL**: Enter the full URL to the application either by typing in the URL, or by clicking **Browse** and selecting the URL from a list of deployed applications.
    -   **Preferred Security Mode**: The preferred authentication mode to use for applications that support both anonymous and authenticated users. Anonymous only or Authenticated only applications are not affected, and use the authentication mechanism that is supported by the application.
        -   The default is to open the application anonymously. The page shows a selected check box for “Use anonymous access when supported by the application”.
        -   To open an application with the authentication credential of the current WebSphere Portal user, clear the check box for “Use anonymous access when supported by the application”.
    -   **Page refesh setting**: This setting determines whether the portal page is refreshed when the form is submitted. If your portal page depends on portlet wires, then you must have the page refresh upon form submission.
        -   The default is to **not** refresh the portal page when the form is submitted.
3.  Click **OK** to save your changes.


