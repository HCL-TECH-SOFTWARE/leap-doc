# Retrieve Attachment { #reference_swb_lsf_2z .reference }

This action retrieves a single attachment.

```
curl --user <loginId>:<passwd> "http://<host>:<port>/{{apiContext}}/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/attachment/ccb92c12-d435-4288-baff-878d8d3c2923"
```

-   Replace `dd34da19-15c4-4267-8f1e-9f12ece743d7` with the app ID of the desired attachment.
-   Replace `F_Form1` with the form ID of the desired attachment.
-   Replace `ccb92c12-d435-4288-baff-878d8d3c2923` with the UID of the desired attachment.

To determine the UID of an attachment, you can use the [Data access REST API](ref_data_access_rest_api.md) to retrieve the data for a given record. If the form contains an attachment item, the data for that record will contain the UID, ID, and filename of the attachment. This information is also available in the response when you upload a file using the [Create Attachment](ref_data_rest_api_create_attachment.md) REST operation.

For example:

```json
"F_Attachment1" :
{
  "fileName" : "some file.doc",
  "id" : 123,
  "uid" : "ccb92c12-d435-4288-baff-878d8d3c2923"
}
```

When retrieving an attachment, the credentials used for authentication must match the users and permissions specified by the application designer in the **Access** tab.

**Parent topic:** [Data access REST API](ref_data_access_rest_api.md)

