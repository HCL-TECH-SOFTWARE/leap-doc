# Installing or upgrading Domino Leap

To install Domino Leap or to upgrade an existing Domino Leap installation, complete the following tasks:

!!! note
    If you are performing an upgrade, it is recommended to back up your files in [Domino_PROGRAM]/osgi/volt and [Domino_DATA]/volt. You do not need to remove older files before running the installation script.


## Extract installation files

Extract the installation package (.zip file) to any temporary directory on the server.

This installation package will contain the following (minimum) sub-folders:

- **bundles**: OSGI content to be deployed to the server

- **linux**: Linux operating-system specific content

- **templates**: Domino application templates used by Domino Leap

- **windows**: Windows operating-system specific content

## Run the installation script

!!! note
    Important! You must stop the Domino server before running the install script.

1. Open a command line console to the server.
  - For Windows open using an account with elevated administrative privileges such as the Administrator account.
  - For Linux open SSH console to the server. For Linux you will either need to be using the root account or an account with sudo privileges.

2. Navigate to the appropriate subfolder (windows or linux) and run the install script.
  - For Windows this is ```install.bat```.
  - For Linux you may need to add executable permissions to the script using the command: ```sudo chmod +x install```.

3. Answer the questions and follow the instructions from the script.

!!! note
    The Linux install script prompts you for the Domino user and group names. It's important that you choose a name without quotes. If a name defaults to a quoted string (e.g. "notes"), be sure to input a string without quotes. For example, this is incorrect:

```
**********************************
 HCL Domino Leap Environment
**********************************
 HCL Domino User:       "notes"
 HCL Domino Group:      "notes"
 Program Directory:     /opt/hcl/domino
 Data Directory:        /local/notesdata

 Proceed with installation? 
```

This is correct:

```
**********************************
 HCL Domino Leap Environment
**********************************
 HCL Domino User:       notes
 HCL Domino Group:      notes
 Program Directory:     /opt/hcl/domino
 Data Directory:        /local/notesdata

 Proceed with installation?
```

 **Parent topic:** [Installing Domino Leap](dleap_install_overview.md)