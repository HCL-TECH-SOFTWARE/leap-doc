# Upgrading { #upgradingleap_sec .concept}

When upgrading, it is important to take the necessary steps to ensure that you don't lose any data in the event of an unexpected error.

## Pre-upgrade steps
{% if isLeap %}
1. Take a full off-line back up of your Leap database. If anything goes wrong in the upgrade, having a full back-up gives you a restore point.
{% endif %}

{% if isDominoLeap %}
1. Copy the ../Domino/Data/volt directory and store it as a backup in a new location.  
{% endif %}

2. Perform the upgrade first in a pre-production environment using production data. The upgrade duration is proportional to the number of applications deployed to your {{shortProductName}} server. Testing in pre-production helps estimate the upgrade time and identify any applications that may fail during the process.

3. Take {{shortProductName}} offline to prevent public access during the upgrade. If a web server fronts {{shortProductName}}, either turn it off or redirect traffic to a maintenance page. If you disable the web server, update the serverURI in the {{shortProductName}} properties to ensure direct server access without issues.

4. Verify that {{shortProductName}} trace strings are NOT enabled. 


## Post-upgrade steps
{% if isLeap %}
1. Did you customize the location of the extensions directory?

    The default location is c:\HCL\leap\extensions or /opt/HCL/Leap/extensions. If you have customized this directory's location then you will need to re-apply the edit to the fsp.properties.
{% endif %}

2. After upgrading {{shortProductName}}, the first time you try to access {{shortProductName}} you will be redirected to the Setup screen.  The setup can only be run by a user in the {% if isLeap %}**AdministrativeUsers**{% endif %}{% if isDominoLeap %}**LeapAdmin**{% endif %} role for {{shortProductName}}. 

    There are two parts to the {{shortProductName}} upgrade; updating the {% if isLeap %}database schema and tables{% endif %}{% if isDominoLeap %}Leap builder and configuration databases{% endif %}, and upgrading each application to the latest schema.

    Existing applications will be upgraded the first time they are accessed after the upgrade is completed.

## Troubleshooting applications that fail to upgrade

It is our goal to ensure that no app fails the upgrade process. If any applications do fail the upgrade process, then there are a few things that you can do to investigate what happened BEFORE calling HCL Software Support.

1. **Check the SystemOut.log**. Each application failure will be logged in the ```SystemOut.log```. You will likely find a stack trace related to why the upgrade failed.

{% if isLeap %}
2. **Check the FREEDOM.APP_UPGRADE table in the database**. If you have a lot of apps on your server you may find that your logs roll-over and therefore will not contain all the upgrade failures when you go to review them. 

    You can perform a simple SQL statement to get the APPID, NAME andException that was thrown during the upgrade process:

    `db2 “SELECT * from FREEDOM.APP_UPGRADE” > app_upgrade_out.txt`

    If an application fails to upgrade then it will not be accessible, any user trying to access the application will see an error indicating that the application is unavailable and they should contact the system administrator. 
{% endif %}

3. **Try exporting the application from the pre-upgraded database and importing into the new {{shortProductName}} version**. If you can download the application from the backup that was taken before upgrading {{shortProductName}}, then you could try importing the application as a new application. 

    In order to export the application, you would have to have a {{shortProductName}} instance that was connected to the pre-upgraded database. If an app failed to upgrade and you want to keep the same UID (URL to access the form) then you will have to delete the app from the production server first, then you can import (deploy with data) to re-establish the application and all its data to the production server.

4. If you have any issues with upgraded applications after upgrading {{shortProductName}}, **open a support ticket**! Provide the SystemOut.log and the {{shortProductName}} application that won't upgrade.

The following topics describe how to upgrade {{shortProductName}}.

{% if isLeap %}
-   **[Upgrading Leap ](in_upgrading.md)**  
The following instructions describe how to upgrade Leap.
{% endif %}
{% if isDominoLeap %}
-   **[Upgrading from prior releases](dleap_upgrading_prior_releases.md)**  
{% endif %}

**Parent topic:** [Administering](administering_leap.md)

