
# Configure SSL behavior

The default behavior of Open Liberty is that it will not trust any default certificates, which are typically included in all mainstream browsers. By providing this config setting, the default certificates will be trusted enabling communication with third-party services.

```yaml 
configuration:
  leap:
    configOverrideFiles:
      . . .
      sslOverride: |
         <server description="leapServer">
           <ssl id="defaultSSLConfig" trustDefaultCerts="true" />
         </server>
```

**Parent topic:** [Open Liberty server customizations](helm_open_liberty_custom.md)