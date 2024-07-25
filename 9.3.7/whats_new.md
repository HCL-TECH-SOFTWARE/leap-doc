# What's new in 9.3.7?

For a full list of fixes by release, see this [article](https://support.hcltechsw.com/csm?id=kb_article&sysparm_article=KB0104676).

## New features

- Integrate with HCL Volt MX Foundry. For more information, see [Integrate with HCL Volt MX Foundry](admin_foundry_integration.md).
- A Repeating Section widget has been added to the Custom Widget API.  For more information, see [Custom Widget API](customwidgetapi_landing.md).
- Added setup instruction for Kubernetes. For more information, see [Creating a container registry secret](helm_container_registry_secret.md) and [Creating and formatting the custom-values.yaml](helm_creating_custom_values_file.md).

## Behavior changes

**Updated Design Canvas**

The buttons for adding/deleting rows/columns is more prominent and has a new look.

**Updated the Rules Dialog**

The condition is now listed first and then the actions.

**Improved create app from spreadsheet**

An app page with a data grid is included as part of the app creation.

## 9.3.6

**New features**

- Admin Config UI changes. For more information, see [Admin Configuration Page](admin_config_ui.md).

**Behavior changes**

- Embedding Leap applications
    - The 'xFrameOptions' property has been deprecated. Use ['embedDomainWhitelist'](co_configuration_properties.md#embeddomainwhitelist-section_embeddomainwhitelist-section).
    - The default behavior has changed to not allowing Leap forms to be embedded.
- Roles/Permissions
    - AdministrativeUsers now have the privileges of SuperAdminUsers; they can now see and edit all applications.
    - Users in the SuperAdminUsers role no longer have access to the application data by default. To access the data, they must be given the correct permission within the application.
- Leap Kubernetes image
    - A new PostgreSQL JDBC jar file has been included in the Leap image. The file name no longer includes the version number to prevent future breakages when it is updated. The original file 'postgresql-42.6.0.jar' will be removed from the image in the next release.

## 9.3.5 { .section}

- Bug fixes.

## 9.3.4 { .section}

- Bug fixes.
- Added support for Secrets in Kubernetes. For more information, see [Provide admin user a custom secret](helm_admin_customsecret.md).

## 9.3.3 { .section}

- Support for Custom Widget API. For more information, see [Custom Widget API](customwidgetapi_landing.md).
- Support for PostgreSQL databases. For more information, see [Creating a PostgreSQL database](create_postgresql_db.md).
- Admin Application Dashboard. For more information, see [Admin Application Dashboard](admin_application_dashboard.md).

## 9.3.2 { .section}

- **Open Liberty** support.

    For more information, see the following topics

  - [Deploying to a Container (Kubernetes) Platform - Open Liberty](deploy_container_kubernetes_openliberty.md)

## 9.3.1 { .section}

- New **Copy/Paste** feature.

    The "copy/paste" feature enables the application author to copy an item from their form and paste it into another page/form/app page within the same application or another one on the same Leap server. For more information, see [Copying items](cr_copying_items.md).

- New **Workflow Branching** feature.

    The "workflow branching" feature enables the application author to specify a condition that changes where a submitted form is directed. For more information, see [Branching](sub_adding_stages_toc.md#section_hjd_3rw_rvb).

- Improved HTML editor experience.
- Improved page navigation and validation behavior, including custom error handling with JavaScript API.
- Refreshed Workflow diagram UI.

Administrative improvements:

- Beginning with this release, Leap has a limited capability to restrict the rendering of Leap Forms using a “Strict CSP” policy. For more information, see [Strict CSP](leap_strict_csp.md).
- Kubernetes-friendly Container.
- Access to service descriptions may be restricted by user, group or special role \(i.e. authenticated, anonymous, etc\). For more information, see the following topics:
  - [Deploying a Service Description](ref_service_deploying_service_description.md)
  - [Configuration properties](co_configuration_properties.md)

## 9.3 { .section}

UI Improvements:

- Tabs across the top are replaced by a sidebar.
- Added breadcrumb navigation
- Updated the toolbar
- Item Properties are now shown in a side panel instead of a modal dialog.
- New Workflow Design. New apps will have two stages: Start and Submitted.
- Improved user experience for Action Properties and Submit Activities
- Improved user experience for Workflow Stage Visibility
- Improved user experience for Stage Properties and Roles/Permissions

New Palette Items:

- App pages. App Pages provide a free-form app building canvas, and allow authors to build anything from simple welcome pages to complex dashboards. App pages differ from Forms, which provide a canvas that specifically defines an interface to collect and store data with a built-in function to submit a record and move it through workflow stages. For more information, see [Creating an application](cr_creating_application_overview.md) and navigate to Step 4.
- DataGrid
- RichText Entry field
- Name Picker field

Other:

- New service activity timing: before or after data is submitted
- Support for Role based rules allows authors to define a rule with the condition that a user is or is not in a particular role. For more information, see [Creating rules in your application](ru_creating_rules_in_your_form.md).
- Support for Stage based rules allows authors to define a rule with a condition that the form is or is not in a particular stage.
- New javascript functions are supported. For more information, see [Interface objects](ref_jsapi_user_interface_objects.md).
- New options for redirecting: redirect to another Leap Application, web URL, form or app page. For more information, see [Redirecting users after form submission](sub_editing_the_url_a_user_sees.md).
- New form property Show print and delete buttons.
- User’s can now determine where to save a filled PDF. For more information, see Saving a PDF to a file location.
- Ability to add a custom theme to be shared by multiple applications.

## 9.2.1 { .section}

Support for the following:

- Oracle 19c:

New features include:

- Embedding of forms without an `<iframe>`

## 9.2  { .section}

New features include:

- New Application wizard
- Create an application directly from an existing Excel spreadsheet
- Send attachments in email notifications \(including filled PDF’s\)
- Numerous visual and usability improvements, including:
  - Double-click to open item properties
  - One-click copy to clipboard on URLs and embed codes
  - Improved first-time-user experience
  - Redesigned palette
  - Additional confirmation prompts on irreversible actions
  - Stylistic improvements to the Manager page
- Addition of has value and not operators for View Responses and the Data REST API
- Addition of has value and has no value for rules
- Improved experience for those using FlexNet licensing
- Print view enhancements
  - Vertical table layout option \(for wide tables\)
  - Removed application size limit
  - Use the Data Label property
  - mark-up is instrumented to allow for easier manipulation
- Better default logging on failed service calls
- Attachment clean-up service now configurable
- Include record UID in exported spreadsheets
- General fixes and security patches

## 9.1 { .section}

New features include:

- PDF document integration enhancements:
  - Store filled PDFs to a network drive
  - Map Table items to tables in a PDF
  - Ability to flatten a filled PDF
- New JavaScript API functions:
  - app.getLocation\(\)
  - item.setColumnHeaders\(\) and item.getColumnHeaders\(\) for Table items
- A new Custom Attribute property
- Full accessibility of the date picker
- Ability to render HCL Leap applications within ElectronJS desktop applications
- New applications now have a middle Submitted stage by default
- Option to block UI interaction while a service call is executing
- Ability to hide the Use tab
- General fixes and minor improvements

## 9.0 { .section}

New features include:

- New JavaScript API functions: `BO.isValid()`, `BO.getInvalidMessages()`, and `app.showMessage()`.
- "Reply To" capability for email notifications.
- Allow attachments to be viewed in browser instead of downloading.
- Display Data Label property in View Responses.
- Custom JavaScript editor is now resizable.
- Design-time usability improvements for service calls.
- General and security fixes.

## 8.6.4.2 { .section}

Support for the following versions:

- Oracle 12c and 11g
- 10.5 and 11.x
- 8.5.5 and 9
- Java™ 7
- Derby 10.10.2
- ICU 55.1

New features include:

- An updated Styles tab to enable easy customization of an application's appearance through changes to colors, fonts and other style attributes. Use the provided Customize action to customized your theme and then use the theme export and import functionality to style other applications with the same theme. Previously available styling features, like the ability to add additional custom CSS are still available and contribute to the overall look of an application, but are not edited or modified as part of the new theme customization feature. For more information, see [Styling your application with a custom theme](cr_custom_theme.md).
- Application owners can now import a set of data from a spreadsheet into an application. An Import Data button for each application is provided in View Responses. Data can be imported from recent versions of xls and xlsx and the data must conform to specific application constraints and setup requirements. For more information, see [Importing data in view responses](cr_import_data_in_view_responses.md).
- Application designers will now have the choice to store filled PDF documents as an attachment as part of a submitted record, rather than simply returning the filled PDF to the user. For more information, see [Mapping form items to PDF fields and storing the filled PDF](di_mapping_form_items_to_pdf_fields_and_attaching.md).
- General and security fixes.

## 8.6.3 { .section}

Support for the following versions:

- Oracle 12c and 11g
- 10.5
- 8.5.5
- Java 7
- Derby 10.10.2
- ICU 55.1

New features include:

- An easy-to-use **Format** feature. Line of Business users can enter simple expressions samples of the required format to set format parameters. More advanced users can enter regular expressions. A customizable error message is also available for this feature.
- **Post deployment window** containing all the details that are required to start using your application. After you deploy an application, the window opens and describes the“Next Steps” available. Send the launch URL to your users so they can access the application. URLs for viewing responses, charts, and other options are also displayed. The post deployment dialog is also displayed when you import and deploy an application.
- When you import an existing application, you can choose to remove users from theAccess page. Clearing the previously added users ensures only the people you add to the application have access. After importing an application, use theAccess page to review and modify the existing permissions.
- The editor for adding rich text to your application was updated.
- The Data Access Rest API contains additional filtering parameters to allow more specific refinement of the response data.
- The following API usability enhancements were added:
  - Simplified JSON requests and response structures.
  - New **metadata** option
- Automatic generation of swagger files for applications.
- A new Service Configuration window where you can quickly set up your application to make JSON service calls.
- The addition of a new configuration flag that disables the embedding of your application into other web sites.
- General usability enhancements include:
  - Carbon Copy and Blind Carbon Copy fields for Stage Action emails.
  - New Welcome text on the **Manage** page.
  - On the **Manage** page, you can access the Summary Charts URL. This link takes a user with the appropriate permission settings to the stand-alone Summary Chart page.
- Security fixes.
- General bug fixes.

## 8.6.2 { .section}

Support for the following versions:

- Oracle 12c and 11g
- 10.5
- 8.5.5
- Java 7
- Derby 10.10.2
- ICU 55.1

New features include:

- A new **Events** tab for easier management of custom JavaScript™ within an application. The Events tab displays all JavaScript used within an application.
- A new **Alterntative text** tag for Image and Media form items. To increase the accessibility of your form, you can now add alternative text to the Image and Media form items.
- You can now import a list of choices from a spreadsheet into **Select One**,**Select Many**, and **Dropdown** form items. The lists can be comma separated, or space separated. If you copy two columns of choices from a spreadsheet, the first column is set as the Displayed Value, and the second column set as the Saved Value.
- In the **Settings** tab, under **Files**, you can now download any previously uploaded file.
- A Java 2 Connector \(J2C\) provider is now supported for use in the HTTP Service Transport with .
- A new **openURL** query parameter so you can dynamically set a application to open at run time.
- The **Media** form item is supported in Google Chrome via HTML5.
- Two new JavaScript functions were added to the User Interface Objects: **setTabTitle** and**setTabTitleList**.
- The amount of Stage Action data an application can have has been increased.
- General and security fixes.

## 8.6.1 { .section}

Support for the following versions:

- Oracle 11g
- 10.5
- 8.5.5
- Java 7
- Derby 10.10.2

New features include:

- **Document Integration**: Where compliance or regulatory requirements mandate it, integrating captured data with existing documents can be an important part of the overall solution. These output documents can be provided for precise printing, document signing or archiving. Using a Service Configuration, you can map form items to PDF items. When the user clicks a button, the PDF is populated. For more information, see [Leap document integration](di_pop_doc_with_app_data.md).

- **Integration features**
  - **Render parameters**: Two public render parameters were added to provide additional portlet-to-portlet communication.
  - **Page refresh setting**: A new page refresh setting is available in the **Shared Settings**. This property lets you set whether the portal page is refreshed when the form is submitted.
  - **Support for non-default portal context root**: The Leap Portlet now supports portal with a non-default context root, or an empty context root.
  - **Script Portlet and DDC samples**: Two new samples are available for usingwith . Both samples are available on the developerWorks® wiki.
- **Additional in-product help**: If you're new to , blue help bubbles describe the basic function of each page or section, as well as provide additional help resources. Additional hover help, and context sensitive help were added throughout the application.
- **JSON is now supported in the**:
  - HTTP Transport
  - JavaScript Data Access Rest API
- **New JavaScript functionality**: New JavaScript functions were added to the User Interface Objects.
- **Forms Tab**:
  - **Moving items in an application**: You can now move form items between pages of a form.
  - **Order of forms in a application**: You can change the order of the forms within an application by dragging and dropping them in the Outline view. When the application is deployed and launched, the first form in the application becomes the default form seen by the user.
  - **Warning message on Save**: does not support multiple people editing the same application. If you and another user edit the same application, and the other user saves changes while you are still editing, a warning message is now displayed asking if you want to overwrite the changes made by the other user.
  - **Date item loads current date**: A new property is available for the**Date** field. When selected, if the user leaves the **Date**field empty, the current date is loaded upon form submission. If the user fills in the date field, the date supplied by the user is used.
  - **Single and Multi-Line entries uppercase**: This new feature, located in the**Basic** tab of the Properties window lets you automatically change the user's entered text into upper case letters.
  - **Hiding Table buttons for Add, Edit, and Delete**: In the**Advanced** tab for a **Table**, you can now set that no buttons are displayed with your table. The buttons can be enabled using JavaScript, if required.
- **Manage Tab**:
  - **Default sort order**: Default sort order was changed so the most recently changed applications are listed at the top. Now you can quickly find recently modified applications. Alphabetical sorting is still available, but no longer the default.
  - **Redeploy after saving**: When you edit an application, and save the changes you must redeploy the application for the changes to be implemented. A visual indicator is now displayed as a reminder when an application has changes that have not been deployed.
  - **Adding tags to an application**: When you create a new application, you can add tags at the same time. Tags are used to search for applications in the**Manage** screen. Previously, you could only add tags to your application after it was created and listed in the Manage tab. Tags are separated by spaces, so if you need to make a multiple-word tag, use an underscore between the words.
- **Access Tab**: The "All Authenticated Users" group cannot be added to any role that has **Edit** permissions. Users can still be assigned individually, or as groups, to roles with edit permissions. This prevents your application from showing up in the Manage Tab for all authenticated users, and from their applications appearing on your Manage tab. You see only the applications you created, or those to which you have edit permissions.
- **Rules**:
  - **Naming Rules**: You can now name and rename rules. Providing unique, descriptive names to rules makes them easier to find when building your application.
  - **See which item is used in a Rule**: When a form item has a rule enabled, the Rules icon for the item contains a check mark. The check mark lets you quickly see which form items are involved in a rule.
- **Stages**:
  - **Stage Description**: When you create a new Stage, you can add a detailed description. Adding descriptions is useful if you will have several similarly named stages that perform slightly different portions of the workflow.
  - **Rich Text Action Completion Message**: The Action Completion Message is now a rich text field.
  - **Success message after submission**: When a user completes and submits a form, the new default is to take the user away from the form and display the Action Completion Message. This reduces user confusion as they no longer see an empty, reloaded form on the screen. The existing options for the action taken upon form submission are still available in the**Edit Form Properties** window.
- **View Responses**:
  - **Individual Print, Email, and Delete buttons added**: Print, email and delete buttons were added to each record row, so you can access them without opening each individual record.
  - **Email option contains the link to the record**: The email operation emails the link to both print and launch the record.
  - **New fields added to Responses screen**: “Created on”and “Last Updated By” were added to the table so you can see additional information on each submitted form.
  - **Selected results open in a new window**: When you click on a submitted record, it opens in a window, rather than in a side pane.
  - **Default view changed**: When you click the **View Responses** link, the default view is now **Responses**, rather than**Summary**.
- A number of upgrade routine fixes, accessibility, and usability changes were implemented.
- Values entered into the password item are not stored in your application. Since the password is never stored, it is never exported or shown in any field. The password field is empty when the form is rendered in its next stage. Using the password for calling server-side services during stage transitions still work as the value is included as part of the submitted data and not stored as part of the application record.
