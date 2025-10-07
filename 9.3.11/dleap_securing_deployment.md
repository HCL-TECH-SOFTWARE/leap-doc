# Securing your Domino Leap deployment

The data for each Domino Leap application is stored in a separate Domino database. The ACLs of the database, the permissions, and the access to documents within it are matched as closely as possible to the Domino Leap permissions model - which is enforced by Domino Leap code. One difference is that Domino Leap offers a further refinement and enforcement beyond simply "Author" in a Domino Database ACL. With enough privilege and access through a non-Domino Leap channel, users can create documents in the Domino database that they wouldn't be able to create through Domino Leap UIs or REST endpoints. If this is a concern, below are some of the options that can be leveraged:

- **NRPC Access** - The Domino Leap server can be configured to disallow communication through non-Domino Leap channels. For example, the Domino administrator may wish to limit communication via NRPC port on the Domino Leap server.

- **Hide Form** - Another option is to hide **Forms** from the **Create** menu in a Domino Database by unchecking the box to "Appear in Create Menu".

- **Separate Database** - Another option is to advise application authors to use a separate Domino Leap application if the creation of documents related to a specific form needs to be more tightly controlled.

- **Extending via Domino Application Modifications** - Domino applications can have various form or database events added to monitor and control any unintended activity. For example, an agent that alerts when a form is created by someone without the right role. This option is similar to how protections are enforced in a traditional Domino application.

**Parent topic:** [Administering](administering_leap.md)