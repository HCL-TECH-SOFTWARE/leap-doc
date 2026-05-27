# Header Credentials Provider

This topic describes the Header Credentials Provider used within a service description.

## Purpose of the Header Credentials Provider

The Header Credentials Provider allows client request headers to be passed to a service transport. It is primarily used with the HttpServicesTransport when making HTTP requests to external services.

## When to use the Header Credentials Provider

When you need to propagate headers that exist in a user's browser to a service being invoked, use the Header Credentials Provider.

**Limitations**

- will not propagate "Cookie" header, use [CookieCredentialsProvider](ref_service_cookie_credentials_provider.md)
- will not propagate Authorization header over non-TLS http requests

## Using the Header Credentials Provider in a service description 

The **providerId** for the Header Credentials Provider to enter in a service description is "header".

## Credential Provider Parameters

|Name|Description|Mandatory|Default|
|----|-----------|---------|-------|
|headers|A comma-separated list of header names to be passed on to the service transport.|Yes|N/A|

## Sample Service Description 

```xml
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="header">
    <property name="headers" value="User-Agent,X-Auth-Header,Accept-Language" />
  </credentials>
  <inbound>
    <parameters>
      <parameter>
        <id>request-url</id>
        <name xml:lang="en-us">URL</name>
        <description xml:lang="en-us">URL to request.</description>
        <mandatory>true</mandatory>
        <type>STRING</type>
      </parameter>
      <parameter>
        <id>request-method</id>
        <name xml:lang="en-us">Method</name>
        <description xml:lang="en-us">HTTP method to use, one of GET, PUT, POST, or DELETE.</description>
        <mandatory>true</mandatory>
        <type>STRING</type>
      </parameter>
    </parameters>
  </inbound>
  <outbound>
    <parameters>
      <parameter>
        <id>response-entity</id>
        <name xml:lang="en-us">Response</name>
        <description xml:lang="en-us">Response returned by making a request to the configured URL.</description>
        <mandatory>false</mandatory>
        <type>STRING</type>
      </parameter>
    </parameters>
  </outbound>
</serviceDescription>
```

**Parent topic:** [Services](ref_services_toc.md)