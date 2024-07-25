# SAML configuration {#helm_saml_config .concept}

The Leap Helm chart and container offer a basic SAML configuration through the Helm values. To enable SAML you must pass the IdP Metadata of the identity provider.

The idpMetadata accepts IdP Metadata in xml format. Please use the [multiline string feature of Helm](https://helm.sh/docs/chart_template_guide/yaml_techniques/#strings-in-yaml) to pass this value.

Example:

```yaml
security:
  leap:
    . . .
    saml:
      idpMetadata: |
        <EntityDescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="SAMLtestIdP" entityID="https://samltest.id/saml/idp">
            <IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol urn:oasis:names:tc:SAML:1.1:protocol urn:mace:shibboleth:1.0">
              ...
            </IDPSSODescriptor>
        </EntityDescriptor>
```

**Parent topic:** [Preparation](helm_preparation.md)

