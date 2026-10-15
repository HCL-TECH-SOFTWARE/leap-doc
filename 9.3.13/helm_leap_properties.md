# Defining configuration properties { #helm_leap_properties .concept }

## Required properties

The following properties must be added: 

- **[ibm.nitro.SetupAll.setupStatus](co_configuration_properties.md#setupallsetupstatus)**=start
- **[ibm.nitro.NitroConfig.loginIdIsEmail](co_configuration_properties.md#loginidisemail)**=true
- **[ibm.nitro.NitroConfig.userLookup](co_configuration_properties.md#userlookup)**=false
- **[ibm.nitro.NitroConfig.userGroups](co_configuration_properties.md#usergroups)**=false
- **[ibm.nitro.NitroConfig.enableAdminConfigUI](co_configuration_properties.md#enableadminconfigui)**=true
- **[ibm.nitro.NitroConfig.rootAdminId](co_configuration_properties.md#rootadminid)**=adminUser
- **[ibm.nitro.NitroConfig.reauthOnFailedRequest](co_configuration_properties.md#section_reauthOnFailedRequest)**=true
- **[ibm.nitro.NitroConfig.reauthInNewWindow](co_configuration_properties.md#section_reauthInNewWindow)**=true
- **ibm.nitro.NitroConfig.memberManagerType**=liberty-user-registry
{% if isDWLeap %}
- **ibm.nitro.NitroConfig.commonNavBarService**=https://navbar.example.com
- **[ibm.nitro.NitroConfig.serverURI](co_configuration_properties.md#section_serveruri)**=https://forms.example.com/leap
- **[ibm.nitro.NitroConfig.blockAnonAccess](co_configuration_properties.md#section_blockanonaccess)**=disabled
- **[ibm.nitro.LogoutServlet.postLogoutRedirectURL](co_configuration_properties.md#section_logout)**=https://auth.example.com/auth/protocol/oidc/logout?client_id=leap&post_logout_redirect_uri=https://forms.example.com/leap/secure/org/ide/manager.html
{% endif %}

{% if isLeap %}
!!!note
    If the configuration regarding **loginIdIsEmail**, **userLookup**, and **userGroups** does not suit your organizational needs, contact HCL Support for a possible workaround.
{% endif %}

## Optional properties

{% if isLeap %}
- **[ibm.nitro.NitroConfig.serverURI](co_configuration_properties.md#section_serveruri)**=https://forms.example.com/leap
- **[ibm.nitro.NitroConfig.blockAnonAccess](co_configuration_properties.md#section_blockanonaccess)**=disabled
{% endif %}
- **[ibm.nitro.NitroConfig.appFilesWhiteList](co_configuration_properties.md#appfiles)** = css js svg png gif bmp jpg webp txt pdf ttf otf woff woff2 swf mpg mp4 xml
- **[ibm.nitro.NitroConfig.attachmentFilesWhiteList](co_configuration_properties.md#section_attachmentfiles)** = png gif bmp jpg webp txt pdf odt ods odp doc docx ppt pptx xls xlsx csv tsv log leap mpg mp4 xml

For additional optional properties, see [Configuration properties](co_configuration_properties.md).

## Example

Below is an example snippet of setting product-specific properties:

```yaml
configuration:
   leap:
      . . .
     leapProperties: | 
        ibm.nitro.SetupAll.setupStatus=start
        ibm.nitro.InfoEntryPoint.dailyInfo=<div>Welcome to <b>HCL {{shortLeapProductName}} {{currentLeapVersion}}</b> in Kubernetes!</div> 
        ibm.nitro.NitroConfig.serverURI=http://myleapserver.example.com
        ibm.nitro.NitroConfig.loginIdIsEmail=true
        ibm.nitro.NitroConfig.userLookup=false
        ibm.nitro.NitroConfig.userGroups=false
        ibm.nitro.NitroConfig.enableAdminConfigUI=true
        ibm.nitro.NitroConfig.rootAdminId=adminUser
```

For more information, see [Configuration properties](co_configuration_properties.md).

**Parent topic:** [Preparation](helm_preparation.md)

