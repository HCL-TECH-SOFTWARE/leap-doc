# Creating an application from an excel spreadsheet {#creatinganapplicationexcel .task}

Leap allows you to create an application from an excel spreadsheet, automatically creating the widgets and importing the data found in the spreadsheet.

The following steps describe how to prepare a spreadsheet that you want to import into Leap and how to create the application from the spreadsheet.

1.  Prepare the spreadsheet for importation.

    Points to consider:

    -   Each sheet in the spreadsheet file will be turned into a form in a new application.
    -   The first non-empty row in the sheet will be considered the 'header row'.
    -   If all the sheets in the spreadsheet have no header rows, the import will fail.
    -   The contents of a header row cell will be the name of the widget for that column.
    -   There can be a horizontal gap of a single cell between the header row cells. If there is a gap of more than one cell in the header row, then the cells to the right of the gap will not be processed.
    -   Header titles get processed to only have valid characters and then are assigned to the corresponding widget name. If after processing there are too few characters, the widget gets a default name.
    -   The contents of cells under the header row cell will be used for the data import process.
    -   There can be one gap of up to two columns in the data and header row.
    -   There can be a gap between the left-hand edge of the spreadsheet and the header row.
    -   There can be a gap between the header row and data.
    -   Parsing of rows will stop after parsing 10 empty rows in a row.
    -   If the column under a non-blank header row cell is empty, then the resulting widget will be a single line entry.
    -   Web links must have https:// or http:// at the beginning of the URL.
    -   Select many widgets can be created when the contents of a cell contains \[value\],\[value\],\[value\].... with no spaces between values and commas. Values cannot be duplicated, and the cell cannot begin or end with a comma. Commas are used as delimiters for multi select widgets; therefore, any comma will not be part of the value itself and will separate values.
    -   For a widget to be selectable \(i.e. a Dropdown, Select One, Select Many, etc.\), then the number of possible values must be greater than one and less than a certain value, currently set at 30.
    -   If there are only numbers and currency cells in a column, then the column widget type will be whichever count is greater.
2.  Log on to Leap. By default you see the **Manage** window which displays the **New Application** button, any previously created applications, and any applications to which you have edit permissions.

3.  Click **New Application**.

    A dialog will open, which provides a choice to create an application from a blank canvas or from an Excel spreadsheet. The rest of this topic describes how to create an application from an Excel spreadsheet. For a topic covering creating applications from a blank canvas, see [Creating an application](cr_creating_application_overview.md).

4.  Click **From Spreadsheet**.

    An upload file dialog will open. Upload the prepared excel spreadsheet here, then click **Next**. Leap will parse the spreadsheet one sheet at a time. Each column in the main data range will be used to create a widget in the form. Leap will go through the rows of each column within that range, then attempt to assign a type based on the contents of the cells of the column.

5.  Choose the fields, names, and types of your application.

    On the next dialog, the names of sheets \(forms\) and columns \(widgets\) can be changed. Additionaly, the type of the created widgets can be changed \(within limits of the imported data\). When the names and types are set up properly, click **Next**.

6.  Enter the name of the new application, and \(optional\) a description or tags for the application. Click **Create**.


**Parent topic: **[Creating and managing applications](cr_creating_and_managing_toc.md)

