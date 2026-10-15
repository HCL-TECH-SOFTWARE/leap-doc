# Using the correct URLs for anonymous access { #usingthecorrecturlsforanonymousaccess .task }

To allow anonymous access in {{fullProductName}} applications, you must first configure the server. For more information about configuring the server for anonymous access, see [Setting up security for anonymous access](as_setting_up_security_for_anon_access.md).

The URL used for each form determines whether it allows for anonymous or secure access.

The Base URL for every form uses the following "launch" URL: 

**http://localhost/volt-apps/secure/1/app/f759fc03-301c-4d61-8aec-53fa2ebcedd8/launch/index.html?form=F_Form1**


The launcher checks the access conditions of the form and then opens the correct URL.    

If a form is configured for anonymous access ONLY, it uses the following URL:

**http://localhost/volt-apps/anon/1/app/f759fc03-301c-4d61-8aec-53fa2ebcedd8/launch/index.html?form=F_Form1**

!!! note
            With anonymous access, the system does not prompt you to log in.

If a form is configured for secure access ONLY, it uses the following URL:

**http://localhost/volt-apps/secure/1/app/f759fc03-301c-4d61-8aec-53fa2ebcedd8/launch/index.html?form=F_Form1**

!!! note
            With secure access, the system prompts you to log in.

If a form is configured for both anonymous and secure access, the launcher prompts you to choose either anonymous or authenticated access.

**Parent topic:** [Securing](se_security_toc.md)

