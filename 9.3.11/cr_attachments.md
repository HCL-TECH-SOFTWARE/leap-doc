# Working with attachments

A file that is added to a form using the attachment item is uploaded to the {{shortProductName}} server as soon the user adds it.  The attached file is associated with the form **after** it is submitted.  If the form is not submitted then the uploaded file will be removed by the server after 48 hours.

An attachment item is made up of an id, uid and filename and it can be used in many different ways.  There is a [REST API for working with attachments](ref_data_rest_api_retrieve_attachment.md), this can be used to produce some dynamic behavior in your application.


## Get Attachment File Name

You can retrieve the file name of an attachment item by using javascript.

```javascript
// if secureJS == true
var filename = get(BO.F_Attachment.getValue(), "fileName");

// if secureJS == false
var filename = BO.F_Attachment.getValue().fileName;
```


## Render attachment in a later stage

If you have a form where the user attaches an image, you can render that image in the form, in a later stage, after it has been submitted.

1. Create an attachment item (F_Attachment)

2. Create an HTML item.  In the **onShow** event of place the code:

```javascript
var attachmentUid = BO.F_Attachment.getValue().uid;
var url = "/{{context}}/secure/org/data/" + app.getUID() + "/" + form.getId() + "/attachment/" + attachmentUid;
 
item.setContent("<img src='" + url + "'></url>");
```

3. Hide the HTML item in the *Start* stage (using a rule or workflow visibility controls). It is important to note that the content of an attachment cannot be displayed until the form has been submitted.  The URL here is using the REST API to get the content of the attachment, but until the form has been submitted the attachment is not available on the server.

4. When your form gets to the next stage you will now see the image rendered!


## Display link to attached file in a later stage

You can provide the user with a link to the attached file on a different page of the form than where the attachment item is located.

1. Create an Attachment object (id = F_Attachment)

2. Create a Link item (in the Action drawer)

3. Place this code in the *onShow* event:

```javascript
var attachmentUid = BO.F_Attachment.getValue().uid;
var url = "/{{context}}/secure/org/data/" + app.getUID() + "/" + form.getId() + "/attachment/" + attachmentUid;

item.setDisplayValue(BO.F_Attachment.getValue().fileName);
item.setLinkValue(url);
```

4. When the page where the link is rendered the link display will be set to the filename and clicking on the link will open/download the file.

!!! note
    You can access the file name at anytime even before the form has been submitted, but you cannot create a valid link to the attachment until the form has been submitted.


## Multiple Attachments

You can place the Attachment item within a table.  The table should have two single-line fields; one for the filename and the other for the attachment UID.  In the *onItemChange* event of the attachment item you can use the following JavaScript to set the field values:

```javascript
// modern browsers may add a 'fakepath', remove it
BO.F_AttachmentName.setValue(BO.F_Attachment0.getValue().fileName.replace("C:\\fakepath\\", ""));
BO.F_AttachmentUid.setValue(BO.F_Attachment0.getValue().uid);
```

Now your users can attach as many files as they want and have a way of seeing what they have added. You can hide the ID column by removing it from the defined columns on the Advanced tab of the table properties.


## Attachment summary

In this example we have a table of attachments from a previous stage and we want to provide a way for the user to download the attachments from a summary page in a future stage.  We can use JavaScript with the Link item to provide this functionality.

Place a Link item on your form, outside the table.  When you click on a row of the table we are going to set the link URL and display value to point to the attachment from the selected row. To do this we place the following code in the *onClick* event of the table:

```javascript
if(item.getSelection() !== null) {
  var url = "/{{context}}/secure/org/data/" + app.getUID() + "/" + form.getId() + "/attachment/" + item.getSelection().F_AttachmentUid.getValue();
  item.getPage().F_StaticWebLink1.setLinkValue(url);
  item.getPage().F_StaticWebLink1.setDisplayValue(item.getSelection().F_AttachmentName.getValue());
}
```

When the user selects a row of the table, the URL of the attachment is set to the Link value and its display value is set to the attachment name.

This will only work after the form has been submitted.


## Reading contents of an uploaded file

If you are running on a server that has JavaScript sandbox turned off (secureJs=false), a setting found in the {{shortProductName}} properties, then you could use AJAX to retrieve the content of the file that was uploaded.  

For this example, the code was placed in the *onShow* event of a multi-line text field that is visible after the form has been submitted.  When the field is shown it will contain the content of the file that was previously uploaded.

```javascript
var attachmentUid = BO.F_Attachment.getValue().uid;
var url = "/{{context}}/secure/org/data/" + app.getUID() + "/" + form.getId() + "/attachment/" + attachmentUid;

// create function to get file content using REST API
function loadDocContent()
{
  var xmlhttp;
  if (window.XMLHttpRequest) {
    // code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp=new XMLHttpRequest();
  } else {
    // code for IE6, IE5
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }

  xmlhttp.onreadystatechange=function()
  {
    if (xmlhttp.readyState==4 && xmlhttp.status==200) {
      BOA.setValue(xmlhttp.responseText);
    }
  }

  xmlhttp.open("GET",url,true);
  xmlhttp.send();
}
 
var attachedFileContent = loadDocContent(); //executes the function
item.setValue(attachedFileContent);
```

**Parent Topic:** [Adding dynamic behavior](cr_adding_dynamic_behavior.md)