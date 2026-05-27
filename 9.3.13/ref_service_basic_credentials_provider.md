# Basic Credentials Provider { #ref_service_basic_credentials_provider .reference }

This topic describes Basic Credentials Providers used within a service description.

## Purpose of the Basic Credentials Provider { .section }

The Basic Credentials Provider provides a mechanism that allows user name and password credentials to be gathered, and provided to a Service Transport. The credentials that are gathered are specific to a single user session with {{fullProductName}}. These credentials are not shared between multiple sessions and are not accessible to other users or administrators of {{shortProductName}}.  The credentials may also be defined by the {{shortProductName}} server administrator and associated with an alias that is used in the service description. {% if isLeap %}The value of the alias will depend on the deployment environment of Leap.  The alias can refer to environment variables (when deployed to Kubernetes) or a Java 2 Connector (J2C) Authentication Data (when deployed to WebSphere).{% endif %}

## When to use the Basic Credentials Provider { .section }

When a service description needs a set of credentials and the credentials vary based on the user invoking the service call, use the Basic Credentials Provider.

## How to Configure the Basic Credentials Provider { .section }

In general, the Basic Credentials Provider does not need any custom configuration to work. By configuring the service description to use the Basic Credentials Provider, {{shortProductName}} collects credentials, and makes them available to the Service Transport configured in the service description.

{% if isLeap %}
To use the 'alias' with an authentication data credential, the WebSphere Application Server administrator must first define a user identity (User ID, Password, and Alias name) within the JAAS – J2C authentication data section of the WebSphere Application Server administrative console. For an example of the WebSphere Application Server Network Deployment 9.0.5, see the [WebSphere Application Server documentation](https://www.ibm.com/docs/en/was-nd/9.0.5?topic=jaas-java-2-connector-authentication-data-entry-settings).
{% endif %}

{% if isDominoLeap %}
To use the 'alias' property, the Domino Leap administrator must first define a user identity (User name, Password, and alias name) within the Domino Leap configuration database (VoltConfig.nsf). To do this, complete the following steps: 

### Use the HCL Notes client to open VoltConfig.nsf.

1. Select the All Service Credentials view.

1. Select New Credential Set.

1. Enter the alias.

1. OPTIONAL: Complete the Description field. The intent of this field is to help you remember the purpose of these credentials. As an example, "Credentials for the Acme Widget API".

1. Enter the User name.

1. Enter the Password.

1. Select Done and choose to save the credentials.

!!! note
    When you save your credentials, the user name and password fields are automatically encrypted. Another administrator of the same Leap Configuration database cannot read the encrypted data unless you have added them to the Consumers field. However, all administrators may read the credentials alias and description.
{% endif %}

## Sharing Credentials Between Service Descriptions { .section }

In some cases, several service descriptions might need to share a set of user credentials. Instead of having the user enter their credentials once per service, the Basic Credentials Provider can be configured to allow multiple service descriptions to share user-entered credentials using a realm.

The realm is a property of the Basic Credentials Provider. Its value is the name of the realm to which entered credentials are associated. When multiple service descriptions share the realm value, they share the set of credentials.

## Using the Basic Credentials Provider in a Service Description { .section }

The provider ID for the Basic Credentials Provider to enter in a service description is: basic

## Credentials Provider Parameters { .section }

|Name|Description|Mandatory|Default|
|----|-----------|---------|-------|
|realm|The name of the realm to use to associate entered credentials so that they can be shared between multiple service descriptions.|No|N/A|
|alias|The alias name of a user identity that contains the credentials that are required for the Service Description. This value must match the alias of a credentials set in VoltConfig.nsf.|Yes|N/A|

## Sample Service Description using 'realm' property { .section }

```xml
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="basic">
    <property name="realm" value="myRealm" />
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

## Sample Service Description using 'alias' property

```xml
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="basic">
    <property name="alias" value="myServiceCredential"/>
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

