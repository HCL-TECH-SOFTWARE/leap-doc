# Security hardening

This page outlines some basic guidelines for ensuring that your Leap server is operating securely. Several out of the box security hardenings should be applied.

```
configuration:
  leap:
  . . .
  configOverrideFiles:
    securityOverride.xml: | 
    <server description="leapServer"> 
      <webAppSecurity httpOnlyCookies="true" trackLoggedOutSSOCookies="false"/>
      <httpDispatcher enableWelcomePage="false" />
      <httpOptions removeServerHeader="true" />
      <httpSession invalidateOnUnauthorizedSessionRequestException="true" cookieHttpOnly="true"/>
    </server>
```

The `httpOnlyCookies` setting, tells browsers to restrict the use of LTPA cookies to only HTTP connections.

The `trackLoggedOutSSOCookies` setting, when enabled, ensures that if a user logs out from one browser, the same user will be required to log in again if they try to access the resource from another browser. This setting helps prevent session replay attacks by marking the LTPA cookie as invalid upon logout.

However, enabling `trackLoggedOutSSOCookies` can impact your SSO scenarios. For example, if a user logs in from multiple browsers to the same server and logs out from one browser, they must log in again if they try to access the resource from another browser. As a result, `trackLoggedOutSSOCookies` is set to `false` by default but can be enabled for production environments.

The `enableWelcomePage` setting, disables the Open Liberty welcome page, which is enabled by default.

The `removeServerHeader` setting, impacts information returned to browsers or web clients about the server implementation.

The `cookieHttpOnly` setting, can help to prevent cross-site scripting attacks. When the value is set to `true`, this attribute specifies that session cookies must include the HttpOnly field. Browsers that support the HttpOnly field don’t allow client-side scripts to access cookies.

To allow HTTP access for developer setups with the Docker image, SSL only has not been enforced.

Do not enter passwords into any override as plain text, use the [securityUtility](https://openliberty.io/docs/latest/reference/command/securityUtility-encode.html) to encode them or create a [Kubernetes secret](https://opensource.hcltechsw.com/leap-doc/9.3.13/helm_admin_customsecret.html#section_nc2_1l4_hzb).

For more information about security hardening for applications hosted by Open Liberty, see [Security hardening for production](https://openliberty.io/docs/latest/security-hardening.html);