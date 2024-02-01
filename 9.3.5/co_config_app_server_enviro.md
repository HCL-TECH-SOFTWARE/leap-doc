# Application server environment configuration {#concept_zdw_tzs_nv .concept}

The following general information describes the requirements for configuring your application server environment.

By default the settings available from WebSphere® Application Server are sufficient for general usage. Refer to the WebSphere Application Server documentation for general set-up. For basic architecture of Leap, see [Leap Basic Architecture](in_basic_architecture.md).

**Loading/performance:** When you set up your Application Server environment for HCL Leap, you should follow the performance tuning guidelines in the [WebSphere Application Server documentation](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/welc6toptuning.html). To achieve the best performance for the workload on your system, you might want to consider altering the following settings:

-   Use a web server and configure the [WebSphere Application Server plugins](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/tins_webplugins.html) to provide load balancing, fail-over, and the ability to deploy in a DMZ.
-   Update the Java heap size for your server. For further information, see [WebSphere Application Server documentation](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/tprf_tunejvm_v61.html?lang=en).
-   Increase the web container threads within WebSphere Application Server
-   Increase the JDBC connection pool to the Leap database.

For more information, see [WebSphere Application Server documentation](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/welc6toptuning.html?lang=en).

**Security:** When you consider security, standard web application security practices must be considered. Leap provides application-level security. However it relies on the server environment for extra security.

-   Ensure that your information is secure by using SSL whenever possible. Communication between the web browser and Leap when you use service descriptions and web services through the HTTP Service Transport, and the JDBC connection between Leap and the Leap database must be secured.
-   [Setting up an HTTP Strict Transport Security](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.ihs.doc/ihs/tihs_hsts.html) provides a method to ensure SSL communications from your application environment.
-   [Restrict cookies to HTTP requests](http://www.ibm.com/developerworks/websphere/techjournal/1210_lansche/1210_lansche.html#step29) whenever possible to prevent access from JavaScript, especially relating to sessions and authentication \(LTPA tokens\).
-   Restrict the ability to put Leap content in an iFrame if embedding is not part of your planned integration. Adding HTTP headers such as X-Frames-Options or Content-Security-Policy provides an extra layer of security.
-   Use IBM HTTP Server as a front end server to prevent direct access to the Application Server environment. Using a front end server allows for clustering through the WebSphere Application Server plug-in.
-   Keep your system updated with all security and maintenance patches to ensure a safe and stable environment. Watch for security bulletins in the HCL Support Portal, or by subscribing to My Notifications for updates.

For more WebSphere Application Server information, see [WebSphere Application Server documentation](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.nd.doc/ae/tfullp_sec.html), and [Advanced Security Hardening WebSphere Application Server](http://www.ibm.com/developerworks/websphere/techjournal/1210_lansche/1210_lansche.html).

**Parent topic: **[Configuring](co_config_toc.md)

