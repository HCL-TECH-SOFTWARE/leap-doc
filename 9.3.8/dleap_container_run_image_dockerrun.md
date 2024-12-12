# Running an image - docker run

There are many options for running Domino as a container. For Domino Leap, the recommended approach is to use the one-touch Domino setup with a JSON configuration file.

For more information, see the following topics in the Domino documentation:
- Domino in Docker
- Invoking one-touch Domino setup with parameters in a JSON file on Docker

## Prerequisites

- A general understanding of Docker, or Podman.
- An environment that is enabled with Docker, or Podman.
- A built Domino Leap image, loaded into Docker, or Podman, or deployed to a repository that it can be fetched from.

## Full sample

The following steps will run a Domino Leap container for the fictional “Renovations” company.

This setup will include four fictional person records:

- Admin/Renovations
- Ted Amado/Renovations
- Samantha Daryn/Renovations
- Betty Zechman/Renovations

Each person is designated as a Domino Leap author and has the ability to create, edit, deploy, and use Domino Leap applications. The Admin user is also designated as the server administrator and the Domino Leap administrator.

The password for each persona is "passw0rd". You can log in to Domino Leap using any of the common names listed above.

## Procedure

1. Copy the example JSON below to a renovations-setup.json file in your local environment.

    !!! note
        The JSON file must be saved in UTF-8 format without a byte order mark (BOM) at the beginning of the file.

2. Run the following Docker command to create a new container and configure the Domino server inside the container using one-touch setup leveraging a JSON file. The one-touch JSON file from the host file system is mounted into the container. For additional info, see Invoking one-touch Domino setup with parameters in a JSON file on Docker in the Domino documentation.

```
docker run -it -d -v <volume-name>:/local/notesdata -v 
<one-touch-json-file>:/tmp/auto-config.json --name <container-name> 
--env SetupAutoConfigure=1 --env 
SetupAutoConfigureParams=/tmp/auto-config.json -p 1352:1352 -p 80:80 
--stop-timeout=60 --cap-add=SYS_PTRACE <docker-image>
```

Where:

- ```<container-name>``` is the name you want to assign to the running container .

- ```<volume-name>``` is the name of the new volume created.

- ```<one-touch-json-file>``` is the full path of the JSON file in your local environment.

- ```<image>``` identifies the Domino Leap container image that has already been loaded into Docker, or Docker is configured to fetch the image from a repository.

3. For example, the following command starts a container named dleap-renovations, configured using /tmp/renovations-setup.json, and bound to the dleap-data volume:

```
docker run -it -d -v dleap-data:/local/notesdata -v 
/tmp/renovations-setup.json:/tmp/auto-config.json --name 
dleap-renovations --env SetupAutoConfigure=1 --env 
SetupAutoConfigureParams=/tmp/auto-config.json -p 1352:1352 -p 80:80 
--stop-timeout=60 --cap-add=SYS_PTRACE hclcom/domino:14.0
```

Result:

The Domino Leap server container is created. The underlying Domino server starts and is ready to use. Launch a browser and visit the Domino Leap Manager page:

http://dleap.renovations.com/volt-apps/secure/org/ide/manager.html

!!! note
    If dleap.renovations.com is not a resolvable hostname and you are only accessing the container locally for experimentation, you will need to map dleap.renovations.com to 127.0.0.1 in your local hosts file. Alternatively, you may be able to access Domino leap using “localhost” for experimentation; however this requires setting the value of the serverURI property in renovations-setup.json to "http://localhost/volt-apps".

## Example renovations-setup.json:

```
"http://localhost/volt-apps".
Example renovations-setup.json:

{
  "serverSetup": {
    "server": {
      "type": "first",
      "name": "Dleap",
      "title": "Domino Leap Renovations server",
      "domainName": "Renovations",
      "password": null,
      "additionalServerTasks": "http"
    },
    "network": {
      "hostName": "dleap.renovations.com"
    },
    "org": {
      "orgName": "Renovations",
      "certifierPassword": "passw0rd"
    },
    "admin": {
      "lastName": "Admin",
      "password": "passw0rd",
      "IDFilePath": "admin.id"
    },
    "notesINI": {
      "HTTPEnableMethods": "GET,POST,PUT,DELETE,HEAD"
    },
    "registerUsers": {
      "defaults": {
        "saveIDToPersonDocument": true,
        "mailTemplatePath": "mail12.ntf",
        "enableFullTextIndex": true,
        "certificateExpirationMonths": 120
      },
      "users": [
        {
          "firstName": "Ted",
          "lastName": "Amado",
          "IDFilePath": "tamado.id",
          "password": "passw0rd",
          "setInternetPassword": true,
          "mailFilePath": "mail/tamado.nsf"
        },
        {
          "firstName": "Samantha",
          "lastName": "Daryn",
          "IDFilePath": "sdaryn.id",
          "password": "passw0rd",
          "setInternetPassword": true,
          "mailFilePath": "mail/sdaryn.nsf"
        },
        {
          "firstName": "Betty",
          "lastName": "Zechman",
          "IDFilePath": "bzechman.id",
          "password": "passw0rd",
          "setInternetPassword": true,
          "mailFilePath": "mail/bzechman.nsf"
        }
      ]
    }
  },
  "appConfiguration": {
    "databases": [
      {
        "filePath": "names.nsf",
        "action": "update",
        "documents": [
          {
            "action": "update",
            "findDocument": {
              "Type": "Server",
              "ServerName": "CN=Dleap/O=Renovations"
            },
            "items": {
              "HTTP_EnableSessionAuth": "1"
            }
          }
        ]
      },
      {
        "filePath": "volt/VoltBuilder.ntf",
        "action": "update",
        "ACL": {
          "ACLEntries": [
            {
              "name": "[Admin]",
              "level": "manager",
              "type": "person",
              "canDeleteDocuments": true,
              "roles": [
                "VoltAppsManager",
                "LeapAdmin"
              ]
            },
            {
              "name": "[Ted Amado]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            },
            {
              "name": "[Samantha Daryn]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            },
            {
              "name": "[Betty Zechman]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            }
          ]
        }
      },
      {
        "filePath": "volt/VoltAppHistory.ntf",
        "action": "update",
        "ACL": {
          "ACLEntries": [
            {
              "name": "[Admin]",
              "level": "manager",
              "type": "person",
              "canDeleteDocuments": true
            },
            {
              "name": "[Ted Amado]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            },
            {
              "name": "[Samantha Daryn]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            },
            {
              "name": "[Betty Zechman]",
              "level": "editor",
              "type": "person",
              "canDeleteDocuments": true
            }
          ]
        }
      },
      {
        "filePath": "volt/VoltConfig.ntf",
        "action": "update",
        "documents": [
          {
            "action": "create",
            "items": {
              "Form": "Setting",
              "settingName": "serverURI",
              "settingValue": "http://dleap.renovations.com/volt-apps",
              "enabled": "1"
            }
          }
        ]
      }
    ]
  }
}
```

**Parent topic:** [Deploying Domino Leap in a container](dleap_deploy_to_container.md)