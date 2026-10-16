# Core Domino server configuration

HCL Domino Leap is an add-on to the core HCL Domino server. Domino Leap runs in the context of the Domino web server (HTTP process). Therefore, Domino Leap is affected by the underlying Domino server configuration. This topic covers some of the core configuration settings that may affect Domino Leap.

## Performance settings

**Web server threads**

By default, the HTTP process allocates a maximum of 40 threads to handle incoming requests. On a busy server, this can result in multiple requests waiting for an idle thread. Depending on server hardware capacity, you can often increase the maximum number of threads to 500 or more. For instructions on increasing the thread limit, see [Specifying the number of threads used by the Web server]({{dominoDocBaseUrl}}/admin/tune_specifyingthenumberofthreadsusedbythewebserver_t.html) in the Domino documentation.

**Web user cache**

The HTTP process caches information about each authenticated web user. For example, it caches the list of groups to which a user belongs. When a single user makes multiple sequential requests, the cache can reduce the work required to complete some of the requests. By default, the HTTP process caches information for 64 users. If your server is regularly used by more than 64 users, consider increasing the cache size. For instructions on increasing the number of cached users, see [Managing the memory cache on the Web server]({{dominoDocBaseUrl}}/admin/tune_managingthememorycacheonthewebserver_t.html) in the Domino documentation.

For other performance settings that may affect Domino Leap, see [Improving Web server performance]({{dominoDocBaseUrl}}/admin/tune_improvingwebserverperformance_c.html) in the Domino documentation.

## Security settings

**Enable HTTPS**

By default, the Domino web server accepts connections on the HTTP port (usually port 80). When a user authenticates over HTTP, a bad actor on the network could steal the user's credentials. Therefore, you should enable the HTTPS port to encrypt network connections. For instructions on enabling the HTTPS port, see [SSL security]({{dominoDocBaseUrl}}/admin/conf_sslsecurity_c.html) in the Domino documentation. After you have enabled HTTPS, be sure to update the serverURI setting in VoltConfig.nsf.

**Disable authentication on the HTTP port**

After you enable HTTPS, a user could still attempt to authenticate over HTTP. You can disable this by making a simple change to your web site document.

1. Open your web site document.

2. Select the Security tab and look for the TCP Authentication section.

3. Change the Redirect TCP to SSL setting to Yes and save your changes.

**Configure the Strict-Transport-Security header**

The Strict-Transport-Security response header (abbreviated as HSTS) lets a web site tell browsers that it should only be accessed using HTTPS. Although Domino automatically writes the HSTS header (when applicable), you may want to configure the contents of the header. For example, the **HTTP_HSTS_MAX_AGE** setting specifies the value of the HSTS max-age directive. For more information, see [How to configure Domino for HTTP Strict Transport Security](https://ds_infolib.hcltechsw.com/ldd/dominowiki.nsf/dx/HSTS).

**Enable account lockout**

If a "user" attempts to authenticate but specifies the wrong password many times in a row, your server could be under a brute force or dictionary attack. The Internet password lockout feature lets you set a threshold value for Internet password authentication failures. For instructions on enabling Internet password lockout, see [Securing Internet passwords]({{dominoDocBaseUrl}}/admin/conf_securinginternetpasswords_t.html) in the Domino documentation.

**Parent topic:** [Administering](administering_leap.md)