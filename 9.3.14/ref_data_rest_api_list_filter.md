# Filtering Data REST API results 

The following information describes how to filter Data REST API results.

You can filter the results of the **List** action by providing extra URL parameters. For example:

```
/{{apiContext}}/secure/org/data/{app-uid}/{form-id}?F_Amount__lt=1000
```

This sample query would limit results to records whose **F\_Amount** currency field value is less than 1000. The syntax of a single filter parameter is `{element}__{operator}={value}`, where `{element}` is the ID of an item in the form, or one of the record metadata properties. For example, the author\_name is used to filter by the name of the initial submitter of a record.

!!! note
    All filter parameters must be properly URL encoded. Common encoding characters are described as follows:

-   **%3A** - a colon
-   **%20** - a space
-   **%2B** - the plus sign \(+\)

For example, the colon in a time value of “09:40” would need to be encoded as **%3A** resulting in an encoded value of **09%3A40**.

Two simple examples of single filter parameters are:

**F\_Age\_\_equals=5**

**author\_name\_\_equals=James%20Smith**

## Multiple Filters { .section}

Multiple filter parameters can be included in a single URL along with a searchOperator parameter.

**OR**  
In an OR relationship, any one of the filters is true.

```
?{element1}__{operator1}={value1}&{element2}__{operator2}={value2}&searchOperator=OR
```

**AND**  
In an AND relationship, all of the filters must be true.

```
?{element1}__{operator1}={value1}&{element2}__{operator2}={value2}&searchOperator=AND
```

!!! note
    Only a single **searchOperator** parameter is supported in a request. You cannot use both AND and OR in a single request. If no **searchOperator** parameter is present, the default is AND.

## Metadata properties { .section}

Each record can use the following properties for filtering.

|Element|Operator Type|Description|
|-------|-------------|-----------|
|author\_name|See the table of **String Operators**|The name of the user that initially created the record.|
|updater\_name|See the table of **String Operators**|The name of the user that last updated the record.|
|creation\_time|See the table of **Time Stamp Operators**|The time stamp of when the record was initially created.|
|updated|See the table of **Time Stamp Operators**|The time stamp of when the record was last updated|
|flow\_state|See the table of **Stage Operators**|The ID of the stage that the record is in. For example, “ST\_End”|

{% if isLeap %}
## Global operators

All items can use the following global operators for filtering.

|Operator|Description|
|--------|-----------|
|hasvalue|Checks to see whether the value of the element is not empty.|
|not_hasvalue|Checks to see whether the value of the element is empty.|
{% endif %}

## String Operators { .section}

String operators are used on the values of the following form items: **Single-Line Entry**, **Multi-Line Entry**, **Email**, **Drop Down**, **Select One**, **Select Many**, **Survey** question, **Choice Slider**, and **Website**. String operators are also used on the following metadata properties: author\_name and updater\_name.

{% if isLeap %}
|Operator|Description|
|--------|-----------|
|equals|The value of the element is tested for equality against the specified value.|
|not_equals|The value of the element is tested for equality against the specified value.|
|contains|Checks to see whether the value of the element contains the specified value.{% if isDominoLeap %}The contains operator only works if the target application has a full text index. If the application does not have a full text index, your request will fail. See the notes below about using wildcards with the contains operator.{% endif %}|
|not_contains|Checks to see whether the value of the element does not contain the specified value.{% if isDominoLeap %}The contains operator only works if the target application has a full text index. If the application does not have a full text index, your request will fail. See the notes below about using wildcards with the contains operator.{% endif %}|
{% if isLeap %}|startswith|Checks to see whether the value of the element starts with the specified value.|
|not_startswith|Checks to see whether the value of the element does not start with the specified value.|
|endswith|Checks to see whether the value of the element ends with the specified value.|
|not_endswith|Checks to see whether the value of the element does not end with the specified value.|
|like|Checks to see whether the value of the element is like the specified value. Use the SQL operators % ( represents zero, one or multiple characters) and _ (represents one single character) to create more refined filters.|
|not_like|Checks to see whether the value of the element is not like the specified value. Use the SQL operators % ( represents zero, one or multiple characters) and _ (represents one single character) to create more refined filters.|{% endif %}
{% endif %}

{% if isDominoLeap %}
|Operator|Description|
|--------|-----------|
|equals|The value of the element is tested for equality against the specified value.|
|contains|Checks to see whether the value of the element contains the specified value. The contains operator only works if the target application has a full text index. If the application does not have a full text index, your request will fail. See the notes below about using wildcards with the contains operator.|

!!! note
    When you use the contains operator, the value you specify may include wildcard characters. Use a question mark (?) in place of a single character in a word. Use an asterisk (*) in place of zero or more characters in a word. For example:

    - **blue** matches the whole word blue  
    - **blue???** matches bluejay, but not bluebird  
    - **blue\*** matches bluebird and bluejay, but not abluent  
    - **\*blue\*** matches all of the above (abluent, blue, bluebird and bluejay)  
{% endif %}

## Number operators { .section}

Number operators are used on the values of the following form items: **Number**, **Currency**, and **Numeric Slider**.

|Operator|Description|
|--------|-----------|
|equals|The value of the element is tested for equality against the specified value.|
|notequals|The value of the element is tested for non-equality against the specified value.|
|gt|Checks to see whether the value of the element is greater than the specified value.|
|lt|Checks to see whether the value of the element is less than the specified value.|
|gte|Checks to see whether the value of the element is greater than or equal to the specified value.|
|lte|Checks to see whether the value of the element is less than or equal to the specified value.|

## Boolean operator { .section}

This operator is only used on the value of the **Checkbox** form item.

|Operator|Description|
|--------|-----------|
|equals|The value of the element is tested for equality against the specified value. Valid values to compare against are **true** and **false**.|

## Time, Date, and Time Stamp operators { .section}

-   Time values are valid against **Time** form items only.
-   Date values are valid against **Date** form items only.
-   Time stamp values are valid against **Time Stamp** form items, or the creation\_time and updated metadata properties.
-   Time, date, and time stamp values must be provided in ISO 8601 extended format. For example, a time stamp for 21 Dec 2015 10:00 AM Pacific Standard Time must be given as: 2015-12-21T10:00:00-08:00 or 2015-12-21T18:00:00Z.

    !!! note
        Remember to take daylight savings into account based on the time zone and the date of a time stamp value. For example, 21 June 2015 10:00 AM Pacific *Daylight* Time must be given as 2015-06-21T10:00:00-**07:00** or 2015-06-21T**17:00**:00Z

-   Dates must be passed in the format **yyyy-mm-dd**
-   Times must be passed in the format **hh\:mm\:ss**
-   Remember that all values must be properly URL encoded. For example, a value of `2015-06-21T17:00:00Z+8:00` must be encoded as `2015-06-21T17%3A00%3A00%2B8%3A00`.

|Operator|Description|
|--------|-----------|
|after|Filters so that the results provided come after the specified time and date.|
|before|Filters so that the results provided come before the specified time and date.|
|between|Filters so that the results provided fit on or within the specified times and dates. The between operator takes a value in the following format: `{start moment}**A*N*D**{end moment}`. For example, to search between the start of day 1 June 2015 and the start of day 8 June 2015 (in Pacific Daylight Time) the value is: `2015-06-01T07:00:01Z**A*N*D**2015-06-08T07:00:01Z`|


## Additional Date and Time Stamp operators { .section}

To adjust for different time zones, use the tzOffset URL parameter. The value is the number of seconds of offset from Coordinated Universal Time. For example, for Pacific Standard Time use tzOffset=-28000

|Operator|Description|
|--------|-----------|
|year|Filters the results so that the year matches the specified numerical value.|
|month|Filters the results so that the month matches the specified numerical value. The value must use the numbers 1-12, where 1 is January and 12 is December.|
|day|Filters the results so that the day matches the specified numerical value. The value must use the numbers 1-31, where each numeral matches a day of the month.|

## Stage ID operators { .section}

Stage operators are used with the value of the flow\_state metadata property.

|Operator|Description|
|--------|-----------|
|equals|The value of the flow\_state is tested for equality against the specified value.|
|notequals|The value of the flow\_state is tested for non-equality against the specified value.|

## Examples { .section}

The following parameters are examples of filtering. Each example contains the search parameter and a description of the returned result.

This filter returns the first 20 records where the value of the F\_Number field is greater than or equal to 5.

```
?F_Number__gte=5&to=20
```

This filter returns the first 30 records of where the record was last updated between the start of day June 1, 2015 and the start of day Aug 31, 2015, China Standard Time.

```
?updated__between=2015-06-01T00%3A00%3A01%2B8%3A00A*N*D2015-08-31T00%3A00%3A01%2B8%3A00&to=30
```

This filter returns first five records where the value of the F\_Currency field is less than 1000 AND the value of the F\_Number field is greater than 10.

```
?F_Currency__lt=1000&F_Number__gt=10&searchOperator=AND&to=5
```

This filter returns the first 20 records where the value of the F\_Number field is less than 5 OR greater than 10.

```
?F_Number__lt=5&F_Number__gt=10&searchOperator=OR&to=20
```

**Parent topic:** [List](ref_data_rest_api_list.md)

