# Deploying a Service Description 

This topic contains information about how to deploy an HCL Leap Service Description.

To deploy a Service Description, place the XML document in one of the following directories, or in a subdirectory of one of the following directories:

-   Windows™:

    any drive\\HCL\\Leap\\ServiceCatalog\\1\\

-   Linux™, or AIX®:

    /opt/HCL/Leap/ServiceCatalog/1/


Important notes on directories:

-   There must be an extensions directory in the same parent directory as the ServiceCatalog directory. Otherwise, the ServiceCatalog directory is not found. For example, /opt/HCL/Leap/extensions/.
-   If the extensions directory or ServiceCatalog/1 directory does not exist, then the Leap server must be restarted after the directories are created.
-   /opt/HCL/Leap/ is not case-sensitive.

When the Leap server starts, the ServiceCatalog directory and its subdirectories are scanned for new, deleted, and changed Service Descriptions. New and changed Service Descriptions are loaded and registered with the Leap server, and become available immediately. Service Descriptions that fail to load, or do not have an appropriate Service Transport registered, are not available.

Access to a service description may be given to a specific user, group, or special assignment \(i.e. Authenticated, Anonymous, etc\). The access control is made up of two parts: who may discover and work with the service while designing an application, and who may run the service. Users or Groups provided must be in the proper format - it is recommended to use the dialog \(by clicking the button with the down arrow\) when adding permissions. Adding or removing users does not require a server restart, but there will be a short delay before the changes take effect.

Deleting Service Descriptions and changing Service Descriptions must be done with care. Applications might depend on any or all of the parameters for the Service Description, as well as data returned within the Service Description. Therefore, modifying the structure or ID of parameters, or how data is mapped into the parameters, can potentially cause failures within deployed applications.

Deleted Service Descriptions are unregistered and immediately become unavailable to any applications, deployed or otherwise. It is critical that before deregistering a Service Description, a check is performed to ensure that there are no applications that are using the Service Description.

In general, adding new parameters or mappings and changing names and descriptions does not cause failures. However, removing existing parameters, changing parameter mapping, or modifying IDs for Service Description, Service Transport, or a parameter, are likely to cause failures. A list of potentially safe and unsafe operations are summarized in Table 2.

Table 1. Summary of potentially safe and unsafe changes

<table>
<tr>
<td><b>Potentially Safe Changes</b> </td><td> <b>Potentially Unsafe Changes</b></td>
</tr>
<tr>
<td><ul>
<li> Adding new parameters</li>
<li> Changing the name of a parameter</li>
<li> Changing the description of a parameter</li>
<li> Changing the name of the Service Description</li>
<li> Changing the description of the Service Description</li>
<li> Adding support for an additional language within the Service Description</li>
<li> Changing the Service Description default locale</li>
</ul>
<td><ul>
<li> Removing existing parameters</li>
<li> Changing the ID of an existing parameter</li>
<li> Changing the ID of the Service Description</li>
<li> Changing the Transport ID of the Service Description</li>
<li> Changing the mapping of existing parameters.</li>
</tr>
</table>


If significant changes must be made to a Service Description that is in use by deployed applications, a new Service Description must be created and the existing Service Description that remains intact. The new Service Description must be given a unique ID, and given a distinct name with a version number to indicate that this new Service Description is different from similarly named ones.

**Parent topic: **[Service Description](ref_service_service_description.md)

