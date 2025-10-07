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

**format or Accept header**

The format in which the data must be returned. You can use either **format** or **Accept header**.

!!! note
    When using the format parameter, you must encode the value. For example, **application/atom+xml** must be inserted into the curl command as **application%2Fatom%2Bxml**.

- **application/atom+xml** returns data as a standard ATOM feed in XML format. This is the default value.
-   **application/json** returns data in JavaScript™ Object Notation format
-   Set **itemOnly** to **true** if you want to receive a simplified response. **itemOnly** is only available for JSON.

The result of this request is an ATOM Entry XML document:

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

