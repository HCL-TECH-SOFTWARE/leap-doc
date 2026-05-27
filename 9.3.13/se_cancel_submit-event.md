# Cancel submit event

Have you ever wanted to update the form with some programmatic content after the user clicks submit but before the form gets submitted?  

In this example we want to assign the form a unique ID right at the time the user submits the form.  Using the **validateButtonPressed** event we can cancel the submit event, perform our asynchronous service call to get our next form ID and then programmatically submit the form.  A global variable is used to determine if the form is complete and can be submitted.

In the **validateButtonPressed** event:

```javascript
// check the global variable that indicates a submission is allowed - this gets set by our service handler once the ID has been retrieved
 
if(app.getSharedData().submitAllowed) {
  app.getSharedData().submitAllowed = false; //we have to reset the global variable for subsequent submissions within the same browser session
  return true;
} else { 
  // We get here the first time the user clicks submit.  We call the async service and return false which cancels the submit event
  form.getServiceConfiguration('SC_ServiceConfig1').callService();
  return false;
}
```

In the form **onLoad** event place a listener for the service that is getting your ID:

```javascript
//this gets called when the service is complete
 
var srv = form.getServiceConfiguration('SC_ServiceConfig1');
srv.connectEvent("onCallFinished", function(success)
{
  if(success) {
 
   // set the global flag to true so that when we programmatically trigger the submit it is allowed to proceed
   app.getSharedData().submitAllowed = true;
 
   // set ID to next number
   BO.F_SingleLine0.setValue(parseFloat(BO.F_Number.getValue()) + 1);
 
   // trigger the submit button
   var actionButtons = form.getStageActions();
   for(var i=0; i<actionButtons.length; i++) {
     if(get(actionButtons, i).getId() === 'S_Submit')
       get(actionButtons, i).activate();
  }
});    
```

**Parent Topic:** [Incorporating web services into your applications](cr_using_apps_as_services_toc.md)