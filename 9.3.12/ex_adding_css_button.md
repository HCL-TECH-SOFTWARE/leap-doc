# Adding CSS to buttons in your application { #addingcsstobuttons .task }

The following instructions explain how to apply CSS to table buttons.

## Procedure

1. Create a {{fullProductName}} application.

2. Add a Table to the canvas.  

3. In the **Table properties**, set the **Button Style** to **Show Labels**.

4. Navigate to the **Style** tab and add the following custom CSS:

    ```css
    .lfMn.lotusui30dojo .aggregationListBtn:not(.lfMn.lotusui30dojo .lfFormBtnDisabled.dijitButtonDisabled){
      background-color: gold;
      color: black;
      border-style: solid black;
    }
    ```

    !!! note
        - `.lfMn.lotusui30dojo` `.aggregationListBtn` is the class for a Table's enabled button like the **Add** button. 
        - ` lfMn.lotusui30dojo` `.lfFormBtnDisabled.dijitButtonDisabled` is the class for a Table's disabled button. By default, **Edit** and **Delete** are not clickable.

5. Save and deploy the application.


**Parent topic:** [Using custom style sheets](ex_css_toc.md)

