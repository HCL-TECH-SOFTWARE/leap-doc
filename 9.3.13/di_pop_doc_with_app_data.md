# {{shortProductName}} document integration { #generatingfillablepdfs .concept }

{{shortProductName}}'s document integration feature lets you use previously built PDF files and populate them with data captured by {{shortProductName}}.

Where compliance or regulatory requirements mandate it, integrating {{shortProductName}} captured data with existing documents can be an important part of the overall {{shortProductName}} solution. These output documents can be provided for precise printing, document signing or archiving.

You can now use a {{shortProductName}} form to collect user data, and display the information in a PDF. This process requires four steps:

1.  Load an existing PDF into {{shortProductName}}.
2.  Create a form that contains information fields that align with fields in the PDF.
3.  Create a service description by mapping fields from your form to fields in the PDF.
4.  Add a button that the user can click to populate and display a PDF.

!!! note
    For the {{shortProductName}} document integration, PDFs must allow the input of information to be populated by data that is collected in a {{shortProductName}} application.

-   **[Adding a PDF to {{shortProductName}}](di_adding_pdf_to.md)**  
The following instructions describe how to add a PDF to {{shortProductName}}.
-   **[Mapping form items to PDF fields](di_mapping_form_items_to_pdf_fields.md)**  
The following instructions describe how to create a Service Configuration to map {{shortProductName}} fields to fields in an existing PDF and, when triggered, returns the filled PDF to the user.
-   **[Mapping form items to PDF fields and storing the filled PDF](di_mapping_form_items_to_pdf_fields_and_attaching.md)**  
NEW - The following instructions describe how to create a Service Configuration to map {{shortProductName}} fields to fields in an existing PDF and, when triggered, stores the filled PDF as an attachment to the record.
-   **[Creating the PDF trigger](di_creating_the_pdf_trigger.md)**  
The following instructions describe how to create a trigger that calls the PDF service, and triggers the service when the user clicks the button.
-   **[Document integration usage details](di_usage_details.md)**  
The following usage details describe the best practices and limitations for integrating your {{shortProductName}} application with a PDF.

**Parent topic:** [Building Apps](cr_creating_and_managing_toc.md)

