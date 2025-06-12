# Saving a PDF to a file location { #savingpdf .concept}

Determining where you want to save your filled PDF is useful considering how many processes "pick up" documents from watched folders. Designers have the option of saving the file to a specific location, as an attachment to the {{shortProductName}} submission record, or both.

File locations are whitelisted in the {% if isLeap %}Leap\_config.properties{% endif %}{% if isDominoLeap%}VoltConfig.nsf{% endif %}. Your file location can be any non-root directory. For example:

`storageBaseDirWhiteList = /Leap/PDFs`

Multiple locations can be whitelisted by separating them with a comma:

`storageBaseDirWhiteList = /Leap/locationA , /Leap/locationB`

The option for **PDF Save Location** appears in your PDF fill service configuration if a location has been whitelisted as described above. You need to map the location you want to save to the option in your service configuration. This can be done as an input item from the form or a constant \(shown in the following graphic\). The path must match exactly to what is whitelisted and the location must include the file name and path.

If the file already exists a duplicate will be made - for example, sample.pdf, sample\(1\).pdf, etc.

**Parent topic:** [Adding stages to an application](sub_adding_stages_toc.md)

