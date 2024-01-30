# Java 2 Connector \(J2C\) Authentication Credentials Provider {#ref_service_j2c_credentials_provider .reference}

This topic describes J2C Authentication Credentials Providers that are used within a Service Description.

## Purpose of the J2C Credentials Provider { .section}

The J2C Authentication Credentials Provider provides a mechanism that allows user name and password credentials to be provided to a Service Transport without being hardcoded within the Service Description. The credentials are defined by the WebSphere® Application Server administrator and associated with an alias that is then used within the Service Description.

## When to use the J2C Credentials Provider { .section}

Use the J2C Authentication Credentials Provider when a Service Description needs to define a static set of credentials, typically used to access a backend resource or service, and not specific to a particular user starting the service.

## How to Configure the J2C Credentials Provider { .section}

To use the J2C Authentication Credential Provider, the WebSphere Application Server administrator must first define a user identity \(User ID, Password, and Alias name\) within the JAAS – J2C authentication data section of the WebSphere Application Server administrative console. For an example of the WebSphere Application Server Network Deployment 8.5.5, see the [WebSphere Application Server documentation](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/usec_j2cauthdata.html).

## Using the J2C Credentials Provider in a Service Description { .section}

The provider ID for the J2C Credentials Provider to enter in a Service Description is: j2cAlias

## Credentials Provider Parameters { .section}

|Name|Description|Mandatory|Default|
|----|-----------|---------|-------|
|alias|The Alias name of a user identity that contains the credentials that are required for the Service Description.|Yes|N/A|

## Sample Service Description { .section}

```
<serviceDescription>
   <id>watsonTranslateJ2C</id>
   <defaultLocale>en</defaultLocale>
   <transportId>HTTPServiceTransport</transportId>
   <name xml:lang="en">Watson Translator J2C</name>
   <description xml:lang="en">
 	Translate text using the bluemix Watson Service
   </description>
	<credentials providerId="j2cAlias">
		<property name="alias" value="someNode01/BlueMixTranslateService"/>
	</credentials>
   <inbound>
	   <parameters>
			<parameter>
				<id>text</id>
				<type>STRING</type>
				<name xml:lang="en">Text</name>
				<description xml:lang="en">Text to be translated</description>
				<mandatory>true</mandatory>
			</parameter>
			<parameter>
				<id>model_id</id>
				<type>STRING</type>
				<name xml:lang="en">Model ID</name>
				<description xml:lang="en">Translation to be performed (ex. 'en-fr' to translate from English to French)</description>
				<mandatory>true</mandatory>
			</parameter>
		</parameters>
	<serviceMapping>
	  <constants>
		<constant>
		  <id>request-url</id>
		  <value>https://gateway.watsonplatform.net/language-translation/api/v2/translate</value>
		</constant>
		<constant>
		  <id>request-method</id>
		  <value>GET</value>
		</constant>
	  </constants>

	  <mapping xmlns="">
		<mapping target="transport:request-url" source="constant:request-url"/>
		<mapping target="transport:request-method" source="constant:request-method"/>
		<mapping target="transport:request-query-txt" source="parameter:text"/>
		<mapping target="transport:request-query-model_id" source="parameter:model_id"/>
	  </mapping>
	</serviceMapping>
  </inbound>

   <outbound>
 	<parameters>
 	  <parameter>
 		<id>response-entity</id>
 		<type>STRING</type>
		<name xml:lang="en">Translated Text</name>
 		<description xml:lang="en">Text containing new translation.</description>
 	  </parameter>
 	</parameters>
   </outbound>
</serviceDescription>
```

**Parent topic:**[Services](ref_services_toc.md)

