# User Tracking with HCL Volt MX Foundry

The Leap user tracking feature leverages MX Foundry Reports to monitor active users and track detailed application usage. 

## Prerequisites

1. Have access to **HCL Volt MX Foundry** console.
2. Create a Foundry app, publish the app, and prepare the serviceUrl, appKey, and appSecret for Leap to communicate with Foundry. 
Refer to [HCL Volt MX Foundry](https://opensource.hcltechsw.com/volt-mx-docs/95/docs/documentation/Foundry/voltmxFoundryFundamentals.html) for details.

## Setup and verification

1. The Leap Admin configures the MX Foundry App information in the Leap_config.properties file or through the Admin configuration page to establish communication between Leap and the MX Foundry server.
(Once the Admin configuration page is used, the corresponding entry in Leap_config.properties will no longer take effect.)
2. Leap designers create Leap apps as usual.
3. Leap end users interact with Leap apps runtime, user tracking requests are automatically sent to the Foundry server in the background.
4. To verify that the configuration is correct and communication between Leap and MX Foundry is successful, open an app form or app page in the browser, open the browser’s console tab, and check "Integrity Successful" is showing, that means user tracking feature is working, otherwise see below troubleshooting section.
5. Leap user data will appear in Foundry Reports (with a delay of approximately 20 minutes).

## Known Limitations:

For Leap apps deployed prior to this feature release, user tracking will not be available until those apps are re-deployed.

## Troubleshooting 
To diagnose issues with user tacking feature, access the Leap app runtime in your browser and open the browser’s console or network tab, check for errors and response status for request send to Foundry

1. 401 (Unauthorized) Response:
    This indicates that the AppKey or AppSecret is incorrect.
2. 404 (Not Found) Response:
    This suggests that the serviceURL is incorrect.
3. net::ERR_NAME_NOT_RESOLVED:
     This points to a network connection issue or an inability to resolve the domain name.

## Data Protection
Data that is sent to Volt MX Foundry is well segregated and properly access controlled. 

The Volt MX Foundry GDPR Policy section provides settings that enable the protection of the Personally Identifiable Information (PII) of a user, refer to [HCL Volt MX Foundry](https://opensource.hcltechsw.com/volt-mx-docs/95/docs/documentation/Foundry/vmf_integrationservice_admin_console_userguide/Content/Runtime_Configuration.html#gdpr-policy) for more information.