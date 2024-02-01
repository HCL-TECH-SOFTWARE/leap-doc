# Embedding API 

The Embedding API can be used to embed a Leap form directly in another webpage without using an <iframe\>. 
The Leap form will be inserted into the DOM of the hosting page and can be interacted with using the Leap JavaScript API or any custom JavaScript. 
Additionally, the style of items in the Leap form can be customized by the CSS of the hosting page.


## Example 1 - Declarative { .section}

```

<html> 
…  
<body> 
 
    <div id="myLeapDiv"> <!-- Leap form will go here --> </div> 
 
    <script src="https://leap.example.com/apps/api/leap.js" 
		data-leap-config="{launch: {appId: 'e9ec1ed3-c12b-4b5c-8f5e-7a6ff4800a55', formId: 'F_Form1', targetId: 'myLeapDiv'}}">
	</script> 
 
</body> 
</html> 
			
```

## Example 2 - Programmatic { .section}

```

<html> 
… 
<body> 
 
<div id="myLeapDiv"> <!-- Leap form will go here --> </div> 

<script src="https://leap.example.com/apps/api/leap.js"></script> 

<script> 
  function onLeapFormSubmitted (BO) 
  { 
	 alert ("submitted record id: " + submittedBO.getDataId());       
  } 

  function onLeapFormLoaded (app, launchParams) 
  { 
	 app.getForm(launchParams.formId).connectEvent("afterSave", onLeapFormSubmitted); 
  } 

  Leap.onReady = function() { 
	  var launchParams =  
	  { 
		 appId: 'e9ec1ed3-c12b-4b5c-8f5e-7a6ff4800a55', 
		 formId: 'F_Form1', 
		 target: document.getElementById("myLeapDiv"), 
		 locale: 'fr-FR' 
		 callback: onLeapFormLoaded 
	  }; 
	  Leap.launch(launchParams);  
  }; 

</script> 
 
</body> 
</html>  
			
```

## Loading the Leap Embedding UI { .section}

```

<script src="https://leap.example.com/apps/api/leap.js" data-leap-config="[leap configuration]" id="leapJS'"></script>
			
```

-   **id** \(optional\) - fallback for older browsers; the value should always be "leapJS"
-   **data-leap-config** \(optional\) - JSON or the name of an existing JavaScript object. Properties:
    -   locale \(optional\) - indicates the preferred locale to the Leap API. For example, "fr-FR"
    -   **launch** \(optional\) - equivalent to calling **Leap.launch**\(\{…\}\) function with respective parameters \(see below for more details\)
    -   **overwriteExistingDojoConfig** \(optional\) - In some environments, such as HCL Digital Experience or IBM WebSphere Portal, the **djConfig** or **dojoConfig** object may be defined on a page and not used. Set the value of this property to **true** to override it.

Loading the Leap API will result in the creation of global object named Leap.

After initial load of the leap.js, you can define a **Leap.onReady**\(\) function which will be called when the necessary Leap resources have been loaded into the page and the API is ready to be used.

## Embedding a form programmatically { .section}

To embed a Leap form programmatically, call Leap.launch\(\{launch\_params\}\);

\{**launch\_params**\} properties:

|Property|Required?|Description|
|--------|---------|-----------|
|appId|Yes|The Leap application UUID.|
| | |  For example, 'e9ec1ed3-c12b-4b5c-8f5e-7a6ff4800a55'|
|formId|Yes|The Leap form ID.|
| | |  For example, 'F\_Form1'|
|targetId|Either **target** or **targetId** must be provided.|The id of the HTML DOM element to embed the Leap form within.|
| | |  For example, 'myLeapFormDiv'|
|target|Either **target** or **targetId** must be provided.|The HTML DOM element to place the Leap form within.|
|mode|No|Determines the mode for embedding.  Possible values:|
| | | -   '**iframe**': embeds the form in an <iframe\> element. For complete isolation of the form, if necessary|
| | | -   '**embed**' \(default\): embeds the form into the hosting page in a <div\>|
|locale|No|Indicates the preferred locale for the embedded form.|
| | | For example, 'fr-FR'|
|prefSecMode|No|If the form supports both anonymous and authenticated usage, this property can be used to automatically choose the preferred security mode.  Possible values:|
| | | -   '**anon**': for anonymous usage|
| | | -   '**secure**': for authenticated usage|
|callback|No|A callback function which will be called when the application launch completes successfully and the form is ready to be interacted with.  The callback function will be passed the following parameters:
| | | -   **app**: the Leap JavaScript API application object. For more details, see [Interface objects](ref_jsapi_user_interface_objects.md)|
| | | -   **launchParams**: the original launch parameters object, for convenience|

## Known Limitations { .section}

-   Only one Leap form can be embedded on the page at a time.
-   Once the Leap form is embedded, it cannot be changed to a different form or reloaded.
-   The hosting page cannot contain any version of the Dojo JavaScript library. The Leap Embedding API will load its own copy of the Dojo JavaScript library into the hosting page.
-   For authentication, it is expected that the hosting page and the Leap server are configured with single sign-on \(SSO\). Leap’s login UI will not display properly within the hosting page.

## Cross-Domain Usage { .section}

If Leap and the hosting page are in different domains, the Leap front-end must be configured to return appropriate CORS headers.

**Parent topic: **[Reference](reference_toc.md)

