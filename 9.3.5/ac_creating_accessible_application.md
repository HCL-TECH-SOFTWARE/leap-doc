# Creating an accessible application {#creatinganaccessibleapplication .concept}

When you create a form or application, the following information helps you design an accessible form for users with disabilities.

HCL Leap is designed to make building accessible forms easy. For example, the tab order of form items is set to start at the first item on the page, and work through consecutive items. You do not have to reset the tab order if you must add items to the beginning of a form. There are several things that you can do to make your forms more accessible to users with disabilities:

-   During the creation of your application, accessibility standards, such as [WCAG 2.0](http://www.w3.org/TR/WCAG20/), should be considered with regards to layout and content. Leap does not prevent authors from creating non-accessible forms.
-   When you add items to your form, give each form item a clear description or name. Screen readers read the name that is associated with a form item. You can also use a Text item as a data label instead of the field provided. For more information, see [Using a Text item as a label](ac_using_text_item_as_label.md).
-   Add hints to each form item by modifying the **Add hint** field. The Hint provides more information when read to the user. For example, if your form has a **Name** field, the hint tells the user your preference for how to enter their given and surnames.
-   Text blocks are not automatically part of the tab order. Screen readers do not put focus on text blocks, and your users might miss vital information. To ensure that text information is not omitted, select the text item, in the properties side panel, select the check box for **Add to tab order**. The text is added to the tab order, and is read by screen readers.
-   If you add images or media items to your forms, open the Properties side panel and add descriptive text to the **Alternative text** property. A screen reader uses the alternative text to describe the image or media item to the user.
-   You can add text items to your form and have them associate with other form items. You can use this technique to create formatted titles for your form items. However, you must link the text item and the form item together. For example, you have a Select One item on your form. You want its title to be rich text so it can have a color, background, and format different from the default title. You add the title with the Text form item, which gives the formatting you want. However, the text item is not read by the screen reader, and the user might not know what the choice list represents. To ensure that the **Text** field is read by a screen reader, go to the choice list Properties side panel. Insert the name of the **Text** field into the **Accessibility – Alternative label ID** field. A screen reader reads the appropriate text for the choice list.
-   When using the new dynamic layout, it might be necessary to group items into Sections to convey the proper meaning to users. For example, when creating a custom label via the alternative text ID option.
-   When using **Sections**, if a label exists, it provides a navigation landmark using WAI-ARIA that is available to assistive technologies. For more information, [WAI\_ARIA roles](http://www.w3.org/WAI/PF/aria/roles).

-   **[Using a Text item as a label](ac_using_text_item_as_label.md)**  
For accessibility ease of use, users might prefer to see the title of an entry field to the side of the field, rather than above the field.

**Parent topic:**[Creating and managing applications](cr_creating_and_managing_toc.md)

