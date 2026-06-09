# Domino Leap Cleanup process

Domino Leap Cleanup primarily purges orphaned Builder attachments, orphaned application attachments, and old Preview databases. Prior to release 1.0.3, this process was done by the Domino Leap Cleanup Agent.

## Orphaned Builder attachments

When a user creates a Domino Leap application, they can upload various files and store them as attachment documents in VoltBuilder.nsf. If the associated application is not saved, the uploaded files are no longer needed and should be deleted. This agent will purge these artifacts that have not been modified for the number of hours specified by the **purgeOrphanFilesHours** setting in VoltConfig.nsf

## Orphaned application attachments

Domino Leap applications can have attachment uploads. These attachments are stored in the application .nsf on individual document notes. If the associated record is not saved, the uploaded file is no longer needed and should be deleted. This agent will purge these artifacts that have not been modified for the number of hours specified by the **purgeOrphanFilesHours** setting in VoltConfig.nsf.

## Old Preview databases

When a Domino Leap Application is being designed, the user has the option of previewing their application prior to saving or deploying. A special preview-only nsf is generated for applications being previewed. This agent will delete all unused preview nsfs that have not been modified within the last seven days.

This clean-up process runs as part of the Domino Leap server process and no longer needs to be scheduled to run as an agent. The configuration and functionality are otherwise unchanged. To determine which hour of the day the clean-up process will run, set the **orphanFileCheckHour** parameter in VoltConfig.nsf. The default time is "0" for midnight.

**Parent topic:** [Administering](administering_leap.md)