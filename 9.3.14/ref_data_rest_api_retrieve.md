# Retrieve 

This action retrieves a single record.

!!! note
    The **curl** command must be entered as a single line.

```
curl --user <loginId>:<passwd> --header "Accept:application/atom+xml" "http://<host>:<port>/{{apiContext}}/secure/
     org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/f82e576f-cb67-4008-8219-f49a1b369f7d"

curl --user <loginId>:<passwd> "http://<host>:<port>/{{apiContext}}/secure/
      org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/f82e576f-cb67-4008-8219-f49a1b369f7d
      ?itemOnly=true&format=application%2fjson"
```

## Optional Parameters

There are several optional query parameters that can affect the output.

### columns

Limits the response to the specified properties, which can only be the id of a field in the form. Columns must be separated by spaces (%20). Invalid column names will be ignored. Only applies to JSON response format.

!!!note
    You may encounter issues trying to specify a url with a large number of columns.  There is no official length restriction on a URL, however in practice urls that are more than 2048 characters may experience issues.

**Sample URL**
```
http://.../secure/org/data/e46fe2c0-8414-40ff-9890-c9d795990480/F_Form1/b464befb-fbe9-4afe-8fb8-8e7c3bc9fe46?columns=F_SingleLine1%20F_SingleLine3%20F_Invalid
```

**Sample output**
```
{
    "application_uid": "e46fe2c0-8414-40ff-9890-c9d795990480",
    "formId": "F_Form1",
    "recordCount": -1,
    "items": [
        {
            "F_SingleLine1": "1",
            "F_SingleLine3": ""
        }
    ]
}
```

### Save Draft

Returns drafts in non-Start stage.

```GET /secure/org/data/[app_uid]/[form_id]/[record_uid]``` will return the original record,  the ```has_draft=”true”``` attribute indicates that the current user has a draft for the specified record id. 

!!!note
    Known issue: This attribute is missing from the JSON response.

```GET /secure/org/data/[app_uid]/[form_id]/[record_uid]?draft=true``` will return the current user’s draft for the specified record id. A 404 will be returned if the current user does not have a draft for the specified record id.

### format or Accept header

The format in which the data must be returned. You can use either **format** or **Accept header**.

!!! note
    When using the format parameter, you must encode the value. For example, **application/atom+xml** must be inserted into the curl command as **application%2Fatom%2Bxml**.

- **application/atom+xml** returns data as a standard ATOM feed in XML format. This is the default value.
-   **application/json** returns data in JavaScript™ Object Notation format
-   Set **itemOnly** to **true** if you want to receive a simplified response. **itemOnly** is only available for JSON.

## Sample Atom Response

The result of this request as an ATOM Entry XML document:

```xml
<?xml version="1.0" encoding="UTF-8"?>
   <entry xmlns="http://www.w3.org/2005/Atom">
      <id>f82e576f-cb67-4008-8219-f49a1b369f7d</id>
      <title type="text">F_Form1</title>
      <updated>2011-11-22T19:36:31.000Z</updated>
      <author>
         <name>Mike Smith</name>
         <email>msmith@mycompany.com</email>
         <login xmlns="http://www.ibm.com/xmlns/prod/forms/extension/1.0">msmith@mycompany.com</login>
      </author>
      <contributor>
         <name>Brenda Jones</name>
         <email>bjones@mycompany.com</email>
         <login xmlns="http://www.ibm.com/xmlns/prod/forms/extension/1.0">bjones@mycompany.com</login>
      </contributor>
      <content type="application/xml">
         <F_Form1 xmlns="" application_uid="dd34da19-15c4-4267-8f1e-9f12ece743d7" draft_ownerid="" 
            flowState="ST_NewStageName" id="0" uid="f82e576f-cb67-4008-8219-f49a1b369f7d">
            <F_Amount>30.45</F_Amount>
            <F_Name>Brenda</F_Name>
            <F_Age>39.0000</F_Age>
         </F_Form1>
      </content>
      <link href="../../../../../secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/
          f82e576f-cb67-4008-8219-f49a1b369f7d" rel="edit"/>
      <link href="../../../../../secure/1/app/dd34da19-15c4-4267-8f1e-9f12ece743d7/print/
          index.html?form=F_Form1&amp;id=f82e576f-cb67-4008-8219-f49a1b369f7d" rel="print"/>
      <link href="../launch/index.html?form=F_Form1&amp;id=f82e576f-cb67-4008-8219-f49a1b369f7d" rel="form"/>
   </entry>
```

## Sample JSON Response

The result of this request as a JSON document:

```json
{
   "lastModified": "2013-11-22T19:37:09.060Z",
   "lastModifiedBy" : {             
      "displayName" : "Demo User 1",
      "email" : "demo_user1@yourcompany.com",
      "login" : "demo_user1"           
   },
   "created": "2013-11-22T19:37:09.060Z",
   "createdBy": {
      "displayName": "Demo User 2",
      "email": "demo_user2@yourcompany.com",
      "login" : "demo_user2" 
   },
   "flowState": "ST_End",
   "id": 1,
   "uid": "f82e576f-cb67-4008-8219-f49a1b369f7d",
   "F_SingleLine1": "Jane",
   "F_SingleLine2": "Test",
   "F_Number1": 25.0
}
```

Refer to the [List](ref_data_rest_api_list.md) action for a detailed description of the returned entry.

**Parent topic:** [Data access REST API](ref_data_access_rest_api.md)

