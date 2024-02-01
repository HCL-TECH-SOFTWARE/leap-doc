# Document integration usage details {#documentintegrationusagedetails .concept}

The following usage details describe the best practices and limitations for integrating your Leap application with a PDF.

-   **Selecting PDF types**:
    -   PDFs must allow the input of information to be populated by data that is collected in a Leap application. Adobe™ Acrobat Pro is the primary tool that is used for creating PDFs where you can complete fields, and can be used to reliably create or modify existing PDFs to make them compatible with the Leap document integration feature.
    -   In some cases, Adobe Acrobat Reader extensions are removed by Reader after the document is populated.
    -   XFA PDFs have partial support when they have “compatibility mode” enabled.
    -   Encrypted PDFs cannot be populated.
    -   Some PDF documents are intended only for printing and have no data entry fields. These PDFs cannot be populated.
    -   A number of freely available PDF authoring tools on the web do not create compatible PDFs. Some PDF documents that are created or modified with these tools might appear to have direct text entry support but do not allow completion of fields.
    -   If a PDF has limitations that make it unusable for populating with data from Leap, you can still attach the PDF to the form and it is returned unmodified. This is useful if you want to return a static PDF containing detailed instructions.
    -   Populating fields in a signed PDF document results in a validation warning message that is displayed by the PDF Reader. The warning message tells users unsigned changes were added after the document was signed.
    -   When you work with languages that contain extended character sets, be sure to match the language of the Leap form with the Language/Font of the PDF item. Any character or glyph that is missing from a font is omitted from the value that is passed.
    -   The built-in PDF viewer on iOS/Safari does not properly render values of filled PDF's. This is an iOS/Safari limitation.
-   **Mapping information**:
    -   Values can be mapped to PDF **Text Fields** that are marked as readonly. You can populate a PDF from values that are collected in the Leap form, while the PDF remains unmodifiable through direct entry.
    -   The design time exercise of creating a map to indicate how data moves from application to the PDF are made much easier when items on both sides are properly named. When you use the Leap mapping dialog, if items in the PDF do not have recognizable names, Adobe Acrobat Pro can be used to modify the PDF.
    -   Take care to understand the format and constraints of the item you are mapping to and from. In some cases, a poorly matched map results in a blank item in the PDF because no value is mapped. For example, mapping a **Number** into a PDF **Date Text Field**, or mapping multiple selections from a **Select Many** choice item into a PDF **Radio Group**. In other cases, a value appears in the PDF but might result in constraint violations within the PDF. For example, mapping an unconstrained **Single-Line Entry**into a PDF **Field**.
    -   Multi-lined values cannot be mapped to single lined text fields in a PDF.
    -   The **Export Values** for PDF choice type items can be determined by inspecting the PDF with an editing tool. The **Export Values** are also displayed as part of the **Description** property in the extra information hover text within the Leap mapping dialog. To see the **Export Values**, hover over the information icon next to any PDF item in the list to be mapped. For a successful map, the **Saved Value** for the Leap item should be adjusted to match the **Export Value**.
    -   To map choice items, the **Saved Value** for the selected choice must match the **Export Value** for the available choice in the PDF item. The **Export Value** is used as an indicator of whether a particular choice in the item is marked as selected, or turned “on”. This note is applicable to Leap choice items such as **Select One**, **Select Many**, **Drop Down**, **Survey**, and **Choice Slider**.
    -   When you map a **Check Box** to a PDF **Check Box**, the **Export Value** is automatically determined so no special consideration needs to be made around matching the Export Value.
    -   **Select Many**
        -   A **Select Many** can be mapped into a PDF **Radio Group**. However, configure the**Select Many** with a constraint that allows only one choice selection so the constraints of the PDF **Radio Group** are not violated
        -   A **Select Many** should **not** be mapped to a cluster of PDF **Check Boxes** if the PDF **Check Boxes** do not have unique **Export Values**. In this case, the Leap form might need to be altered to replace the **Select Many** item with a cluster of individual **Checkboxes**.
        -   A **Select Many** maps well to a PDF**List Box Multi-Select** but can also be mapped to a cluster of PDF **Check Boxes** by creating multiple maps. One map from the **Select Many** to each **Check Box** in the cluster. When mapping from a **Select Many** to a PDF **Check Box**, the **Saved Value** of a selected choice must match the **Export Value** of the PDF **Check Box** for the PDF check box to be turned on.
    -   Each question in a **Survey** must be mapped separately, and must use the same rules for mapping as a **Select One** or **Select Many**.
    -   Leap tables are repeating rows of data and cannot be mapped directly into a PDF.
    -   Some Leap items that cannot be mapped are **Image**, **HTML Fragments**, **Text**, **Button**, **Line**, **Media**, **Web Link**, **Attachment**, **Page Navigation**, **Section**, and **Tabbed Folder**.
    -   Some PDF items that cannot be mapped are **Button**, **Digital Signature**, **Image**, and **Text**.

**Parent topic: **[Leap document integration](di_pop_doc_with_app_data.md)

