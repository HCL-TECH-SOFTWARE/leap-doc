
# Configure SSL behavior

The default behavior of Open Liberty is that it will not trust any default certificates, which are typically included in all mainstream browsers. By providing this config setting, the default certificates will be trusted enabling communication with third-party services.

``` 
configuration:
  leap:
    configOverrideFiles:
      sslOverride: |
         <ssl id="defaultSSLConfig" trustDefaultCerts="true" />
```

**Parent topic:** [Preparation](helm_preparation.md)