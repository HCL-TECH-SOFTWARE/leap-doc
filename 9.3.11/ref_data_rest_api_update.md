# Update 

This action updates an existing record.

!!! note
    The **curl** command must be entered as a single line.

```
curl --user <loginId>:<passwd> --request PUT --header "Accept:application/atom+xml" --header "Content-Type:application/atom+xml" --data-binary @put.xml
     "http://<host>:<port>/{{apiContext}}/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/f82e576f-
     cb67-4008-8219-f49a1b369f7d"
```

**Content-Type**

Indicates the type of document submitted.

-   ATOM Feed: **application/atom+xml**
-   JSON: **application/json.**

**Accept**

Indicates the type of accepted response.

-   ATOM Feed: **application/atom+xml**
-   JSON: **application/json.**

**--data-binary**

Provides the actual data that is PUT to the URL. In this case, it is pointing to a file, put.xml, on the local system that contains the data to send.

**--request PUT**

Specifies the correct HTTP method verb for the action.


## ATOM Feed { #section_afj_djl_nzb .section }

Example PUT data:

```xml 
<entry xmlns="http://www.w3.org/2005/Atom">
   <title type="text">F_Form1</title>
   <updated>1970-01-01T00:00:00Z</updated>
   <content type="application/xml">
      <F_Form1 xmlns="" application_uid="dd34da19-15c4-4267-8f1e-9f12ece743d7" pressedButton="S_Submit1" 
          flowState="ST_Stage2" uid="f82e576f-cb67-4008-8219-f49a1b369f7d" id="0">
         <F_Amount>19.25</F_Amount>
         <F_Name>Brad Walker</F_Name>
         <F_Age>40</F_Age>
      </F_Form1>
   </content>
</entry>
```

**`<title>`**

The ID of the form to which this record is being submitted.

**`<updated>`**

This must be included, but its value is replaced by the server with a new timestamp. A value of **1970-01-01T00:00:00Z** can always be used.

**`<content>`**

Contains the submitted data. The structure of the data within the content element is different for each application, and is based on the list of form items used to create the application. The easiest way to find the complete list of elements is to issue a Retrieve REST call and look at the resulting data.

!!! note
    The root element of the submitted data, in this example the `<F_Form1>` element, is always in the null namespace, `xmlns=""`

The root element must have the **application\_uid, pressedButton, flowState, uid,** and **id** attributes.

   - The **application\_uid** is the UID of the application.
   - The **flowState** is the ID of the current stage of the record.
   - The **pressedButton** is the ID of the stage action submit button, which simulates the submission. A submit button ID must be specified to activate the appropriate stage activities and transfer the record to the next appropriate stage.
   - The **uid** is the unique ID for the record being updated.
   - The **id** must be an integer, although the actual value is meaningless. A value of **0** can always be used.

!!! note
    A PUT REST command updates an existing record with new values. All data fields in the old record will be replaced by the data fields provided in the payload. If the new submission does not include a field, the field will be updated to have an empty value even if it previously had a value \(i.e. the two records are NOT merged\).

## JSON { #section_wwg_2jl_nzb .section }

Example JSON payload:

```json 
{
   "uid": "f82e576f-cb67-4008-8219-f49a1b369f7d",
   "flowState": "ST_ReviewStage",
   "pressedButton" : "S_Approve",
   "F_SingleLine1": "Jane",
   "F_SingleLine2": "Test",
   "F_Number1": 26.75
}
```

!!! note
    The **uid** is optional. If supplied, it must match the record uid. For example: f82e576f-cb67-4008-8219-f49a1b369f7d.

**Parent topic:** [Data access REST API](ref_data_access_rest_api.md)

