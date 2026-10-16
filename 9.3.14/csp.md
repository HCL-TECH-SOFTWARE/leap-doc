# Content Security Policy (CSP) { #csp .concept }

## Requirements

The minimum required CSP header for {{shortLeapProductName}} is:

{% if not isDWLeap %}
```
base-uri 'none'; form-action 'self'; frame-ancestors 'self'; default-src 'none'; connect-src 'self'; font-src 'self'; script-src 'self' 'unsafe-eval' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self'; frame-src 'self'; 
```
{% endif %}
{% if isDWLeap %}
```
base-uri 'none'; form-action 'self'; frame-ancestors 'self'; default-src 'none'; connect-src 'self' https://navbar.<your_domain> https://meetings.<your_domain> https://search-middleware.<your_domain>; font-src 'self'; script-src 'self' 'unsafe-eval' 'unsafe-inline' https://navbar.<your_domain>; style-src 'self' 'unsafe-inline'; img-src 'self' https://navbar.<your_domain> data:; frame-src 'self' https://meetings.<your_domain> https://search-middleware.<your_domain> https://auth.<your_domain>
```
{% endif %}

- Additional trusted domains for each resource type can be added as required.
- The `frame-ancestors` directive can be controlled separately by the `embedDomainWhitelist` configuration setting. See [Configuration properties > embedDomainWhitelist](co_configuration_properties.md#embedDomainWhitelist). If a general CSP header is also applied, the browser will merge `frame-ancestors` directives and enforce the least privileged setting.

**Security Note:** {{shortLeapProductName}} will not function correctly if `'unsafe-eval'` and `'unsafe-inline'` are omitted from the CSP header. To apply a targeted (and limited) "strict" CSP on published forms, see [Strict CSP](leap_strict_csp.md).

## Setting a CSP Header

A general purpose CSP header for {{shortLeapProductName}} must be configured at the web server or reverse proxy layer.

{% if isDWLeap %}

For {{shortLeapProductName}}, a general purpose CSP header can be configured with Helm values, using APISIX's `response-rewrite` plugin.

```yaml
extraObjects:
  - apiVersion: apisix.apache.org/v2
    kind: ApisixRoute
    metadata:
      name: leap
    spec:
      ingressClassName: apisix
      http:
        - name: main
          ...
          plugins:
            ...
            - name: response-rewrite
              enable: true
              config:
                headers:
                  set:
                    Content-Security-Policy: "<CSP header>"
```
{% endif %}

{% if isLeap %}
For an IBM WebSphere Application Server (WAS) installation, the CSP header can be set using the following configuration in IBM HTTP Server (IHS)
```
<Location /apps>
  Header always set Content-Security-Policy "<CSP header>"
</Location>
```

For a Helm/Kubernetes deployment, refer to your ingress controller's documentation on setting response headers. 
For example, if you are using Traefik as your ingress controller, you can set the CSP header using the Traefik `headers` middleware for your Ingress resource.  

Example:
```
extraObjects:
  - apiVersion: traefik.io/v1alpha1
    kind: Middleware
    metadata:
      name: leap-csp-headers
    spec:
      headers:
        customResponseHeaders:
          Content-Security-Policy: "<CSP header>"
  - apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: leap
      annotations:
        traefik.ingress.kubernetes.io/router.middlewares: "\{\{ .Release.Namespace \}\}-leap-csp-headers@kubernetescrd"
    spec:
      ingressClassName: traefik
      rules:
        - host: leap.example.com
          http:
            paths:
              - path: /apps
                pathType: Prefix
                backend:
                  service:
                    name: "\{\{ .Release.Namespace \}\}-leap"
                    port:
                      number: 9443
      ...
```

{% endif %}


{% if isDominoLeap %}
For a {{shortLeapProductName}} installation, the CSP header can be set by configuring the Domino web engine.

Search the HCL Domino server documentation for "Web Site rules and global Web settings > HTTP response header rules"

{% endif %}

**Parent topic:** [Administering](administering_leap.md)

