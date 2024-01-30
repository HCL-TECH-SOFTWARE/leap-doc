# Creating a formula from the Settings tab {#creatingaformulafromthesettingstab .task}

The Settings tab contains a Formula section from which you can view and create formulas.

When you select the Formulas menu option, you are shown the formulas for your form. They are divided into two categories: General Formulas and Item Formulas. **Item Formulas** is a list of the formulas created in the form using the Properties side panel. **General Formulas** are complex formulas created on the Settings tab.

**Note:** If you are creating a formula to assign a string value to a **Time** form item, the content of the string must be based on a 24-hour clock. If the input value is not in a valid 24-hour clock format, the resulting value will not be correct.

To create a complex formula:

1.  Click **Add Formula**.

2.  Add a title and description to your formula.

    Although the description is optional, it is useful for users to distinguish between several similarly titled formulas.

3.  Select the function from the list of available options.

    The available options are:

    -   **Add** – Adds two values together.
    -   **Assign** – Assigns a value to the specified form item.
    -   **Table Average** – Calculates the average column value of a table.
    -   **Concatenate** – Concatenates two values together into a single string.
    -   **Power** – Raises power of one value to another value.
    -   **Table Max** – The maximum column value of a table on the form.
    -   **Multiply** – Multiplies two values together.
    -   **Minus** – Subtracts one value from another value.
    -   **Table Sum** – The sum of a column of a table.
    -   **Table Count** – The number of rows in a table.
    -   **Divide** – Divide one value by another.
    -   **Table Min** – The minimum column value of a table.
    After you select a function input areas, and a result area are shown.

4.  Click either the **Input 1** field.

    -   Select a form item from the list.
    -   Click **Or, Enter a Number**. Enter a number in the **Value:** field, and click **OK**.
5.  Click either the **Input 2** field.

    -   Select a form item from the list.
    -   Click **Or, Enter a Number**. Enter a number in the **Value:** field, and click **OK**.
6.  Click **Result** to select where the result of the formula is shown to the user.

    **Note:** If your formula contains errors, an error icon is shown. Ensure that a formula is free of errors before applying it to a form item.

7.  To create complex formulas, click the **Add** green plus icon.

    A second set of inputs is shown. Set values for the inputs and the result to create the second function. You can add as many additional functions as required to complete your formula.

    The formula runs when there are changes to the item. If you do not want the formula to automatically run, clear the check box for **Automatically run this formula when there are changes to item values**.

    You can change the order of functions in a formula by clicking the **Move up** or **Move down** arrows located.

8.  Click **OK** to save and apply the formula.


Save and preview your form to test the formula.

**Parent topic:**[Adding formulas to your application](cr_adding_formulas_toc.md)

