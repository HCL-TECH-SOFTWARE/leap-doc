# List 

This action retrieves a list of records.

!!! note
    The **curl** command must be entered as a single line.

```
curl --user <loginId>:<passwd> http://<host>:<port>/{% if isLeap %}apps-basic{% endif %}{% if isDominoLeap %}volt-api{% endif %}/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/
     F_Form1?format=application%2Fatom%2Bxml&sortBy=lastUpdated&order=DESC&from=10&to=20
```

**format or Accept header**

The format in which the data must be returned. You can use either format or Accept header.

!!! note
    When using the format parameter, you must encode the value. For example, application/atom+xml must be inserted into the curl command as application%2Fatom%2Bxml

- **application/atom+xml** returns data as a standard ATOM feed in XML format. This is the default value.        
- **application/x-msexcel** returns data as an Excel document
- **application/vnd.oasis.opendocument.spreadsheet** returns data as an OpenDocument spreadsheet
- **application/json** returns data in JavaScript™ Object Notation format

**sortBy**

The order in which the data must be returned. The default sort order is indeterminate.

   -   **lastUpdated** uses the last updated date as the sort attribute.
   -   **itemAuthor** uses the display name of the author as the sort attribute.
   -   **flowState** uses the stage name as the sort attribute.
   -   <*item ID*> uses the values of a particular form item, for example, **F_SingleLine**, as the sort attribute. Several widgets cannot be used as the sort attribute due to their storage representation in the database. This includes the **Multi-Line Entry**, **Select Many**, **Table**, and **Attachment** widgets.

**order**

The direction of the sort.

   - **ASC** uses an ascending sort order. This is the default value.
   - **DESC** uses a descending sort order.

**from**

The starting offset of a range of results. The default value is 0.

**to**

The ending offset of a range of results. The default value is the end of the list. If you set a value for **to**, the result is not inclusive of the **to** value. For example, there are 100 submitted records. You want to view the results 5 per page. You set the **from** value to 6, and the **to** value to 11. Records 6 - 10 are displayed.

**metadata**

Set to **true** to display extra information about items in the form. 
This parameter is only valid for JSON.

The result of this request is a list of records. An example result represented as an ATOM feed:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom" xml:base="http://<host>:<port>/{% if isLeap %}apps-basic{% endif %}{% if isDominoLeap %}volt-api{% endif %}/landing/1/app/
        dd34da19-15c4-4267-8f1e-9f12ece743d7/viewdata/index.html">
   <id>http://<host>:<port>/apps-basic/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1</id>
   <title type="text">Collection of Form 1</title>
   <updated>2011-11-22T19:37:09.060Z</updated>
   <count xmlns="">-1</count>
   <author>
      <name>Freedom</name>
   </author>
   <link href="http://<host>:<port>/{% if isLeap %}apps-basic{% endif %}{% if isDominoLeap %}volt-api{% endif %}/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1" rel="self"/>
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
      <link href="../../../../../secure/1/app/dd34da19-15c4-4267-8f1e-9f12ece743d7/print/index.html?form=
          F_Form1&amp;id=f82e576f-cb67-4008-8219-f49a1b369f7d" rel="print"/>
      <link href="../launch/index.html?form=F_Form1&amp;id=f82e576f-cb67-4008-8219-f49a1b369f7d" rel="form"/>
   </entry>
   <entry xmlns="http://www.w3.org/2005/Atom">
      <id>9c1f4a5b-c6b2-482d-874f-804c44bdd91e</id>
      ...
   </entry>
   <entry xmlns="http://www.w3.org/2005/Atom">
      <id>86352d79-b52e-48e6-84a2-24174d9d5481</id>
      ...
   </entry>
   ...
</feed>
```

It is important to note:

-   Each submission record is represented by an `<entry>` within the feed.
-   Each entry has an `<author>` that represents the person who initially created the record.
-   Each entry has a `<contributor>` that represents the person who last updated the record.
-   Each entry has a `<link>` with `rel="edit"` that represents the URL to use to Retrieve and Update just this record.
-   Each entry has a `<link>` with `rel="print"` that represents the URL that, when displayed in a browser, is the print version of the record.
-   Each entry has a `<link>` with `rel="form"` that represents the URL that, when displayed in a browser, allows the editing of this record.
-   Each entry has a `<content>` that contains the actual data for this record.
-   The root element of the actual data, which in this example is `<F_Form1>`, has a generated **uid** attribute. This attribute is the unique ID for the record and can be used for subsequent calls to Retrieve, Update, or Delete for that particular record.

An example result represented as a JSON feed:

```json
{
	"metadata": {
		"fields": [{
			"name": "F_SingleLine1",
			"uiType": "textField",
			"dataType": "string",
			"label": "First Name"
		},
		{
			"name": "F_SingleLine2",
			"uiType": "textField",
			"dataType": "string",
			"label": "Last Name"
		},
		{
			"name": "F_Number1",
			"uiType": "number",
			"dataType": "decimal",
			"label": "Hours worked",
			"decimalPlaces": 2
		}]
	},
	"items": [{
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
		"id": 0,
		"uid": "8cca2f81-207c-4780-875f-ee1c2bee4df1",
		"F_SingleLine1": "Joe",
		"F_SingleLine2": "Test",
		"F_Number1": 24.25
	},
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
		"uid": "324007a4-a04f-4649-8d22-e6c764313f1f",
		"F_SingleLine1": "Jane",
		"F_SingleLine2": "Test",
		"F_Number1": 25.75
	}]
}
```


The following information describes how to filter Data REST API results.  **[Filtering Data REST API results](ref_data_rest_api_list_filter.md)**  


**Parent topic:** [Data access REST API](ref_data_access_rest_api.md)

