# Create Attachment 

This action creates a single attachment.

```
curl --user <loginId>:<passwd> -F filename=@c:\new file.doc --header "Accept:application/json" "http://<host>:<port>/apps-basic/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/attachment/"
```

**Accept**

Indicates the type of accepted response.

   -   ATOM: **application/atom+xml**
   -   JSON: **application/json**

The attachment that is created must be uploaded to the server as `multipart/form-data` in the body of a POST.

The response from this call contains the UID, ID, and filename of the newly created attachment.

For example:
```json
{"id": 178, "fileName": "new file.doc", "uid": "ccb92c12-d435-4288-baff-878d8d3c2923" }
```

The UID value that is returned here can be later used with the [Retrieve Attachment](ref_data_rest_api_retrieve_attachment.md) REST operation.

For the attachment to be associated with a form record, a form record must be created or updated that refers to that attachment. Use the [Data access REST API](ref_data_access_rest_api.md), passing the UID, ID, and filename of the attachment.

Example JSON payload:

```json
{
	"pressedButton":"S_Submit",
	"F_SingleLine1" : "22",
	"F_Number2" : 1,
	"F_Number3" : 2,
	"F_Number4" : 3,
	"F_Attachment1" :
	{
		"uid" : "ccb92c12-d435-4288-baff-878d8d3c2923",
		"fileName" : "new file.doc",
		"id" : 178
	}
}
```

If an attachment is not associated with a form record within a certain time period \(48 hours by default\), the attachment is deleted automatically. Deleting the record that is associated with an attachment also deletes the attachment.

**Parent topic: **[Data access REST API](ref_data_access_rest_api.md)

