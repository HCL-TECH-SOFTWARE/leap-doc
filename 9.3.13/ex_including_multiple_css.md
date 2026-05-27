# Including multiple CSS files in your application


You can add multiple custom cascading style sheet \(CSS\) themes to your {{fullProductName}} application.  For example, use `style1.css`  for table styling, and `style2.css` for button styling.

Adding custom cascading style sheet \(CSS\) themes personalizes applications to match your organization’s branding.

## Procedure

1. Ensure that `secureJS` is set to false in the configuration settings. This setting is in `VoltConfig.nsf` on the server and disables JavaScript™ security restrictions. 

2. Ensure the `.css` files are already uploaded to **Files**. For example. `style1.css`, `style2.css`.

3. In the application onStart event, add a global function: 

    ```javascript
    app.getSharedData().loadStyle = function (url) {
      var head = document.getElementsByTagName('head')[0];
      var link = document.createElement("link");
      link.rel = "stylesheet"
      link.type = "text/css";
      link.href = url;
      // Fire the loading
      head.appendChild(link);
    }
    ```

4. To utilize the global function, use it in a form onLoad event:

    ```javascript
    // get url of styles uploaded in the Files
    var url = app.getStyleBaseURL() + "/style1.css"
    var url2 = app.getStyleBaseURL() + "/style2.css"

    // use global function to load styles 
    app.getSharedData().loadStyle(url); 
    app.getSharedData().loadStyle(url2);
    ```

5. Save and deploy the application.

    !!! note
        If the `.js` file resources are not uploaded to Files, or located online, adjust the code below.

      ```javascript
      // get url of online styles
      var url = "https://host_name/sample-css-files/style1.css"
      var url2 = "https://host_name/sample-css-files/style2.css"

      // use global function to load multiple styles 
      app.getSharedData().loadStyle(url); 
      app.getSharedData().loadStyle(url2);
      ```

    !!! note
        To see the style sheet that is applied to your application, either preview, or save and deploy the application.

See [Creating customized Cascading Style Sheets](ref_customized_css.md) for information about creating your own custom CSS.

**Parent topic:** [Using custom style sheets](ex_css_toc.md)