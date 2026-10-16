# Running third party libraries 


Any `.js` file that is added to an application through **Settings** \> **Files** is automatically loaded when the application runs. In some cases, multiple JavaScript™ (JS) file is required. For example `simplePerson.js` can define the Person properties and methods, `simpleCar.js` can define the Car properties and methods, and `utility.js`  can contain shared or custom utility functions.

## Adding multiple JS files in an application

To add multiple JS files in your application, you may use the following steps below.

## Procedure

1. Ensure that `secureJS` is set to false in configuration settings. This setting is located in `VoltConfig.nsf` on the server and disables JavaScript™ security restrictions. 

2. Ensure `.js` files are already uploaded to **Files**. For example, `simplePerson.js`, `simpleCar.js`.

3. In the application onStart event, add a global function: 

    ```javascript
    app.getSharedData().loadScript = function (url, callback) {
      var head = document.getElementsByTagName('head')[0];
      var script = document.createElement("script");
      script.type = "text/javascript";
      script.src = url;
      script.onreadystatechange = callback;
      script.onload = callback;
      // Fire the loading
      head.appendChild(script);
    }
    ```

4. To utilize the global function, use it in a form onLoad event:

    ```javascript
    // get url of js uploaded in the Files
    var url = app.getFileBaseURL() + "/simpleCar.js"
    var url2 = app.getFileBaseURL() + "/simplePerson.js"

    // use global function to load multiple js
    app.getSharedData().loadScript(url,function(){ 
    app.getSharedData().loadScript(url2,function(){
    require([url,url2],function() {

      // For test purposes:
      // Person class has a greet() function. This will output in console log: "Hello, my name is Jack and I'm 30 years old"
      new Person("Jack", 30).greet(); 
      // Car class has age() function. This will prompt a message "10" as how much old the car is based on the year model
      alert(new Car("Ford", 2014).age());
      });
    });
    });
    ```

5. Save and deploy the application.

    !!! note
        If the `.js` file resources are not uploaded to **Files**, or located online, adjust the code below.

      ```javascript
      // get url of online js
      var url = "https://host_name/sample-js-files/simpleCar.js"
      var url2 = "https://host_name/sample-js-files/simplePerson.js"

      // use global function to load multiple js
      require([url,url2],function() {

        // For test purposes:
        // Person class has a greet() function. This will output in console log: "Hello, my name is Jack and I'm 30 years old"
        new Person("Jack", 30).greet(); 
        // Car class has age() function. This will prompt a message "10" as how much old the car is based on the year model
        alert(new Car("Ford", 2014).age());
      });
      ```

**Parent topic:** [JavaScript API](ref_javascript_api.md)

