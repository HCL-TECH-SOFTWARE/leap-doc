# Creating rules in your application 

Rules help you gather the correct information from users and organize your information after data is entered in a form. You can create composite rules that govern how your form, and the data in your form behaves.

With the Rules feature, you can create a dynamic user experience that ensures accurate data capture, and enforcement of business rules. Rules allow you to guide the user through the form by hiding questions, or pages, that are not relevant. Rules also allow you to enforce your business validation rules within the form to ensure that data is valid before the form is submitted. The following steps describe how to set rules that require users to enter more information depending on how the first question is answered.

Rules can be set for the following conditions:

#### Show or Hide

You can set data entry items, buttons, and containers to be hidden, or visible.

#### Enable or Disable

You can set buttons and data entry items as enabled or disabled.

#### Valid or Not Valid

In a data entry item, such as a **Single Line Entry** field, you can set conditions on what type of information is acceptable. For example, in a timesheet application, you can set a rule that the check-out time cannot occur before a check in time.

#### Required or Not required

You can choose whether you want data entry items to be mandatory, or optional.

#### Additional general information on Rules

-   You can add multiple Boolean operators, such as AND, and OR, for each rule. However, you cannot mix the two conditions in a rule.
-   You can name and rename rules. It is useful to give each rule a unique and descriptive name. If you have several rules with similar operations, a descriptive name lets you quickly find the specific rule without having to open each one to view the details.
-   You can search rules based on form item.
-   To set a new rule, use the **Edit rules** icon in each form item. You can also create rules for pages and buttons. You can use the icon to open a rule and edit it.
-   After a rule is set, a checkmark appears on the Rule icon for the form item, as well as any form item involved in the rule. This makes it easy to see which form items are used in rules.

HCL Leap warns you if you attempt to delete a form item that is used in a rule. If you agree, you delete the rule. If you duplicate a field, the rule is duplicated with it.

**Note:** When you set rules for Number or Currency form items, you must set the default value of the form item to zero in the **Properties** side panel. In the **Properties** side panel, set the minimum value to zero. If the Number or Currency form item is blank, it does not default to zero, and any rule you set does not work properly.

-   **[Setting rules on form items](ru_set_rule_on_form_items.md)**  
You can set rules that govern how form items appear in a form.
-   **[Setting rules on pages in an application](ru_setting_rules_on_pages_in_an_application.md)**  
You can set rules that govern how pages are shown or hidden in a form.
-   **[Setting rules on Stages](ru_setting_rules_on_stage_actions.md)**  
You can direct the workflow of an application by setting rules on buttons within Stages.

**Parent topic: **[Creating and managing applications](cr_creating_and_managing_toc.md)

