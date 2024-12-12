# Troubleshooting and support { #troubleshootingandsupport .task}

Troubleshooting and support information for {{fullProductName}}.

If you are experiencing a problem with the {{shortProductName}}:

1.  Refer to the documentation for the task you are performing or the product component you are working with. These topics may contain troubleshooting information for common problems.

2.  Refer to the [Directory of worldwide contacts Web page](http://www.ibm.com/planetwide/) and contact HCL Software Support for your region.

3. Increase the log level to help identify the root cause.

{% if isLeap%}
For troubleshooting issues with HCL support, the following log level trace strings may be defined in WebSphere or a Kubernetes deployment:

```
com.ibm.form.*=FINE
com.ibm.form.nitro.*=finest
com.ibm.form.builder.*=finest
com.ibm.hrl.*level*=FINEST
com.ibm.freedom.*level*=FINEST
com.hcl.nitro.*=FINEST 
```
In a Kubernetes deployment, see [Changing the log level](helm_changing_log_level.md) for further details.

In a WebSphere deployment, see [Configuring Java logging with the administrative console](https://www.ibm.com/docs/en/was/9.0.5?topic=troubleshooting-configuring-java-logging-administrative-console) for further details.
{% endif %}

{% if isDominoLeap%}
For troubleshooting issues with HCL support, the following log level settings are suggested in [Domino_DATA]\domino\workspace\.config\rcpinstall.properties:

```
com.ibm.form.level=FINE
com.ibm.form.nitro.level=FINEST
com.ibm.form.builder.level=FINEST
com.ibm.hrl.level=FINEST
com.ibm.freedom.level=FINEST
com.hcl.nitro.level=FINEST 
dleap.level=FINEST
```

HCL Domino Leap operates as an OSGI Plug-In on the Domino Server. Log files for exceptions and logged events can be found on the Domino server in [Domino_DATA]\domino\workspace\logs.
{% endif %}

Setting a log level to FINE, FINER or FINEST may result in very verbose logging. On a busy server, this could mean hundreds of log messages per minute and it could have a significant impact on {{shortProductName}} performance. After you have gathered logs to troubleshoot a specific problem, we recommend you reduce the logging level to INFO or completely remove them.

**Parent topic:** [Troubleshooting](tr_troubleshooting_toc.md)

