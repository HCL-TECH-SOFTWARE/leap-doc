# Accessibility features for application designers 

HCL Leap contains accessibility features so users with disabilities can create forms and applications.

To make designing forms and applications easier for users with disabilities, Leap has the following keyboard shortcuts:

#### Adding items to your form

To add items to your form from the Palette, set focus on the form item with the Tab key and press Enter. The item appears on the form where indicated by a blue line.

#### Focus indicator

When a form item has focus the background changes color, and the area that is occupied by the form item is defined by a colored line.

#### Item triggers

When an item has focus, you can trigger it by pressing the Enter key or space bar. The browser that you use determines whether you must press the Enter key or space bar.

#### Tab key

You can navigate to any visible form item, link, or menu by pressing the **Tab** key.

#### Tab navigation

The Properties side panel contains multiple tabs. To navigate between tabs, use the arrow keys.

#### Tab order of form items

When you place items on a form, the tab order is set based on item placement. If you insert a form item before existing items, the tab order is automatically reset. You do not have to manually configure tab order when you insert additional items into a form.

#### Navigating between Palettes

You can navigate between the Common, and Specialized palettes. When the focus is on one Palette use any arrow key to collapse the open Palette and expand another one. If you want to switch palettes while focus is on a form item, you must use the Tab key to move to the palette name, then navigate with the arrow keys. You cannot navigate between palettes when a form item has focus.

#### Keyboard commands for common items

Leap has three menu items: **Save**, **Preview**, and **Cancel**. The following keyboard commands are available so you do not have to navigate away from your form.

  - Save: Ctrl+s
  - Preview: Ctrl+e
  - Cancel: Ctrl+q

When designing forms the Properties side panel contains a box titled “Accessibility - Alternative text ID”. Use this box to provide a text description that is used by accessibility tools to describe the item.

The following [WAI ARIA](http://www.w3.org/TR/wai-aria/) attributes are automatically added to form items when you design forms:

-   aria-labelledby and Aria-label are added to fields to associate the correct label with each field.
-   aria-describedby are added to fields where more description is needed to describe the function of a field.
-   aria-required is added to inform a user that the field is mandatory.
-   aria-invalid is added to fields when the value is not valid.
-   aria-alert is used with Aria-invalid in error messages. Screen readers read the Aria-alert text to the user.
-   aria-valuemin and aria-valuemax are used to denote if the file has an acceptable value range. If the value is outside the range, the aria-invalid attribute is set.

**Parent topic: **[Accessibility overview](ac_experience_builder_accessibility.md)

