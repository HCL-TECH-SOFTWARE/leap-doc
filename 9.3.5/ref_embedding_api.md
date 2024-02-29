# Embedding API 

The Embedding API can be used to embed a Leap form directly in another webpage without using an <iframe\>. 
The Leap form will be inserted into the DOM of the hosting page and can be interacted with using the Leap JavaScript API or any custom JavaScript. 
Additionally, the style of items in the Leap form can be customized by the CSS of the hosting page.


## Example 1 - Declarative { .section}

```html
<html> 
…  
<body>
   … 
   <div id="myLeapDiv"> <!-- Leap form will go here --> </div> 
   …
   <script src="https://leap.example.com/apps/api/leap.js" 
    data-leap-config="{launch: {appId: 'e9ec1ed3-c12b-4b5c-8f5e-7a6ff4800a55', formId: 'F_Form1', targetId: 'myLeapDiv'}}">
   </script> 
</body> 
</html>
```

## Example 2 - Programmatic { .section}

```html
<html> 
… 
<body> 
  …
  <div id="myLeapDiv"> <!-- Leap form will go here --> </div> 
  …
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

```html
<script src="https://leap.example.com/apps/api/leap.js" data-leap-config="[leap configuration]" id="leapJS'"></script>
```

-   **id** \(optional\) - fallback for older browsers; the value should always be `"leapJS"`
-   **data-leap-config** \(optional\) - JSON or the name of an existing JavaScript object. Properties:
    -   **locale** \(optional\) - indicates the preferred locale to the Leap API. For example, `"fr-FR"`
    -   **launch** \(optional\) - equivalent to calling `Leap.launch({…})` function with respective parameters \(see below for more details\)
    -   **overwriteExistingDojoConfig** \(optional\) - In some environments, such as HCL Digital Experience or IBM WebSphere Portal, the **djConfig** or **dojoConfig** object may be defined on a page and not used. Set the value of this property to **true** to override it.

Loading the Leap API will result in the creation of global object named `Leap`.

After initial load of the leap.js, you can define a `Leap.onReady()` function which will be called when the necessary Leap resources have been loaded into the page and the API is ready to be used.

## Embedding a form programmatically { .section}

To embed a Leap form programmatically, call `Leap.launch({launch_params})`;

**`{launch_params}`** properties:

<table>
<thead>
<tr>
<th>
Property
</th>
<th>
Required?
</th>
<th>
Description
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
appId
</td>
<td>
Yes
</td>
<td>
The Leap application UUID.<br>
For example, 'e9ec1ed3-c12b-4b5c-8f5e-7a6ff4800a55'
</td>
</tr>

<tr>
<td>
formId
</td>
<td>
Yes
</td>
<td>
The Leap form ID.<br>
For example, 'F_Form1'
</td>
</tr>

<tr>
<td>
targetId
</td>
<td>
Either <b>target</b> or <b>targetId</b> must be provided.
</td>
<td>
The id of the HTML DOM element to embed the Leap form within.<br>
For example, 'myLeapFormDiv'
</td>
</tr>

<tr>
<td>
target
</td>
<td>
Either <b>target</b> or <b>targetId</b> must be provided.
</td>
<td>
The HTML DOM element to place the Leap form within.
</td>
</tr>

<tr>
<td>
mode
</td>
<td>
No
</td>
<td>
Determines the mode for embedding.  Possible values:
<ul>
<li><code>'iframe'</code>: embeds the form in an <code>&lt;iframe&gt;</code> element. For complete isolation of the form, if necessary</li>
<li><code>'embed'</code> (default): embeds the form into the hosting page in a <code>&lt;div&gt;</li></ul></td>
</tr>

<tr>
<td>
locale
</td>
<td>
No
</td>
<td>
Indicates the preferred locale for the embedded form.<br>
For example, 'fr-FR'
</td>
</tr>

<tr>
<td>
prefSecMode
</td>
<td>
No
</td>
<td>
If the form supports both anonymous and authenticated usage, this property can be used to automatically choose the preferred security mode.  Possible values:
<ul>
<li><code>'anon'</code>: for anonymous usage</li>
<li><code>'secure'</code>: for authenticated usage</li></ul></td>
</tr>

<tr>
<td>
callback
</td>
<td>
No
</td>
<td>
A callback function which will be called when the application launch completes successfully and the form is ready to be interacted with.  The callback function will be passed the following parameters:
<ul>
<li><code>app</code>: the Leap JavaScript API application object. <!-- For more details, see [Interface objects](ref_jsapi_user_interface_objects.md)--></li>
<li><code>launchParams</code>: the original launch parameters object, for convenience</li></ul></td>
</tr>
</tbody>
</table>

## Known Limitations { .section}

-   Only one Leap form can be embedded on the page at a time.
-   Once the Leap form is embedded, it cannot be changed to a different form or reloaded.
-   The hosting page cannot contain any version of the Dojo JavaScript library. The Leap Embedding API will load its own copy of the Dojo JavaScript library into the hosting page.
-   For authentication, it is expected that the hosting page and the Leap server are configured with single sign-on \(SSO\). Leap’s login UI will not display properly within the hosting page.

## Cross-Domain Usage { .section}

If Leap and the hosting page are in different domains, the Leap front-end must be configured to return appropriate CORS headers.

**Parent topic: **[Reference](reference_toc.md)

