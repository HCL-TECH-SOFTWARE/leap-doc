# Viewing submitted responses { #viewingsubmittedresponses .concept }

After users complete and submit forms, you can view the submitted responses. Responses are available compiled into summary charts, or as a list of individual forms.

To review user submitted responses, click **View Data** for a specific application. The View Data page opens, and you are presented with two options to view the submitted results:

-   Viewing individual responses on the **View Data** page. The default is to see a list of responses.
-   Viewing a summary of response data displayed in either a pie, bar chart, or table on the **Summary** page.

**Viewing responses in a list**

The following features are available on the View Data page:

-   When you click on a response, it opens in a window so you can see all information easily.
-   Print, email, and delete buttons are available on each row. You can access these buttons without having to open each individual response.
-   If you choose to email the link to a response, the recipient receives not only a method of printing the response, but also a link to open and view the response. To obtain the View Data URL link
    1.  On the **Manage** tab, click the arrow head to the left of the application name.
    2.  The application information window expands and displays the URL of the application. In the **URL Links:**section, change **Launch Form** to **View Data**.
    3.  Copy the URL and paste it into a web browser, or disseminate it through email.

**Viewing summary responses in a chart**

Charts are available for the following form items:

-   Check Box
-   Currency
-   Drop Down
-   Number – both decimal and integer
-   Select Many
-   Select One
-   Survey

If there are no charts to display, or if you do not have the required access to view the submitted data, an error message is displayed. Access is configured when the application is created. The same access permissions that allow users to view and edit the form are used to display submitted results.

The following list is a **Summary** of page chart features:

-   **Display type** – By default, charts are displayed as pie charts. You can select to have the chart display as a bar chart.
-   **Selecting which charts to display** – The **Summary** page displays charts for the first 10 form items in a form. If your form contains more than 10 items that can be displayed as charts, click **Customize** to add or remove form items from the Summary page. Selected charts are remembered as a personal setting from session to session and are also reflected in the distributed Share URLs.
-   **What a chart means** – The question on which the results are based is displayed with each chart. If the form item charted is a survey, the survey title is displayed with each of the survey questions.
-   **Displaying choice results** – Charts display the most popular 10 answers for a question. If there are more than 10 choices available to a user, the most popular 9 are displayed and the rest of the responses are grouped into an **Other** category.
-   **Displaying numerical results** – If the form item requests a numerical value from the user, the first 10 values are displayed. If there are more than 10 submitted responses, the numerical values are grouped into **Ranges**. Although the range is automatically determined, some decisions for the range are based on form item configuration when the application is designed.
-   **Filtering data** – You can filter the results that are displayed in the charts by clicking **Filters** and setting parameters. The charts display only the filtered results. Clearing the filters returns the original data set. You can also quickly filter data by clicking a section of the chart. The filter that results from the click is presented in the search dialog prior to application. Filters are applied to the overall set of submitted records and are therefore reflected in all charts. Filters are remembered as a personal setting from session to session, and are also reflected in any distributed Share URLs. Note that Filtering and Quick Filtering is not supported for the **Select Many** form item.
-   **Sharing charts** – You can share the complete set of charts or individual charts by clicking **Share**. From the **Share** options, select whether to email or embed the URL of the chart. When you share a chart, the chart information is not static, and will continue to reflect new submissions. Any filters applied to the charts are also included when the chart URL is shared.

    !!! note
        When you share charts, the people to whom you send the chart URL must have appropriate access permissions. Otherwise, an error message rather than the chart is displayed.

-   **iFrame embedding of charts** – You can share charts by embedding the charts into an iFrame. You can use the embedding feature to show a chart on your own HTML page, or with an iFrame capable Portlet, such as the Web Clipping portlet. The iFrame content is also used to host the chart in a {{shortProductName}} application using the **HTML** form item.
-   **Statistical data provided** – Each chart displays the number of times the question was answered from the total number of submitted responses. If questions in your form are not mandatory, you can see how many people answered the question, and how many did not answer the question. Charts that are based on Number or Currency form items display statistical data, such as the minimum, maximum, range, and average of the submitted values.
-   **Reflecting new data submission in existing charts** – Click **Refresh** to reflect newly submitted data in existing charts.

**Viewing individual responses** – A list of submitted responses is displayed in a table. By clicking the row of a response, the user’s submitted form is displayed in the Application View frame. If the form contains workflow elements, such as approving or denying the form, buttons that are associated with the workflow are provided for you.

**Parent topic:** [Application Management](cr_application_operations_toc.md)

