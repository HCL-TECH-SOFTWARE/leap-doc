# Connecting to an SMTP Server

To connect Leap with an SMTP server you must use the [configOverrideFiles](helm_open_liberty_custom.md) parameter. 

Below is an example snippet of configuring Leap to use a mail server. The smtphost will need to be replaced with the proper hostname of the mail server. If authentication is required to communicate with the mail server then replace smtpUser and smtpPassword with the correct values, otherwise remove those likes from the snippet.

``` {#codeblock_xhw_l5s_gxb}
configuration: 
  leap: 
    configOverrideFiles: 
      mailOverride: | 
        <server description="leapServer"> 
            <mailSession  
                id="leapMail"
                host="smtphost.com"  
                from="no-reply@smtphost.com"  
                jndiName="mail/BuilderMailSession"  
                description="Leap MailSession"  
                mailSessionID="leapMail" 
                user="smtpUser" 
                password="smtpPassword"> 
                <property name="mail.smtp.auth" value="false" /> 
                <property name="mail.smtp.port" value="25" /> 
            </mailSession> 
        </server>
```

**Parent topic:** [Preparation](helm_preparation.md)