# Page Events 

This topic describes the Page Events, and their parameters when using JavaScript™ API in HCL Leap.

There are many events available to hook into on a page that are accessed from the page **Edit Properties** dialog.

Table 1. JavaScript™ objects available in page events

|Variable|Full name|Description|Example|Type|
|--------|---------|-----------|-------|----|
|app|Application object|Contains functions for accessing global general information|`app.isSingleFormView()`|GUI|
|form|Form object|For accessing the pages and controlling page navigation|`form.getPage('P_Page1');`|GUI|
|page|Page object|For accessing the Page and the items on it|`page.F_Text.setContent('This a Label');`|GUI|
|BO|Business Object object|Top-level data object for the form|`BO.F_Username.getValue();`|DATA|

Table 2. Page Events

<table class="table-wrap">
<tr>
<td width="175"> <b>Event</b> </td><td> <b>Description</b> <td><b>Example</b></td>
</tr>
<tr>
<td>onHide
<td>Called when the page is hidden. This is usually a result of page navigation.
<td>
</tr>
<tr>
<td>onNavigateAway
<td>Called as the page is about to be switched away from this one. A pAllowSwitch variable is passed to this event that contains one property called allow. Setting this property to false cancels the page switch.
<td>Cancel the page switch if a check box is not checked:

```JavaScript
if(!BO.F_Agree.getValue())
   pAllowSwitch.allow = false;
```

</tr>
<tr>
<td>onRemoveFromNavigation
<td>Called when this page is removed from navigation by calling the form.removePageFromNavigation() method for this page.
<td>
</tr>
<tr>
<td>onRestoreFromNavigation
<td>Called when a page is restored to navigation by calling the form.restorePageNavigation() method for this page.
<td>
</tr>
<tr>
<td>onShow
<td>Called every time the page is shown. This includes when the form is first displayed and when the user navigates to the page. A good location to update any display items. <br>

<b>Note:</b> When a form is first opened, this event is only called on the current displayed page.
<td>
</tr>
</table>


**Parent topic: **[Running Custom JavaScript – Events](ref_jsapi_running_custom_js_events.md)

