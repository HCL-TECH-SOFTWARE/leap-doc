# Uninstalling Domino Leap on Linux

To uninstall Domino Leap on a Domino server running on a Linux operating system, complete the following steps.

## Before you begin

Export or backup any Domino Leap data that you want to keep before completing this task.

## Procedure

1. Shutdown the Domino server on Linux.

2. Delete the entire volt folder from the following Domino directory path:

```
/opt/hcl/domino/notes/latest/linux/osgi/
```

3. Delete volt.link file from the following Domino program directory path:

```
/opt/hcl/domino/notes/latest/linux/osgi/rcp/eclipse/links/
```

4. Delete the entire volt folder from the following Domino data directory path:

```
/local/notesdata/
```

5. If you have modified the java.policy for previous versions of Domino Leap to include the following changes, remove the following entries and save the file:

```
// HCL Domino Volt - for Groovy templates
grant codeBase "file:/groovy/shell" {
permission java.security.AllPermission;
};
```

The location of the java.policy within the Domino program directory is the following:

```
/opt/hcl/domino/notes/latest/linux/jvm/lib/security/java.policy
```

**Parent topic:** [Deploying](dleap_deploying.md)