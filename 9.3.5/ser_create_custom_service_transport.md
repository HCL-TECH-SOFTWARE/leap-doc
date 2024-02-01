# Creating your own custom Service Transport {#ser_create_custom_service_transport .task}

By creating a custom Service Transport, you can allow HCL Leap applications to use services from any external system, or access any data source. Alternatively, the transport can implement a custom service itself without communicating with any external system or data source.

If you plan to call an external service using HTTP, consider using the HTTP Service Transport instead. Refer to [HTTP Service Transport](ref_service_http_service_transport.md) for more information.

A custom Service Transport can be added to the Leap environment by creating and deploying an appropriate OSGi JAR bundle. Refer to [Setting up your development environment](ser_setup_development_environment.md) before starting.

1.  Create a Java class

    Create a Java class that implements the com.ibm.form.nitro.service.services.IServiceTransport interface.

    The following example is a Hello example transport that returns a greeting to a person. This transport expects a single input parameter person and responds with a single output parameter greeting. In this simple example, the transport does not talk to any external system to run the service. The transport implements the service itself.

    ```
    package com.mycompany.services;
    
    import com.ibm.form.nitro.service.model.IUser;
    import com.ibm.form.nitro.service.services.*;
    import com.ibm.form.platform.service.framework.i18n.LocaleUtils;
    import java.util.*;
    
    public class HelloServiceTransport
        implements IServiceTransport
    {
    
        public String getId()
        {
            return "com.mycompany.services.HelloServiceTransport.id";
        }
    
        public ServiceResult run(IServiceDescription pDescription,
                                 IServiceCredentialsProvider pServiceCredentialsProvider, IUser pUser,
                                 Map<String, Object> pParameters)
        {
            String personName = (String) pParameters.get("person");
            Locale requestLocale = LocaleUtils.getRequestLocale();
            String greeting = "";
            if (requestLocale.getLanguage().equals(Locale.FRENCH.getLanguage()))
                greeting = "Bonjour" + personName;
            else
                greeting = "Hello " + personName;
            pParameters.put("greeting", greeting);
            ServiceResult result = new ServiceResult(200, "success");
            return result;
        }
    
        public Collection<IServiceDescription> getSampleServiceDescriptions()
        {
            return Collections.emptyList();
        }
    
        public IServiceTransportMetadata getMetadata()
        {
            return new IServiceTransportMetadata()
            {
                public Set<String> getAllowableCredentialsProviderIds()
                {
                    return Collections.emptySet();
                }
            };
        }
    }
    ```

2.  Create an OSGi Service Description

    You must create an .xml file to declare your Java class as an OSGi service. For example, create a HelloServiceTransport.xml file with the following content:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <scr:component xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0" 
      configuration-policy="optional" 
      immediate="true" 
      name="com.mycompany.services.HelloServiceTransport.service">
       <implementation class="com.mycompany.services.HelloServiceTransport"/>
       <service>
          <provide interface="com.ibm.form.nitro.service.services.IServiceTransport"/>
       </service>
    </scr:component>
    ```

    For the class attribute of the implementation element, use the fully qualified name of the Java class you created in Step 1. Ensure that the name attribute of the component element is unique.

    Although not required, you can make it the same as the fully qualified name of the Java class that you created in Step 1.

3.  Create a MANIFEST.MF file

    Sample content:

    ```
    Manifest-Version: 1.0
    Bundle-ManifestVersion: 2
    Bundle-Name: My Company Services
    Bundle-SymbolicName: com.mycompany.services
    Bundle-Version: 1.0.0.b1
    Bundle-Vendor: My Company
    Bundle-RequiredExecutionEnvironment: JavaSE-1.6
    Service-Component: OSGI-INF/*.xml
    Import-Package: com.ibm.form.nitro.service.model,
     com.ibm.form.nitro.service.services,
     com.ibm.form.platform.service.framework.i18n
    ```

    Multiple OSGi services can be packaged within the same OSGi bundle. Therefore, the same MANIFEST.MF file can be used for a custom Service Transport, a custom Service Catalog Group, and a custom Service Catalog.

4.  Deploy the Service Transport.

    Create a .jar file that contains the Java class, OSGi Service Description, and the MANIFEST.MF, created in steps 1 - 3. For example:

    ```
    /
       META-INF/
          MANIFEST.MF
       OSGI-INF/
          HelloServiceTransport.xml
       com/
          mycompany/
             services/
                HelloServiceTransport.class
                HelloServiceTransport$1.class
    ```

    Multiple OSGi services can be packaged within the same OSGi bundle. Therefore, the same .jar file can be used for a custom Service Transport, a custom Service Catalog Group, and a custom Service Catalog.

    On the Leap server, put the .jar file in one the following directories or in a subdirectory of one of the following directories:

    -   Windows™:

        any drive:\\HCL\\Leap\\extensions\\

    -   Non Windows:

        /opt/HCL/Leap/extensions/

    Important notes on directories:

    -   If the extensions directory does not exist, then the Leap server must be restarted after the directory is created.
    -   /opt/HCL/Leap/ is not case-sensitive.

## Sample LDAP query Service Transport { .example}

The following example is a more complex Service Transport that demonstrates one possible way to query an LDAP server. The transport itself remains fairly generic so that multiple different service descriptions, each with their own custom parameters and LDAP search properties, can use this same transport. This sample uses the JVM's naming services \(javax.naming.directory and javax.naming.ldap\) to communicate with the external LDAP server. LDAP search results are converted to XML which can then be pulled apart by the outgoing mapping section of the service description as needed. For example:

```
<searchresults>
	<searchresult>
		<telephone>1-555-555-555</telephone>
		<email>csmith@mycompany.com</email>
		<cn>Chris Smith</cn>
	</searchresult>
	<searchresult>
		...
	</searchresult>
	...
</searchresults>
```

If necessary, the Basic Credentials Provider is used to collect the credentials needed to query the LDAP server.

Sample Java code:

```
package com.mycompany.services;

import com.ibm.form.nitro.service.model.*;
import com.ibm.form.nitro.service.services.*;
import java.io.*;
import java.util.*;
import javax.naming.*;
import javax.naming.directory.*;
import javax.naming.ldap.*;
import javax.xml.parsers.*;
import javax.xml.transform.*;
import javax.xml.transform.dom.*;
import javax.xml.transform.stream.*;
import org.w3c.dom.*;

public class SampleLDAPServiceTransport implements IServiceTransport {

	private IServiceTransportMetadata metaData;

	public String getId() {
		return "com.mycompany.services.SampleLDAPServiceTransport.id";
	}

	public IServiceTransportMetadata getMetadata() {
		if (this.metaData == null) {
			this.metaData = new IServiceTransportMetadata() {
				public Set<String> getAllowableCredentialsProviderIds() {
					Set<String> ids = new HashSet<String>();
					ids.add("basic");
					return ids;
				}
			};
		}
		return this.metaData;
	}

	public Collection<IServiceDescription> getSampleServiceDescriptions() {
		return Collections.emptyList();
	}

	public ServiceResult run(IServiceDescription pDescription, IServiceCredentialsProvider pServiceCredentialsProvider,
			IUser pUser, Map<String, Object> pParameters) {
		if (pParameters == null) {
			pParameters = new HashMap<String, Object>();
		}

		String baseDN = (String) pParameters.get("basedn");

		String filter = (String) pParameters.get("filter");
		List<String> filterArgs = new ArrayList<String>();
		int argIndex = 0;
		while (pParameters.containsKey("filter-arg-" + argIndex)) {
			String filterArgValue = (String) pParameters.get("filter-arg-" + argIndex);
			filterArgs.add(filterArgValue == null ? "" : filterArgValue);
			argIndex++;
		}

		String[] attributes = null;
		if (pParameters.containsKey("result-attributes")) {
			attributes = ((String) pParameters.get("result-attributes")).trim().split("[\\s]*,[\\s]*");
		}

		int resultCountLimit = 50;
		if (pParameters.containsKey("result-count-limit")) {
			resultCountLimit = Integer.parseInt((String) pParameters.get("result-count-limit"));
		}
		int resultCount = 0;
		InitialLdapContext ctx = null;
		try {
			ctx = ldapConnect(pServiceCredentialsProvider, pParameters);
			if (ctx != null) {
				Document doc = createDocument();
				Node rootNode = doc.createElement("searchresults");
				doc.appendChild(rootNode);

				SearchControls sc = new SearchControls();
				sc.setSearchScope(SearchControls.SUBTREE_SCOPE);
				sc.setCountLimit(resultCountLimit);
				sc.setReturningAttributes(attributes);
				sc.setReturningObjFlag(false);
				
				// fetch results
				NamingEnumeration<SearchResult> searchResults = ctx.search(baseDN, filter,
						filterArgs.toArray(new String[0]), sc);
				while (searchResults.hasMore()) {
					Node resultNode = doc.createElement("searchresult");
					rootNode.appendChild(resultNode);
					resultCount++;
					SearchResult result = searchResults.next();
					Attributes resultAttrs = result.getAttributes();
					NamingEnumeration<String> attrIds = resultAttrs.getIDs();
					while (attrIds.hasMore()) {
						String attrName = attrIds.next();
						String attrValue = (String) resultAttrs.get(attrName).get(0);
						Node attrNode = doc.createElement(attrName);
						attrNode.setTextContent(attrValue);
						resultNode.appendChild(attrNode);
					}
				}
				String result = serializeDocument(doc);
				pParameters.put("resultXML", result);
			}
		} catch (AuthenticationException ex) {
			if (pServiceCredentialsProvider != null) {
				return new ServiceResult(401);
			} else {
				return new ServiceResult(500, ex.getLocalizedMessage());
			}
		} catch (Exception ex) {
			return new ServiceResult(500, ex.getLocalizedMessage());
		} finally {
			if (ctx != null) {
				try {
					ctx.close();
				} catch (NamingException ex) {
					// Ignore
				}
			}
		}

		// Success
		return new ServiceResult(200, resultCount + " LDAP search result(s)");
	}

	/**
	 * Creates the LDAP Context used to call to the LDAP server.
	 */
	private InitialLdapContext ldapConnect(IServiceCredentialsProvider pServiceCredentialsProvider,
			Map<String, Object> pParameters) throws NamingException, ServiceException {

		String url = (String) pParameters.get("url");

		Map<String, String> securityInfo = this.getSecurityInfo(pServiceCredentialsProvider, pParameters);
		String securityAuth = securityInfo.get("auth");
		String securityPrincipal = securityInfo.get("principal");
		String securityCredentials = securityInfo.get("credentials");

		InitialLdapContext ctx = null;
		Hashtable<String, String> contextConfig = null;

		// Set up LDAP config settings
		contextConfig = new Hashtable<String, String>();
		contextConfig.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
		contextConfig.put(Context.REFERRAL, "follow");
		contextConfig.put(Context.PROVIDER_URL, url);

		// For non-anonymous authentication security needs to be configured
		if (securityAuth != null && securityAuth.equals("none") == false) {
			contextConfig.put(Context.SECURITY_AUTHENTICATION, securityAuth);
			contextConfig.put(Context.SECURITY_PRINCIPAL, securityPrincipal);
			contextConfig.put(Context.SECURITY_CREDENTIALS, securityCredentials);
		}

		ctx = new InitialLdapContext(contextConfig, null);
		return ctx;
	}

	private Map<String, String> getSecurityInfo(IServiceCredentialsProvider pServiceCredentialsProvider,
			Map<String, Object> pParameters) throws ServiceException {

		Map<String, String> resultMap = new HashMap<String, String>();

		resultMap.put("auth", (String) pParameters.get("security-authentication"));
		if (resultMap.get("auth") != null) {
			resultMap.put("principal", (String) pParameters.get("security-principal"));
			resultMap.put("credentials", (String) pParameters.get("security-credentials"));
		}
		if (pServiceCredentialsProvider != null) {

			if (pServiceCredentialsProvider.getId() == "basic") {
				resultMap.put("auth", "simple");
				try {
					// use reflection to get username and password
					resultMap.put("principal",
							(String) pServiceCredentialsProvider.getClass().getMethod("getUsername", new Class[0])
									.invoke(pServiceCredentialsProvider, new Object[0]));

					resultMap.put("credentials",
							(String) pServiceCredentialsProvider.getClass().getMethod("getPassword", new Class[0])
									.invoke(pServiceCredentialsProvider, new Object[0]));
				} catch (Exception e) {
					throw new ServiceException(e);
				}
			}
		}
		if (resultMap.get("principal") == null)
			resultMap.put("principal", "");
		if (resultMap.get("credentials") == null)
			resultMap.put("credentials", "");
		return resultMap;
	}

	/**
	 * Creates an empty XML document.
	 */
	private Document createDocument() throws ServiceException {
		Document doc = null;
		try {
			DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
			DocumentBuilder db = dbf.newDocumentBuilder();
			doc = db.newDocument();
		} catch (Exception ex) {
			throw new ServiceException(ex);
		}
		return doc;
	}

	/**
	 * Serializes an XML document to a String.
	 */
	private String serializeDocument(Document pDocument) throws ServiceException {
		try {
			Transformer t = TransformerFactory.newInstance().newTransformer();
			ByteArrayOutputStream baos = new ByteArrayOutputStream();
			t.transform(new DOMSource(pDocument), new StreamResult(baos));
			return new String(baos.toByteArray(), "UTF-8");
		} catch (Exception ex) {
			throw new ServiceException(ex);
		}
	}
}
```

**Sample LDAP query Service Description**

This service description utilizes the previous sample LDAP transport to search an LDAP server for employee info. The results returned are based on a wildcard match of the employee's name or email address.

```
<?xml version="1.0" encoding="UTF-8"?>
<serviceDescription>
	<id>com.mycompany.services.SampleLDAPSearch</id>
	<defaultLocale>en-us</defaultLocale>
	<transportId>com.mycompany.services.SampleLDAPServiceTransport.id</transportId>
	<name>Sample LDAP Search Service</name>
	<description>Searches an LDAP server for employee information.</description>
	<credentials providerId="basic">
		<property name="realm" value="com.mycompany.services.SampleLDAPRealm"/>
	</credentials>
	<inbound>
		<parameters>
			<parameter>
				<id>searchName</id>
				<name>Search Name</name>
				<description>The employee name to search for.</description>
				<mandatory>false</mandatory>
				<type>STRING</type>
			</parameter>
			<parameter>
				<id>searchEmail</id>
				<name>Search Email</name>
				<description>The employee email to search for.</description>
				<mandatory>false</mandatory>
				<type>STRING</type>
			</parameter>			
		</parameters>
		<serviceMapping>
			<constants>
				<constant>
					<id>url</id>
					<value>ldap://ldap.mysite.com:389/</value>
				</constant>
				<constant>
					<id>basedn</id>
					<value>ou=employees,o=mysite.com</value>
				</constant>
				<constant>
					<id>filter</id>
					<value>(&amp;(objectClass=person)(cn=*{0}*)(email=*{1}*))</value>
				</constant>
				<constant>
					<id>result-attributes</id>
					<value>cn,telephone,email</value>
				</constant>				
			</constants>
			<mapping>
				<mapping target="transport:url" source="constant:url" />
				<mapping target="transport:basedn" source="constant:basedn" />
				<mapping target="transport:filter" source="constant:filter" />
				<mapping target="transport:filter-arg-0" source="parameter:searchName" />
				<mapping target="transport:filter-arg-1" source="parameter:searchEmail" />				
				<mapping target="transport:result-attributes" source="constant:result-attributes" />
			</mapping>
		</serviceMapping>
	</inbound>
	<outbound>
		<parameters>
			<parameter>
				<id>searchResults</id>
				<name>Search Results</name>
				<description>The list of search results</description>
				<type>LIST</type>
				<parameters>		
					<parameter>
						<id>name</id>
						<name>Employee Name</name>
						<description>The employee's name.</description>
						<type>STRING</type>
					</parameter>		
					<parameter>
						<id>email</id>
						<name>Employee Email</name>
						<description>The employee's email address.</description>
						<type>STRING</type>
					</parameter>			
					<parameter>
						<id>phone</id>
						<name>Employee Phone Number</name>
						<description>The employee's phone number.</description>
						<type>STRING</type>
					</parameter>
				</parameters>
			</parameter>
		</parameters>		
		<serviceMapping>
			<mapping>
				<mapping target="parameter:searchResults" source="transport:resultXML" sourceRef="searchresults/searchresult" sourceType="xml">			
					<mapping target="parameter:name" sourceRef="cn" sourceType="xml" />
					<mapping target="parameter:email" sourceRef="email" sourceType="xml" />
					<mapping target="parameter:phone" sourceRef="telephone" sourceType="xml" />
				</mapping>				
			</mapping>
		</serviceMapping>
	</outbound>
</serviceDescription>
```

**Parent topic: **[Service Oriented Architecture – Service Transport](ex_soa_service_transport.md)

