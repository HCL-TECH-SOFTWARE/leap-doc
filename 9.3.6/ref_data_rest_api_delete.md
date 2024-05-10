# Delete 

This action deletes an existing record.

**Note:** The curl command must be entered as a single line.

```
curl --user <loginId>:<passwd> --request DELETE http://<host>:<port>/apps-basic/secure/org/data/
dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/f82e576f-cb67-4008-8219-f49a1b369f7d?freedomIdentifyKey=1 
--header "Cookie: freedomIdentifyKey=1"
```

**--request DELETE**

Specifies the correct HTTP method verb for this action.

**--header "Cookie: freedomIdentifyKey=1"**

Includes a required cookie as part of the request. The value of the key must match the value of the freedomIdentifyKey URL parameter. Requiring a cookie value that matches the URL parameter value avoids XSS vulnerabilities.

**Parent topic: **[Data access REST API](ref_data_access_rest_api.md)

