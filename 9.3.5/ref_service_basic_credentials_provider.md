# Basic Credentials Provider {#ref_service_basic_credentials_provider .reference}

This topic describes Basic Credentials Providers used within a Service Description.

## Purpose of the Basic Credentials Provider { .section}

The Basic Credentials Provider provides a mechanism that allows user name and password credentials to be gathered, and provided to a Service Transport. The credentials that are gathered are specific to a single user session with HCL Leap. These credentials are not shared between multiple sessions and are not accessible to other users or administrators of Leap.

## When to use the Basic Credentials Provider { .section}

When a Service Description needs a set of credentials and the credentials vary based on the user invoking the service call, use the Basic Credentials Provider.

## How to Configure the Basic Credentials Provider { .section}

In general, the Basic Credentials Provider does not need any custom configuration to work. By configuring the Service Description to use the Basic Credentials Provider, Leap collects credentials, and makes them available to the Service Transport configured in the Service Description.

## Sharing Credentials Between Service Descriptions { .section}

In some cases, several Service Descriptions might need to share a set of user credentials. Instead of having the user enter their credentials once per service, the Basic Credentials Provider can be configured to allow multiple Service Descriptions to share user-entered credentials using a realm.

The realm is a property of the Basic Credentials Provider. Its value is the name of the realm to which entered credentials are associated. When multiple Service Descriptions share the realm value, they share the set of credentials.

## Using the Basic Credentials Provider in a Service Description { .section}

The provider ID for the Basic Credentials Provider to enter in a Service Description is: basic

## Credentials Provider Parameters { .section}

|Name|Description|Mandatory|Default|
|----|-----------|---------|-------|
|realm|The name of the realm to use to associate entered credentials so that they can be shared between multiple Service Descriptions.|No|N/A|

## Sample Service Description { .section}

```
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="basic"\>
    <property name="realm" value="myRealm"/\>
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

