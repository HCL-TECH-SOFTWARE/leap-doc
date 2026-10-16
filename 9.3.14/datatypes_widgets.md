# Data Types { #datatypes_widgets .concept }

Data widgets can declare one of the listed data types, each with additional optional constraints.

Constraints on the data type goes beyond the UI. These constraints will be enforced when data is submitted to the server.

**`string`**

-   A piece of text.
-   Constraints:
    -   `length` : the max number of characters allowed, including multi-byte charaters. Note, if this length is greater than `255` the submitted value will be stored as `CLOB` in the database and will not be sortable. Default value: `50`
    -   `subType`
        -   Email
        -   URL
    -   `format` : limit user's input to specific format, use \# for numbers 0-9, @ for letters A-Z and ? for number or letter
        -   `simplePattern`
        -   `invalidMessage`
    -   `multiValue` - `true` or `false`. If `true`, the value returned by the widget is an array of strings, otherwise it is a single string. The default value is `false`.

```javascript
const myWidgetDefinition = {
   ...
   datatype: {
     type: 'string',
     length: 50,
     format: {
        simplePattern: '#####,#####-####' // US zip code
        invalidMessage: 'Please enter a valid US zip code'
     }
   }
   ...
};
```

**`'boolean'`**

-   A `true` or `false` value. A `null` value is not supported. The default value is `false`
-   Constraints:
    -   None.

**`'number'`**

-   A number.
-   Contraints:
    -   `numberType` : one of `'decimal'` or `'integer'`. Default: `'decimal'`
    -   `decimalPlaces` : if number is a `'decimal'`, will round to the given number of decimal places. Default: `2`
    -   `minValue` : minimum value of number expected. Can be omitted or set to `null` if no minimum
    -   `maxValue` : maximum value of number expected. Can be omitted or set to `null` if no maximum

```javascript
const myWidgetDefinition = {
   ...
   datatype: {
     type: 'number',
     numberType: 'decimal',
     decimalPlaces: 2
   }
   ...
};
```

**`'date'`**

-   A date-only value in `'YYYY-MM-DD'` string format.
-   Custom widgets are expected to handle the setting of the date in a `'YYYY-MM-DD'` string format, or as a `Date` object.
-   Contraints:
    -   `minValue` : minimum value of date expected. Can be omitted or set to `null` if no minimum
    -   `maxValue` : maximum value of date expected. Can be omitted or set to `null` if no maximum

**`'time'`**

-   A time-only value in `'hh:mm'` string format \(24-hour clock\).
-   Contraints:
    -   `minValue` : minimum value of time expected. Can be omitted or set to `null` if no minimum
    -   `maxValue` : maximum value of time expected. Can be omitted or set to `null` if no maximum

**`'timestamp'`**

-   A date-time value in ISO 8601 `'YYYY-MM-DDThh:mmZ'` string format, normalized to the UTC timezone \(denoted by `Z`\)
-   Custom widgets are expected to handle the setting of the date ISO 8601 `'YYYY-MM-DDThh:mmZ'` format, or as a `Date` object.
-   Constraints:
    -   `minValue` : minimum value of time stamp expected. Can be omitted or set to `null` if no minimum
    -   `maxValue` : maximum value of time stamp expected. Can be omitted or set to `null` if no maximum

**`aggregation`**

- Denotes that the widget will capture an array of data
- See [Repeating Sections](widget_aggregation.md) for full details.


**Parent topic:** [Custom Widget API](customwidgetapi_landing.md)

