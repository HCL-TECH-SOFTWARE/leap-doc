# Integrating with {{msEntraName}} (Azure AD)

This section describes how to integrated Leap with {{msEntraName}}, formerly known as Azure Active Directory.

If you are going to integrate Leap with {{msEntraName}}, it is important to do so before allowing users to access the system.

!!!warning
    It is not recommended to convert an existing Leap system, with deployed applications, to {{msEntraName}}. The users and groups from the previous configuration may not match the new configuration which will disrupt the integrity of the Leap applications and data collected.  If you find your self in this situation, reach out to us so that we may assist you.


-   **[Configuring {{msEntraName}} for Leap](azure_config.md)**  
Register Leap as an application in {{msEntraName}}.
-   **[Enabling user/group searching using {{msEntraName}}](azure_lookups.md)**  
Enable Leap to search for users and groups within {{msEntraName}}.

**Parent topic:** [Deploying](in_overview.md)