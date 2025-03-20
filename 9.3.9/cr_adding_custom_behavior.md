# Adding custom behaviour

There may be times that you want your applications to behave a certain way and it is not a built-in feature.  There are many different ways to add custom behavior with a little planning and some custom javaScript.  

This page provides some examples of custom behavior.

## Automatically submit after X minutes

This form will be submit automatically after X minutes.  You could use this technique for a form where the user is only given a certain amount of time to complete it (i.e. a timed test).

This example uses some javaScript in the *onNew* event to programmatically trigger the submit button.  The javaScript is:

if secureJS=false:
```javascript
// Will trigger the submit button after 10 minutes has
// passed since the form was opened.
setTimeout(function(){
var actionButtons = form.getStageActions();
for(var i=0; i<actionButtons.length; i++){
  if(actionButtons[i].getId() === 'S_Submit')
    actionButtons[i].activate();
}},600000);
```

if secureJS=true:
```javascript
setTimeout(function(){
var actionButtons = form.getStageActions();
for(var i=0; i<actionButtons.length; i++){
  if(get(actionButtons, i).getId() === 'S_Submit')
    get(actionButtons, i).activate();
}},600000);
```

There are some key things to remember:

1.  You must redirect the form after the submission, in the properties of the Submit button in the Stages tab

or 

2. You must change the form to render in the next stage

If you do not do one of these two things then this will cause the form to get stuck in an endless loop of opening a new form and then submitting it (which becomes really apparent if you shorten the submit timing to 1s).  However if a user closes the form then the javaScript is not executed.


## Customize the submit behavior

Why would I want to customize the submit behavior and what does that mean?

### Use Cases:

1. You don't like where the submit button is (in the footer) and you want to move it in your form or you want to change the look and feel of the submit button (like use an image for the button).

2. You might want to perform some error checking before allowing the submit to complete.

3. Disable the dialog that appears on submit showing invalid fields.

4. Customize error text that appears below invalid items.

### Case #1 - Creating a form button that triggers the submit action.

1. Create a regular form button.

2. In the onClick event of your button object you can place the following code to activate the "real" submit button:

    ```javascript
    var actionButtons = form.getStageActions();
    for(var i=0; i<actionButtons.length; i++){
      if(get(actionButtons, i).getId() === 'S_Submit')
        get(actionButtons, i).activate();
    }
    ```

    The only part of this code that you may have to change is the "S_Submit", this is the ID of the stage action that you want to trigger.  To find the ID you will have to go to the Stages tab, then open the properties for the button you want to trigger.

3. Next, we need to hide the "real" submit button so that the user can't click it.  If you deselect the checkbox on the page properties to not show the stage buttons then the objects are not created and then cannot be activated.  Instead leave the checkbox enabled and hide the stage buttons with the form is loaded.  In the form onShowActionButtons you can hide the stage buttons by using:

    ```javascript
    var actionButtons = form.getStageActions();
    for(var i=0; i<actionButtons.length; i++){
      get(actionButtons, i).setVisible(false);
    }
    ```

The above code will hide ALL the stage action buttons.  If you just want to hide a single stage action button then you would have to modify the code to look like:

    ```javascript
    var actionButtons = form.getStageActions();
    for(var i=0; i<actionButtons.length; i++){
      if(get(actionButtons, i).getId() === 'S_Submit') {
        get(actionButtons, i).setVisible(false);
      }
    }
    ```

In this example we check for the ID of the action button and only hide the ones that we want.

### Case #2 - Custom Error checking before submit

There are two ways to perform error checking BEFORE the submit operation:

1. If you are implementing a form button that triggers a submit as referenced in Case #1 then you could add the custom error checking to the onClick event of the form button before you execute the stage action.  For example:
    ```javascript
    // only perform the submit if the condition passes
    if(x = 1) {
      var actionButtons = form.getStageActions();
      for(var i=0; i<actionButtons.length; i++){
        if(get(actionButtons, i).getId() === 'S_Submit')
          get(actionButtons, i).activate();
      }
    }
    ```

### Case # 3 - Disable the Invalid Item Dialog

There is no way to disable the invalid item dialog that appears on submit.  The only way to workaround it is to not use the default validity check and to implement your own using javaScript validation.  Let's look at this in greater detail, what is involved in something like this:

1. Can't use the required property of the form items

2. Can't use rules to change required or valid

    Since we can't use the built-in tools for this we now have to manage it on our own.  This means that all the validation will be controlled by javaScript that is executed when the form is loaded in the browser.

3. Since required and valid are controlled by javaScript they cannot be enforced when using the REST API

    So to bypass the default dialog we need to get in front of it, we can do that by adding code to the validateButtonPressed event which is executed anytime a stage button is triggered.  The code might look something like this:

    ```javascript
    if(pActionId === 'S_Submit') {
      // do your custom validation, here you can use setValid() or setRequired() if desired
      // if you consider the form to be in an invalid state then return false to cancel the submit action
      if(!app.getSharedData().isFormValid) {
        return false;
      }
    }
    ```

This technique looks to cancel the submit action if the form is deemed invalid by your criteria.  If the form is considered valid then the submit is allowed to proceed.  In this way the user would never see the invalid items dialog because we never actually trigger the submit action if any of the fields contain invalid data.

### Case #4 - Customize the error text that appears below invalid items

There may be times that you want to customize the error text making it more descriptive of what the user needs to do.  In this example, a message will appear beneath any field on the form that is invalid.

Implementing a solution that allows custom messages means that you have to use javaScript and abandon the default error checking and you cannot use the built-in property or a rule for setting the field as required.  The approach that I took looks like this:

1. Create an object array to store the fields to be considered required and the custom message to use

2. In the *validateButtonPressed* event walk all the form items and use the setValid() function to set the custom error text if the field is empty or invalid.  At the same time we have to set a listener in the onItemChange event to clear the error text if the user enters text into the field.

    This solution leverages the [recursive function](js_sample_functions.md#recursive-function-to-loop-over-all-items-in-a-form)).  Copy the hasItems and getItem functions into the *onLoad* event, in addition to the following code:

    ```javascript
    // add all the fields that you want to be required and their custom error text to the object array
    app.getSharedData().requiredMap = new Array();
    app.getSharedData().requiredMap.push({id: 'F_SingleLine2', msg: 'Please enter name.'});
    app.getSharedData().requiredMap.push({id: 'F_SingleLine3', msg: 'Please enter address.'});
    app.getSharedData().requiredMap.push({id: 'F_SingleLine', msg: 'Please enter age.'});
    
    // This function is used for retrieving an item from the requiredMap by ID specified
    app.getSharedData().getArrayVal = function(id) {
      var theMsg = "";
      for(var i=0; i<app.getSharedData().requiredMap.length;i++) {
        var tmp = get(app.getSharedData().requiredMap, i);
        if (tmp.id === id) {
          theMsg = tmp.msg;
          break;
        }
      }
    return theMsg;
    }
    
    /*
    * This is the function where you place the logic that you want to perform on the item that you are currently looking at.
    * The recursive function passes the handle to the current item, from which you can then access any of its properties
    */
    app.getSharedData().isFormValid = true;
    app.getSharedData().processItem = function(item) {
      if(item.getType() === "text") {
    
        // do your thing
        var theMsg = app.getSharedData().getArrayVal(item.getId());
        if(theMsg !== "") {  //item is a required item
          if(item.getValue() === "" || !item.getBOAttr().getValid()) {
            app.getSharedData().isFormValid = false;
            item.getBOAttr().setValid(false, theMsg);
          }
        }
    
        var ev = "onItemChange";
        // add an onItemChange Listener - the code within will be called when the fields value changes
        var hndl = item.connectEvent(ev, function(success){
          var v = item.getBOAttr().getValue();
          if(v !== "") {
            item.getBOAttr().setValid(true, "");
          }
      }); // end of dynamic event listener
      } // end if item.getType
    }
    ```
    
    The code is then triggered from the validateButtonPressed event:

    ```javascript
    if(pActionId === 'S_Submit') {
    
      // reset valid flag for multiple submit attempts in one session
      app.getSharedData().isFormValid = true;
    
      // walk all form items looking for invalid fields
      app.getSharedData().getItem(form, app.getSharedData().processItem);
      if(!app.getSharedData().isFormValid) {
        return false;
      }
    }
    ```

## Inactive form time-out

This example simulates a forced time-out.  If the form sits inactive for a specified duration then you can for the form to close or redirect to a different page.  This works by using the javaScript setTimeout and clearTimeout functions.

When the form loads we first walk all the input items in the form and attach a listener to the onItemChange event.  When a field changes the event listener will clear the current timeout and then start it over again.

If the duration is met then the form performs the action defined in the app.getSharedData().doTimeout function, which in this case is to switch to a custom page in the application that provides instructions to the user that their session timed out.

The duration for this sample is 5 seconds (5000 milliseconds), if you do nothing

### Code

**onStart**

Copy all of the functions from [recursive functions](js_sample_functions.md#recursive-function-to-loop-over-all-items-in-a-form) into the *onStart* event.

**Form onLoad event**
```javascript
app.getSharedData().timeoutDuration = 5000;  // duration of timeout in milliseconds
app.getSharedData().timeout = null;      // holds the pointer to the current timeout process
app.getSharedData().hndls = new Array(); // holds the handles for all the onItemChange listeners
 
// defines what happens when the timeout is executed
// this action could be anything you want it to be
app.getSharedData().doTimeout = function() {
  form.selectPage("P_NewPage2");
}
 
// hook the timeout functions on all the form input items onItemChange event
app.getSharedData().getItem(form, app.getSharedData().processItem);
 
// start the timeout, if any form item changes then we clear the timeout and start over
app.getSharedData().timeout = setTimeout(app.getSharedData().doTimeout, app.getSharedData().timeoutDuration);
```

**Form onDesctruct event**
```javascript
// disconnect all the handles.  We do this incase the form is ever reloaded in the same
// session, because it will attach new listeners which means there will be duplicates
for(var i=0; i< app.getSharedData().hndls.length;i++) {
  var itm = get(app.getSharedData().hndls, i).itm;
  var hndl = get(app.getSharedData().hndls, i).hndl;
 
  itm.disconnectEvent(hndl);
}
```

## Progress Indicator

Often we want to take user through a few questions / panels at a time.  While doing so it's good practice to let the user know the progress they have made at completing the form with a graphical indicator.

The simplest way to do this is by using the HTML <Progress> Tag.

Let's say that you have 3 steps in the form completion process.  

1. Add an HTML item to each page.
2. Add the "progress" element with the appropriate value for each page in the form.

```html
<progress value="33" max="100"></progress>
```

For a more accurate progress meter, you could calculate its maximum value to be the total number of fields and update its value as each field is filled in.    To accomplish this we have to walk over all the items when the page is loaded and attach an event handler that will update the progress meter.

In the form *onLoad* event you need the isInputField, hasItems and getItem from the [recursive functions](js_sample_functions.md#recursive-function-to-loop-over-all-items-in-a-form), in addition to the following code:

```javascript
app.getSharedData().fieldCount = 0;
app.getSharedData().filledFieldCount = 0;
app.getSharedData().fieldValues = [];

app.getSharedData().processItem = function(item) {
 
  if(app.getSharedData().isInputField(item.getType())) {
    // increment the global field count
  	app.getSharedData().fieldCount += 1;  
    
    // attach an event handler
    item.connectEvent("onItemChange",function(){
  
      if (item.getValue() !== "")
      {
        var field = app.getSharedData().fieldValues.find(field => field.id === item.getId());
        if ( !field ) {      
          // first time so adding to the global array to watch field values
          app.getSharedData().fieldValues.push({id:item.getId(), value:item.getValue()});
          app.getSharedData().filledFieldCount += 1;
        }  
      }
      else
      {
        // field was cleared, decrement the progress meter 
        app.getSharedData().filledFieldCount -= 1;

        // remove the field from the global list
        var filter = app.getSharedData().fieldValues.filter(field => field.id !== item.getId());
        app.getSharedData().fieldValues = filter;
      }

      // update the progress meter
      const str = "<progress value='" + app.getSharedData().filledFieldCount + "' max='" + app.getSharedData().fieldCount + "'></progress>";
      item.getPage().F_HTMLArea4.setContent(str);
    });
  }
}
```


**Parent topic:** [Adding dynamic behavior](cr_adding_dynamic_behavior.md)