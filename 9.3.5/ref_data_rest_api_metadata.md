# Metadata {#reference_adn_qqt_nv .reference}

This JSON-only action retrieves a description of the items in your form.

**Note:** The curl command must be entered as a single line.

```
curl --user <loginId>:<passwd> http://<host>:<port>/apps-basic/secure/org/data/
dd34da19-15c4-4267-8f1e-9f12ece743d7/F_Form1/metadata
```

```
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
            }
}
```

**Parent topic: **[Data access REST API](ref_data_access_rest_api.md)

