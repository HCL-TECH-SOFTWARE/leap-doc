# Service Oriented Architecture – Service Transport {#soaservicetransport .concept}

HCL Leap has a powerful, and extensible, Service Oriented Architecture \(SOA\) integration feature. The foundation of this feature is the Service Transport.

Each Service Transport represents a single communication process. Leap provides a REST transport. Additional transports can be developed and integrated into Leap to allow you to access other Services than ones expressed as REST. Each transport is written in Java™ as an OSGI bundle.

-   **[Creating your own custom Service Transport](ser_create_custom_service_transport.md)**  
By creating a custom Service Transport, you can allow HCL Leap applications to use services from any external system, or access any data source. Alternatively, the transport can implement a custom service itself without communicating with any external system or data source.

**Parent topic:**[Adding services](services_toc.md)

