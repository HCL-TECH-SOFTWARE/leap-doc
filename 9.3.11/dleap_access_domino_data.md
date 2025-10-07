# Accessing data from Existing Domino Applications

Data from existing Domino Databases, that are co-located with Domino Leap, may be accessed by your Domino Leap application. A Service Configuration is used to interact with an existing Domino Database. The operations are: List **View Entries**, **Find View Entries**, **List View Categories**, **Read a single Document**, **Create a Document**, **Update a Document**, **Delete a Document**, and **Run an Agent**.

## List View Entries and Find View Entries

**List View Entries** returns all the entries in the specified View.

**Find View Entries** returns all the entries where the value of the “Sort By” column equals the “Search Value”. This service is for filtering down the View entries to those that match a specific value.

The following apply for both **List View Entries** and **Find View Entries**:

- The Views in the selected database will be populated into the “Select View” field. Choose the View.

- If the View is sorted, then the “Select Column to sort by” and “Sort direction” will be available. You may choose to sort the results by a specific column.

    !!! note
        If you want to map the sorted column dynamically to a field in your form, leave the “Select Column to sort by” empty. If you set the “Select Column to sort by” on the “1. Select Service” tab, then the “Sort By” parameter will not be available on the “2. Inputs” tab. If you set the “Sort Direction” on the “1. Select Service” tab, then the “Sort Direction” parameter will not be available on the “2. Inputs” tab.

- The columns of the selected view will appear in a table. Each column will default to a datatype based on the corresponding field in the first document in the view. Ensure the datatype matches the actual datatype that is in the Domino application. For example, if it is a date only field in Domino then select “Date” as the data type when configuring the service.

    !!! note
        This is an important step - Domino Leap does not allow mixing datatypes. If you want to map a date column from the service to a date field in your form, you must set the data type to “Date”. Domino Leap will not convert or transform the data being returned from the service.

- The results of this service are paginated and the default page size is 50. You may change the page size, up to a maximum of 1000, by mapping a value to the “Page Size” input parameter. You may change the results page by mapping a value to the “Page” input parameter.


## List View Categories

**List View Categories** returns all the categories in a View at the specified level.

- If you call this service and leave the “Category Name” empty it will return the list of first-level categories.

- If you call this service and map the “Category Name” to a category, it will return all the next-level categories. If you specify a sub-category the “Category Name” must be the full path to the sub-category. For example: “Education\Online” or “Education\Online\Programming\JavaScript”.

- The results of this service are paginated - the default page is 1 - and the default page size is 50

- The service returns the category name, count of immediate sub-categories, the parent category and the category path as output parameters.


## Read a single Document

**Read a single Document** returns the values of all the items in the specified document. The document is identified by providing the Universal ID (UNID).

- The Forms in the selected database will be populated into the “Select Form” field. Choose the **Form**.

- The fields in that form appear in a table. Each column will default to a datatype based on the form field in Domino. Change the datatype of each column to match the data you expect to return or how it is to be mapped within the form.

    !!! note
        This is an important step - Domino Leap does not allow mixing datatypes. If you want to map a date column from the service to a date field in your form, then you must set the data type to “Date”. Domino Leap will not convert or transform the data being returned from the service.

- You may add additional fields that may be in your document but not part of the selected form. Click **+ Add Field** and enter the field name and datatype and click OK.

    !!! note
        You may add any field from the document, including “$...” fields.

- This service automatically includes the UNID, when the document was last updated, the Notes URL, and the document’s size as output parameters.

    !!! note
        Mapping Content from Notes/Domino RichTextItems: A service that returns content from the **RichTextItem** of a Notes/Domino document can be mapped to two types of Domino Leap items: a **Rich Text Entry** field, or an **HTML** item. Mapping to a **Rich Text Entry** field now allows that content to be edited, and a subsequent service call can write the updated data back to the rich text field on the source document. At this time, you are limited to updating on one **Rich Text Field** on the source document in a single service call.


## Create a Document

**Create a Document** creates a document in the specified database based on the selected Form.

- The Forms in the selected database will be populated into the “Select Form” field. Choose the **Form**.

- The fields in that form appear in a table. Each column defaults to a datatype based on the form field in Domino. Change the datatype of each column to match the data you expect to return or how it is to be mapped within the form.

    !!! note
        This is an important step - Domino Leap does not allow mixing datatypes. If you want to a map a date field in your form to a date column from the service, then you must set the data type to “Date”. Domino Leap will not convert or transform the data being passed to the service.

- You may add additional fields that may be in your document but not part of the selected form. Click **+ Add Field** and enter the field name and datatype and click **OK**.

    !!! note
        You may add any field from the document, including “$...” fields.

- The document fields to be updated must be mapped to items on your form.

- If you set **Compute with form** to true, the document is validated by executing the default value, translation and validation formulas, if any are defined in the document form. Not all the business logic on the Domino form is executed. For example, it does not raise the QuerySave event as you would expect when saving a document in the Notes client, nor does it raise WebQuerySave.

- If you set the **Compute with form raise error** to true, then an error is raised if the validation fails. If false, no error is raised.

    !!! note
        If you use compute with form, it is recommended that you also use **Compute with form raise error**, which causes a validation error to cancel the operation. The **Compute with Form** flag (no Raise Error) saves the document in spite of validation errors.

- The service returns the universal id of the created document and a boolean that indicates the result of the compute with form operation.

## Update a Document

**Update a Document** updates the fields of a document in the specified database.

- The Forms in the selected database will be populated into the “Select Form” field. Choose the **Form**.

- The fields in that form appear in a table. Each column defaults to a datatype based on the form field in Domino. Change the datatype of each column to match the data you expect to return or how it is to be mapped within the form.

    !!! note
        This is an important step - Domino Leap does not allow mixing datatypes. If you want to a map a date field in your form to a date column from the service, then you must set the data type to “Date”. Domino Leap will not convert or transform the data being passed to the service.

- You may add additional fields that may be in your document but not part of the selected form. Click **+ Add Field** and enter the field name and datatype and click OK.

    !!! note
        You may add any field from the document, including “$...” fields.

- The document fields to be updated must be mapped to items on your form.

- If you set “Compute with form” to true, the document will be validated by executing the default value, translation and validation formulas, if any are defined in the document form.

- The “Universal Document ID” is a required input as this identifies the document to be updated.

- The service returns a boolean that indicates the result of the compute with form operation.


## Delete a Document

**Delete a Document** in the specified database.

- You must map the Universal Document ID input to a field on your form that contains the UNID of the document to be deleted.

- If you set **Force Delete** to true, the document is removed even if another user modifies the document after your program opens it.

- There are no outputs for this service.


## Run an Agent

**Run an Agent** triggers the specified agent.

- If the database contains any agents, they will appear in the “Select Agent” dropdown.

- If you set the “Universal ID” input, it will be passed to the ParameterDocID property of the agent.

- There are no outputs for this service.

    !!! note
        This agent will be executed at the time the service is triggered, therefore if the agent does anything to the document it must already exist.

- The Run an Agent operation assumes detailed knowledge of the target agent. For example, an agent might be designed to run as the web user, as the agent author, or as a specific third-party (neither user or author). The Domino Leap application author needs to consider the "run as" identity and other security settings in the agent itself.

- When the Run an Agent operation executes, it executes synchronously inside a Domino HTTP request. Depending on the design of the agent, it could run for a long time. The Domino Leap app author should consider the implications for the end-user experience and for a busy server handling several simultaneous requests.

**Parent topic:** [Incorporating web services into your applications](cr_using_apps_as_services_toc.md)