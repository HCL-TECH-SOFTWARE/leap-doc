# Public render parameters {#publicrenderparameters .reference}

Public render parameters are leveraged to allow the Leap Portlet to communicate with other portlets. One type of public render parameter instructs the Leap Portlet to load a specific application.

## Open Given Application { .section}

The Leap Portlet opens a form when you specify the application URL as the value of the render parameter.

**Note:** The code must be entered as a single line.

```
[Plugin:RenderURL pr1.value="\{Application URL\}" pr1.key="{http://www.ibm.com/pb/models}openURL"
 copyCurrentParams="true" pr1.mode="set" pr1.type="public"]
```

Where Application URL is a URL pointing to the Leap application.

The format of the Application URL to launch a blank form is: /landing/org/app/<app id\>/launch/index.html?form=<form id\>.

The format of the Application URL to launch the form for a specific record is: /landing/org/app/<app id\>/launch/index.html?form=<form id\>&id=<rec id\>

For more information on the **app id**, **form id**, and **rec id**, see the [developerWorks® Leap wiki](https://hclleapwiki.atlassian.net/wiki/spaces/HL/pages/65698/Launch+Other+Forms).

## Send data { .section}

When data is pushed into the Leap portlet, the **onDataReceived** event fires. The event handler shares the contents of the string as a **pData** parameter, however it is up to the event to understand the contents of the string.

```
[Plugin:RenderURL pr1.value="<your data>" copyCurrentParams="true" pr1.key="{http://www.ibm.com/pb/models}payload" 
   pr1.mode="set" pr1.type="public"]
```

Where your data is the string you want sent to the Leap application.

For more information on render parameters, see [WebSphere® Portal Render Parameters](http://www-01.ibm.com/support/knowledgecenter/SSHRKX_8.5.0/help/panel_help/plrf_rendr_plugin_render_url.dita)

**Usage Details**

If you have multiple Leap Portlets in your Portal site, you can control which Forms Experience Portlet responds to the public render parameters by setting the param.sharing.scope parameter for your portal page. For more information, see [How to control parameter sharing in the portal](http://www-01.ibm.com/support/knowledgecenter/SSYJ99_8.5.0/dev-portlet/pltcom_pubrndrprm.html). Once a FEB Portlet responds to these actions, it will continue to do so until directed to perform another action.

