# Triggering a service 

You can use a service to add information to a form automatically after a user triggered event.  Services can be triggered from almost anywhere within a Leap application.  

## From a button {#triggeringawebservicefromabutton .task}

To use a service call when the user clicks a button:

1.  Add a **Button** to your form from the Palette if your form does not yet have one.

2.  Select the newly added button.

    The Properties side panel opens.

3.  Select **Call a service when clicked**.

    A menu opens where you can:

    -   Select an existing web service from the menu. If you select an existing service from the menu, go to step 8.
    -   Create a service call by clicking **Add/Edit Service Configuration**. To configure a service, go to step 5.
4.  When you click **Add/Edit Service Configuration**, the **Service Configuration** window opens.

    -   Enter the URL of your service
    -   Select **Or, select a service** and select a URL from a list of available services
5.  Click the **Inputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

        The connected source and target are shown in the **Assigned Inputs** section of the page.

6.  Click the **Outputs** tab.

    1.  Select a source from the **Select source:** window.

    2.  Select a target from the **Select target:** window.

    3.  Click the connector icon located between the two windows to link the source and the target.

    The connected source and target are displayed in the **Assigned Outputs** section of the page.

7.  Click **OK** to exit the **Service Configuration** window.


## When the value of a form item changes {.task}

Triggering a service when the value of a field changes is a common use case.  For example, you may want to validate field content as soon as it is entered, giving the user immediate feedback rather then waiting till they try to submit.

1. Click the item from which you want to trigger the service.

2. In the Properties page, click the **Events** tab.

3. Click the **onItemChange** event.

4. Select the "Call a Service" check box and select the service from the drop down list.  If the service does not exist, you can click "Add/Edit Service Configuration" to create one.


## When a new form is launched

You may want to call a service to populate the form when it is loaded for the first time.  For example, you might want to pre-populate information about the current user by calling a service that queries the corporate employee directory.  The danger in simply calling a service like this in the Form *onLoad* event is that it will get called in every stage so the original information would get replaced with the user that opened the form in the later stage.  To avoid this you should use the *onNew* event:

1. Click a blank space on the design canvas.
2. In the Properties pane, click the "Call a service to pre-populate" checkbox.
3. Select the service from the "On display of new form" drop down list.  This will only trigger the service when a new form is created and ignore it on loads in a subsequent stage.  If the service does not exist, you can click "Add/Edit Service Configuration" to create one.

**Note:** if you want to call a service on every subsequent load of a form (but not when it is created) then you could use the On re-load of existing form dropdown list.


## Using javaScript

You can trigger a service call at anytime with JavaScript.  The syntax will change depending on where you are placing the code.  

```javascript
form.getServiceConfiguration("<Service ID>").callService();
```

The service ID can be found on the Settings tab, under the Services section on the left navigation section – click on the link that matches the form where the service was created.  A Service Configuration dialog will appear, the ID is on the Details tab.

The basic structure for connecting an event is:

```javascript
var srv = form.getServiceConfiguration('SC_serviceA');
srv.connectEvent("onCallFinished", function(success, errorObj){
  if(success) {
    try {
      // code to execute when the service completes
    } catch(err) {
      alert("SC_theService: " + err);
    }
  } else {
    // executed if an error occurs
    // set errorObj.handled to true in the errorObj
  }
});
```

This code is available as a code template, which can be accessed by pressing ctrl+space twice. 

There are multiple places where you can put this code but it needs to be adjusted based on the context of where it is located.

### When another service finishes

You may encounter a situation where you need to call a second service after you have received the result of the first service.  Because the service calls are asynchronous, occur at the same time, you have to connect to an event that will execute the provided code when the service completes.

```javascript
var srv = form.getServiceConfiguration('SC_serviceA');
srv.connectEvent("onCallFinished", function(success, errorObj){
  if(success) {
    try {
      form.getServiceConfiguration('SC_serviceB').callService();
    } catch(err) {
      alert("SC_theService: " + err);
    }
  } else {
    // executed if an error occurs
    // set errorObj.handled to true in the errorObj
  }
});
```


### Application onStart event

A good place to trigger a service when any of the forms in an application are launched is in the application *onStart* event.

The form keyword does not exist at this level, therefore you have to explicitly retrieve the form for which you want to reference.

The *onStart* event is executed for every form within an application.  If you try to retrieve a service that does not exist then you will get an error.  Therefore when implementing the listener in this event you must confirm that the form exists before trying to retrieve the service:

```javascript
var form = app.getForm('<Form ID>');
if(form !== null)
{
  var srv = form.getServiceConfiguration('SC_theService');
  srv.connectEvent("onCallFinished", function(success, errorObj){
  if(success) {
    try {
      // put code in here to execute when service is done
    } catch(err) {
      alert("SC_theService: " + err);
    }
  } else {
    // executed if an error occurs
    // set errorObj.handled to true in the errorObj
  }
});
}
```


### Form onLoad event

The form *onLoad* is only called when that form is loaded:
    -  so you won't have to worry about checking to see if the form exists.
    - you don't have to disconnect the event handler

```javascript
var srv = form.getServiceConfiguration('SC_theService');
srv.connectEvent("onCallFinished", function(success, errorObj){
if(success) {
  try {
    // put code in here to execute when service is done
  } catch(err) {
    alert("SC_theService: " + err);
  }
} else {
  // executed if an error occurs
  // set errorObj.handled to true in the errorObj
}
```


### Item event

When you connect to an event from within an item it might get executed multiple times within a single session.  

For example, you might connect to the 'conCallFinished' event in the *onItemChange* event of a field.  In this context, a new instance of the event handler will be created when the field changes.  You must disconnect the event handler, after it executes.  If you forget to do this you may see erratic behavior or code being executed multiple times.

```javascript
var srv = form.getServiceConfiguration('SC_theService');
srv.connectEvent("onCallFinished", function(success, errorObj){
  if(success) {
    try {
      // put code in here to execute when service is done
    } catch(err) {
      alert("SC_theService: " + err);
    }
  } else {
    // executed if an error occurs
    // set errorObj.handled to true in the errorObj
  }
  srv.disconnectEvent(hdl);
});
```

**Parent topic:** [Incorporating web services into your applications](cr_using_apps_as_services_toc.md)

