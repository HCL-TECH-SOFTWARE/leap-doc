# Creating and formatting the custom-values.yaml

## About this task

The Leap deployment requires a custom-values.yaml file that defines the settings for your deployment. When working with yaml files in Kubernetes it is important to understand and remember the following guidelines:

- The file has section names, some of which have nested section names. Values must be placed in the correct section using the correct indentation in order for them to be valid.
- Do not duplicate top-level section names. If you are configuring a setting that belongs in a certain section, check your file for the section name first, then add the value to the existing section. If no such section exists, you can create a new section with the required section name.
- Indentation is always done in increments of two spaces, never a tab key.
- Variable names always begin with a lower case letter, and words are typically “camelCase”.
- Comments can be used in the file, and should begin with a single hash followed by a space (# ). As a best practice each variable should be documented.
- The file consists of key pairs separated by a colon (:) never an equals sign. Values can contain an equals sign or a colon but they must be in double-quotes.

## Procedure

1. Create a new file ```custom-values.yaml``` using a text editor on the machine where you will run helm. 

    For example using vi: 
    ```vi custom-values.yaml```

2. Create a new section name by adding a single line to the beginning of the file:

    ```configuration:```

3. Save and close the file.

## What to do next

[Load images](helm_load_images.md)


**Parent topic:** [Prepare a custom configuration file](prepare_config_helm.md)