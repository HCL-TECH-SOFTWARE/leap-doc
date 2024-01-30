# Strict CSP {#leap_strict_csp .concept}

HCL Leap 9.3.1 has a limited capability to restrict the rendering of Leap Forms using a “Strict CSP” policy.

Strict CSP mode can be enabled using the `ibm.nitro.NitroConfig.runtimeCSP` configuration parameter. For example:

``` {#codeblock_rlp_hp3_rvb}
ibm.nitro.NitroConfig.runtimeCSP=script-src 'self' 
https://trusted.example.com 'nonce-{nonce}'; object-src 'none'; 
base-uri 'none'; style-src 'self' https://trusted.example.com 
'nonce-{nonce}';
```

The `{nonce}` token is replaced with a generated, cryptographically strong random nonce when serving up the Leap form’s HTML page. The nonce is applied as an attribute to all `<script>` and `<style>` tags on the page.

When using the [Embedding API](ref_embedding_api.md), the product is not in control of the page and therefore needs to be informed of the nonce value in the `data-leap-config` attribute so that it can load the product’s scripts in a secure manner. Furthermore, the value of the `data-leap-config` attribute must be valid JSON syntax. For example:

``` {#codeblock_mzc_4p3_rvb}
<script
   src="https://leap.example.com/apps/api/leap.js"  
   data-leap-config="{
     &quot;cspNonce&quot;: &quot;ABC123DEF456&quot;
     &quot;launch&quot;: {
       &quot;appId&quot;: &quot;e9ec1ed3-c12b-4b5c-8f5e-
7a6ff4800a55&quot;, 
       &quot;formId&quot;: &quot;F_Form1&quot;, 
       &quot;targetId&quot;: &quot;myLeapDiv&quot;
     }
   }">
</script>

```

## Limitations {#section_gb5_qp3_rvb .section}

-   Strict CSP only covers the rendering of Leap Forms. This includes fill and submit of a new record, and the update of existing records:
    -   As a stand-alone HTML page
    -   Embedded within an IFRAME
    -   Embedded with the non-IFRAME [Embedding API](ref_embedding_api.md)
-   Strict CSP is not applied to any other runtime pages or scenarios, such as App Pages, View Data, or Summary Charts.
-   Strict CSP is not applied to any aspects of Leap’s authoring environment.
-   When using the Embedding API, if you want a callback function to be called after the form has been launched, it cannot be specified in the `data-leap-config` attribute. It must be supplied by providing as a parameter to `Leap.launch()` function.
-   JavaScript \(.js\) files contained in the application will no longer be evaluated in context, therefore the `app` variable will not be available. The global `NitroApplication` variable should be used instead.
-   All existing applications must be redeployed if the `ibm.nitro.NitroConfig.runtimeCSP` config value contains the `{nonce}` token.
-   In rare cases, some forms may fail to render when Strict CSP is enabled and JavaScript security is enabled \(ie. when `ibm.nitro.ApplicationCompilerService.secureJS=false` is enabled or unset\). This depends on the exact product features being used.
-   Errors regarding inline styles will appear in the browser console, however effort has to been made to ensure there are no noticeable side-effects for end-users, with the following exceptions:
    -   Styles applied to the content of the Text widget might not be preserved - these would be inline-styles and therefore not allowed by the browser in Strict CSP mode.
-   The Rich Text Entry and Data Grid items will not render with Strict CSP enabled, because of limitations in 3rd-party libraries.

## Known risks {#section_zbc_jq3_rvb .section}

-   As mentioned above, the non-IFRAME Embedding API does not have control of the page, and therefore needs to be informed of the nonce token by the hosting page. The Embedding API will nullify the cspNonce value once the form launch is complete; however, there will be a short period of time where the nonce is available to other scripts running on the page. It is the responsibility of the customer to ensure that this temporary exposure of the nonce cannot be exploited.
-   As mentioned above, Strict CSP only applies to the rendering of Leap Forms. It is the responsibility of the customer to ensure other product pages \(ex. App Pages\) are not exposed to an audience that is meant to be protected by Strict CSP.
-   Not all browsers may support CSP equally. It is the responsibility of the customer to ensure the CSP header is configured with suitable fallbacks, if necessary for their user-base.

**Parent topic:**[Administering Leap](administering_leap.md)

