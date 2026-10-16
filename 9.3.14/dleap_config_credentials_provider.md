# Leap Configuration Credentials Provider

The Leap Configuration Credentials Provider provides a mechanism that allows user name and password credentials to be provided to a Service Transport without being hardcoded within the Service Description. The credentials are defined by the Domino Leap server administrator and are associated with an alias that is used in the Service Description.

Use the Leap Configuration Credentials Provider when a Service Description needs to define a static set of credentials - it is typically used to access a backend resource or service, and is not specific to a particular user starting the service.

## Configuring the Leap Configuration Credentials Provider

To use the Leap Configuration Credentials Provider, the Domino Leap administrator must first define a user identity (User name, Password, and alias name) within the Domino Leap configuration database (VoltConfig.nsf). To do this, complete the following steps:

1. Use the HCL Notes client to open VoltConfig.nsf.

2. Select the **All Service Credentials** view.

3. Select **New Credential Set**.

4. Enter the alias.

5. OPTIONAL: Complete the Description field. The intent of this field is to help you remember the purpose of these credentials. As an example, "Credentials for the Acme Widget API".

6. Enter the User name.

7. Enter the Password.

8. Select **Done** and choose to save the credentials.

When you save your credentials, the user name and password fields are automatically encrypted. Another administrator of the same Leap Configuration database cannot read the encrypted data unless you have added them to the Consumers field. However, all administrators may read the credentials alias and description.

## Using the Leap Configuration Credentials Provider in a Service Description

The provider ID for the Leap Configuration Credentials Provider to enter in a Service Description is: Leap Configuration.

## Credentials Provider Parameters

- alias: Required.  The alias name of a user identity that contains the credentials that are required for the Service Description. This value must match the alias of a credentials set in VoltConfig.nsf. 

## Sample Service Description

```xml
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
  <credentials providerId="Leap Configuration">
    <property name="alias" value="Acme Widgets"/>
  </credentials>
  . . .
</serviceDescription>
```

**Parent topic:** [Services](ref_services_toc.md)