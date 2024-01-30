# Create {#create-rest-api .reference}

This action creates new records.

**Note:** The curl command must be entered as a single line.

```
curl --user <loginId>:<passwd> --header "Accept:application/atom+xml" --header "Content-Type:application/atom+xml" --data-binary
     @post.xml "http://<host>:<port>/volt-api/secure/org/data/dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1
     ?freedomIdentifyKey=x" --header "Cookie: freedomIdentifyKey=x"
```

Content-Type
:   Indicates the type of document submitted:

    -   ATOM Feed: application/atom+xml
    -   JSON: application/json.

Accept
:   Indicates the type of accepted response.

    -   ATOM Feed: application/atom+xml
    -   JSON: application/json.

--data-binary
:   Provides the actual data that is POSTed to the URL. In this case, it is a file on the local system, post.xml, that contains the data to send.

--header "Cookie: freedomIdentifyKey=x
:   Includes a required cookie as part of the request where x is a randomly generated, difficult to guess single-use numerical value. The value of the key must match the value of the freedomIdentifyKey URL parameter. Requiring a cookie value that matches the URL parameter helps avoid possible browser vulnerabilities.

## ATOM Feed {#section_ng4_v3l_nzb .section}

One type of data to POST when doing a creation is a full ATOM Feed. The data starts with a <feed\> element and contains one or more <entry\> elements. Each <entry\> element represents a single record to add to the application.

``` {#codeblock_xyr_v3l_nzb}
<feed xmlns="http://www.w3.org/2005/Atom">
<entry>
   <title type="text">F_Form1</title>
   <updated>1970-01-01T00:00:00Z</updated>
   <content type="application/xml">
      <F_Form1 xmlns="" form_id=2b2c2b58-520a-45c3-8438-8bbaa2f9aaa9" pressedButton="S_Submit" flowState="ST_Start">
         <F_Amount>19.25</F_Amount>
         <F_Name>Brad Walker</F_Name>
         <F_Age>40</F_Age>
      </F_Form1>
   </content>
</entry>
<entry>
	...
</entry>
...
</feed>
```

It is also possible to POST a single stand alone <entry\> element such as:

``` {#codeblock_yyr_v3l_nzb}
<entry xmlns="http://www.w3.org/2005/Atom">
   <title type="text">F_Form1</title>
   <updated>1970-01-01T00:00:00Z</updated>
   <content type="application/xml">
      <F_Form1 xmlns="" pressedButton="S_Submit" flowState="ST_Start">
         <F_Amount>19.25</F_Amount>
         <F_Name>Brad Walker</F_Name>
         <F_Age>40</F_Age>
      </F_Form1>
   </content>
</entry>
```

<title\>
:   The ID of the form to which this record is being submitted.

<updated\>
:   Mandatory, but its value is replaced with a new timestamp by the server. A value of 1970-01-01T00:00:00Z can always be used.

<content\>
:   Contains the submitted data. The structure of the data within the <content\> element is different for each application, and is based on the list of form items that were used to create the application. The easiest way to find the complete list of elements is to issue a Retrieve REST call and look at the resulting data.

The root element of the submitted data, which in this example is the <F\_Form1\> element, must be in the null namespace, which is xmlns="".
:   The root element must have the pressedButton and flowState attributes.

    -   The flowState is the ID of the current stage of the record. For all Create REST calls, this is always ST\_Start, which is the ID of the Start stage.
    -   The pressedButton indicates the ID of the stage action submit button, which simulates the submission. A submit button ID must be specified to activate the appropriate stage activities and transfer the record to the next appropriate stage.

Upon creation, the new record is assigned a generated unique record UID. This UID can be found in the response data, which is similar to the data returned from a Retrieve action. Response data is only returned when a stand alone <entry\> is POSTed rather than multiple entries in a <feed\>.

## JSON {#section_y4x_w3l_nzb .section}

You can also POST a JSON payload, for example:

``` {#codeblock_vf1_x3l_nzb}
{
         "uid": "324007a4-a04f-4649-8d22-e6c764313f1f",
         "pressedButton" : "S_Submit",
         "flowState": "ST_Start",
         "F_SingleLine1": "Jane",
         "F_SingleLine2": "Test",
         "F_Number1": 24.25
}
```

**Note:** The **uid** is optional. If supplied, it must be unique and use the format displayed in the JSON example. If not supplied, a unique uid is generated.

**Parent topic:**[Data access REST API](ref_data_access_rest_api.md)

