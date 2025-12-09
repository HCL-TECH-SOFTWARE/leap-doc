# Troubleshooting installation

If Domino Leap is not accessible, complete the following steps.

1. Check the logs for any helpful information. The logs can be found at:

- [domino_data_dir]/domino/workspace/.metadata/.log 
- [domino_data_dir]/IBM_TECHNICAL_SUPPORT/console.log 

2. Execute the following command in the Domino console and then check the logs:

```
tell http osgi start dleap
```

Or:

```
tell http osgi diag dleap
```

Verify that the user running Domino has ‘read’ and ‘execute’ permissions for all of the directories in the following paths:

- [Domino_PROGRAM]/osgi/rcp/ecplise/links/volt.link 
- [Domino_PROGRAM]/osgi/volt/eclipse/plugins/*.jar


**Parent topic:** [Installing Domino Leap](dleap_install_overview.md)