# HTTP Service Transport {#http_service_transport .reference}

This topic provides reference information on HTTP Service Transports used in HCL Leap.

## Purpose of the HTTP Service Transport { .section}

The HTTP Service Transport provides a mechanism to communicate with HTTP servers. The transport allows configuration of the URL to request, HTTP method to use, query parameters, and request headers. When combined with the Leap service mapping engine, the HTTP Service Transport extracts data from an HTTP response and makes it available to your application.

## When to use the HTTP Service Transport { .section}

The HTTP Service Transport can be used to communicate with any standard HTTP server. There are some limits on what the HTTP Service Transport can provide, but in most cases, the HTTP Service Transport is all that is required to communicate with a basic HTTP server, or RESTful service.

## How to use the HTTP Service Transport { .section}

The HTTP Service Transport has numerous parameters to configure it to talk to many HTTP Servers. In many cases, only a subset of the available parameters is needed. However, all the parameters can be used for any Service Description. The following sections provide a high-level outline of the parameters needed to configure specific parts of your HTTP request.

Configuring the Request Method
:   All HTTP requests require a request method, which tells the receiving HTTP server what to do with the request.

    The HTTP Service Transport supports all the basic HTTP request methods, including: GET, PUT, POST, and DELETE. The HTTP Service Transport supports configuring the HTTP request method with the request-method parameter. If this parameter is missing, or does not contain a valid HTTP request method, then the default, GET is used.

Configuring the Request URL
:   A URL is required to make an HTTP request. There is no default for this parameter, so it must be provided to the HTTP Service Transport. There are several parameters that affect how the request URL is built: request-url, request-url-postfix, request-url-postfix-encoded, and two dynamic parameters: request-url-postfix-N and request-url-postfix-N-encoded.

    The HTTP Service Transport constructs the URL by starting with the value of request-url and appending postfixes. If request-url-postfix is present, its value is appended to the value of request-url. Before appending, the HTTP Service Transport URL encodes the value of request-url-postfix if the request-url-postfix-encoded flag is not present or if its value is anything other than true. Encoding allows values containing characters that are not valid to be placed into the URL without any harm. Choosing to not encode a value allows it to be appended without modification to the URL.

    For example, consider a Service Description that requires the path to a file as input. Since the path might contain slash \(/\) characters that must be preserved, then request-url-postfix-encoded is set to true. This instructs the HTTP Service Transport to leave the value alone. However, another Service Description might need to include a text string as a path component. In this case, the slash \(/\) or any other characters are encoded such that they do not interfere with the path. In this second case, the request-url-postfix-encoded parameter is set to false or omitted from the Service Description.

    In some cases, having a single postfix does not provide enough flexibility. Therefore, the dynamic parameters request-url-postfix-Nand request-url-postfix-N-encoded are used. The N in each of these parameters refers to its order. During processing, the HTTP Service Transport appends the value of these parameters starting with 0 until it finds a missing parameter. As with the single postfix, encoding is optionally performed on each of the parameters before it is added if the value of the request-url-postfix-N-encoded flag is not present or contains any value other than true.

    For example, if the Service Description contains parameters called request-url-postfix-0, request-url-postfix-1, and request-url-postfix-3, only request-url-postfix-0 and request-url-postfix-1 are appended to the URL.

    While building the request URL if a parameter called request-url-postfix is found, the dynamic parameters are ignored. The Service Description developer must make a conscious choice to use these dynamic parameters.

Configuring Request Parameters
:   Query parameters are configured using parameters with the prefix request-query-. Text after the prefix is considered to be the name of the query parameter to pass. The value of the query parameter comes from the value of the transport parameter, and is encoded to prevent the URL from being disrupted. All parameters with the request-query- prefix are added to the URL. No guarantees are made as to the order in which the query parameters are added. For example, consider a search service that requires the search criteria term to be passed as a query parameter. In order to communicate with this service, the Service Description must have a parameter called request-query-term.

Configuring Request Headers
:   The HTTP Service Transport allows HTTP request headers to be configured using parameters with the prefix request-header-. Text after the prefix is considered to be the name of the header. The value of the request header is the value of the parameter. No escaping or encoding is performed on either the name or value of request headers. Therefore, header configuration must include only characters that are permissible.

Configuring the Request Body
:   HTTP allows a body, or entity, to be sent with PUT and POST requests. In order to allow a Service Description to include a request entity, the HTTP Service Transport sends the contents of the request-entity parameter with the request. The contents of this parameter are ignored if the content of request-method is not PUT or POST.

Configuring HTTP Authentication
:   The HTTP Service Transport supports HTTP Basic and HTTP Digest authentication schemes. There arethreetwo mechanisms through which the credentials can be configured: hard coded in the Service Description, provided through the Java 2 Connector \(J2C\) Authentication Credentials provider, or provided at run time through the Basic Credentials Provider.

:   To hard code the credentials that the HTTP Service Transport uses to authenticate, the request-http-auth-username and request-http-auth-password parameters must be available. The values of these parameters are used during any HTTP authentication challenge for either HTTP Basic or HTTP Digest authentication. The HTTP Service Transport performs any hashing required. Therefore, the values of these parameters must be the plain text version of both the user name and password.

:   Credentials can be provided at run time using the Basic Credentials Provider. Refer to the [Service Description](ref_service_service_description.md) and [Basic Credentials Provider](ref_service_basic_credentials_provider.md) help topic for more information. The HTTP Service Transport only uses credentials provided by the Basic Credentials Provider if the request-http-auth-username and request-http-auth-password parameters are empty.

:   Credentials can be provided using the J2C Authentication Credentials Provider. Refer to the [Java 2 Connector \(J2C\) Authentication Credentials Provider](ref_service_j2c_credentials_provider.md) help topic for more information.

    **Note:** The HTTP Service transport can only use credentials provided by the Basic Credentials provideror the J2C Authentication Credentials Provider if the request-HTTP-auth-username and request-HTTP-auth-password parameters are empty.

:   In addition to HTTP Basic and HTTP Digest authentication, the HTTP Service Transport supports Single Sign on \(SSO\) authentication using the Cookie Credentials Provider. In the case where the request made through the HTTP Service Transports needs to passLeap authentication cookies, the Cookie Credentials Provider can be used. In general, the Cookie Credentials Provider is configured to pass the LtpaToken and LtpaToken2 cookies. Consult the [Service Description](ref_service_service_description.md) and [Cookie Credentials Provider](ref_service_cookie_credentials_provider.md) help topics for information.

Receiving Response Status Information
:   The HTTP Service Transport ensures that the HTTP status code and message are available for consumption. The HTTP status code, for example, 200, 404, or 500, is available in the outbound response-code parameter. Similarly, the outbound response-message parameter contains the status message returned, for example, OK, Not Found, or Server Error.

Receiving Response Headers
:   All the headers that are returned in the HTTP response are made available to the Service Description via dynamic parameters. Each header name is converted to lowercase and appended with response-header-. For example, the content-type header would be available as an outbound parameter called response-header-content-type. The parameter contains the value of the header. In the case where a header contains more than one value, the header values are collapsed into a single comma-separated list.

Receiving the Response Body
:   The entire response body, or entity, is made available via the outbound response-entity parameter.

## Specifying the HTTP Service Transport in a Service Description { .section}

The HTTP Service Transport can be used by specifying its unique ID as the value of the transportId element of the Service Description. The unique ID of the HTTP Service Transport is:

-   HTTPServiceTransport

## Supported Credentials Providers { .section}

The HTTP Service Transport supports the following Credentials Providers:

-   Basic
-   Cookie
-   J2C

## Transport Parameters { .section}

Inbound
:   Inbound parameters are provided to the HTTP Service Transport.

    |Name|Description|Mandatory|Type|Default|
    |----|-----------|---------|----|-------|
    |request-url|Base URL to request.|Yes|String| |
    |request-method|HTTP verb to use when making the request. Acceptable values are GET, PUT, POST, or DELETE.|No|String|GET|
    |request-url-postfix|Postfix to append to the value of request-url.|No|String|N/A|
    |request-url-postfix-encoded|Flag indicating whether the value of request-postfix is encoded. If this parameter is missing or is set to false, the value is URL encoded.|Yes|Boolean|FALSE|
    |request-url-postfix-N|The N postfix to append to the value of request-url. This parameter is only considered if request-postfix is not present.|No|String|N/A|
    |request-url-postfix-N-encoded|Flag indicating whether the value of the corresponding request-postfix-N is encoded. If this parameter is missing or set to false, the value is URL encoded.|No|Boolean|FALSE|
    |request-header-x|The value for the request header x. For example, request-header-accept creates a request header called accept.|No|String|N/A|
    |request-query-x|The value for the query parameter called x. For example, request-query-term creates a query parameter called term.|No|String|N/A|
    |request-entity|The body of the request to send. The UTF-8 character set is used.|No|String|N/A|

Outbound
:   Outbound parameters are returned from the transport as a result of the service invocation.

    |Name|Description|Type|
    |----|-----------|----|
    |response-code|HTTP status code returned by the server. This could be any of the standard values, for example, 200, 400, and 500, or a non-standard code returned by the server.|Integer|
    |response-message|HTTP status message associated with the HTTP status code. The value of this parameter is determined by the server. Generally, this message is a standard status message, for example, OK, Not Found, or Server Error.|String|
    |response-header-x|The value of the response header named x in lowercase. For example, if the response contains the response header Content-Type: text/html then response-header-content-type contains the value text/html.|String|
    |response-entity|The entire response body from the HTTP request. It is assumed that the response uses the UTF-8, or ASCII character set.|String|

## Sample Service Description { .section}

For more examples using the HTTP Service Transport, see [Service Description](ref_service_service_description.md).

```
<?xml version="1.0" encoding="utf-8"?>
<serviceDescription>
  <id>make-http-request</id>
  <defaultLocale>en-us</defaultLocale>
  <transportId>HTTPServiceTransport</transportId>
  <name xml:lang="en-us">Make an HTTP Request</name>
  <description xml:lang="en-us">Makes an HTTP request to the configured URL and returns the result</description>
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

**Parent topic:**[Services](ref_services_toc.md)

