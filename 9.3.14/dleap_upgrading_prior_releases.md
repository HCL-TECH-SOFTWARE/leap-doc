# Upgrading from prior releases

All Domino Leap NSF files set the database property **Don't Maintain Unread Marks** as default, which should improve performance. NSF files created in prior versions of Domino Leap are not changed.

!!! note
    Administrators can choose to set the Don't Maintain Unread Marks property on pre-existing Domino Leap applications either by using the database infobox individually on each application, or can use the compact tool to update a set of applications at once.

Admins can use the indirect files option to disable the **Don't Maintain Unread Marks** property using compact. For more information, see [Using indirect files to run database maintenance tasks]({{dominoDocBaseUrl}}/admin/admn_using_indirect_files_to_run_database_maintenance_tasks_t.html).

1. Create a text file with the .ind file name extension. For example, voltapps.ind.

2. Add the list of volt apps/databases/directories to the text file. For example, in the voltapps.ind file, you would add the following:

- volt/3f3c6795-99ff-4f32-bf7e-f873fa580f30.nsf
- volt/a8e1a577-843c-4d3d-8a75-30bf80ed3589.nsf
- volt/7e35779d-865c-4d5d-adcd-e39b0915780a.nsf

3. With the Domino Leap server running, enter the following commands from the Domino console or using the Domino remote console:

    ```
    load compact -U voltunread.ind
    ```

    !!! note
        You must have the proper administrator rights to complete this step.

4. Check that the **Don't Maintain Unread Marks** property (on the **Advanced** tab of the Database infobox) is now set for all the applications you put in the .ind file.

**Parent topic:** [Administering](administering_leap.md)