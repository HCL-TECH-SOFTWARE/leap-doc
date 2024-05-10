# Cookie Credentials Provider {#ref_service_cookie_credentials_provider .reference}

This topic describes Cookie Credentials Provider used within a Service Description.

## Purpose of the Cookie Credentials Provider { .section}

The Cookie Credentials Provider provides a mechanism through which cookies between the Leap and the web browser can be made available to a Service Transport.

## When to use the Cookie Credentials Provider { .section}

The Cookie Credentials Provider is used when Leap and the endpoint of a Service share common Single Sign-On \(SSO\) credentials.

For example, Leap and a service application are installed into the same SSO domain configured using Lightweight Third-Party Authentication \(LTPA\). The Cookie Credentials Provider is used to pass the LTPA tokens that were generated at login by Leap to the service application when a service call is made.

## How to Configure the Cookie Credentials Provider { .section}

By default, the Cookie Credentials Provider does not make any cookies available to the Service Transport. In order to make cookies available to a Service Transport, the Cookie Credentials Provider must be configured. The value of the cookie’s property is a comma-separated list of cookie names. Any request cookies that have the same name, based on a case insensitive comparison, as the names in the cookies property are made available to the Service Transport.

## Using the Cookie Credentials Provider in a Service Description { .section}

The provider ID for the Cookie Credentials Provider to enter in a Service Description is: cookie

## Credentials Provider Parameters { .section}

|Name|Description|Mandatory|Default|
|----|-----------|---------|-------|
|cookies|A comma-separated list of cookie names available to the Service Transport|No|N/A|

## Sample Service Description { .section}

```xml
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="cookie"\>
    <property name="cookies" value="LtpaToken,LtpaToken2"/\>
  </credentials\>
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

**Parent topic: **[Services](ref_services_toc.md)

