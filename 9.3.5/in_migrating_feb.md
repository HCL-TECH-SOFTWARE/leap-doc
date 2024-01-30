# Migrating from IBM Forms Experience Builder {#migratingformsexperiencebuilder .concept}

The following instructions describe how to upgrade from IBM Forms Experience Builder to HCL Leap.

The process of upgrading from IBM Forms Experience Builder to HCL Leap is very similar to the instructions given in [Upgrading Leap on a traditional platform](in_upgrading.md). However, the default web module context roots have changed from `/forms` and `/forms-basic` to `/apps` and `/apps-basic` respectively. When upgrading to Leap you will want to ensure that you retain the same URLs used with IBM Forms Experience Builder.

When upgrading the EAR in the WebSphere Application Server Administrative console, choose the **Detailed** option for “How do you want to install the application?”. When you reach the **Map context roots for Web modules** step, ensure the **Context Root** values are the same as what you had previously.

**Parent topic:**[Deploying Leap](in_overview.md)

