<p align="center"><strong><a href="https://opensource.hcltechsw.com/leap-doc/9.3.5/index.html"> HCL Leap for on-premises product documentation</a></strong></p>
</p>


## Contributing

Bug reports on **product documentation** and pull requests are welcome on GitHub at https://github.com/HCL-TECH-SOFTWARE/leap-doc. 
This is the Leap documenation site and not a product support platform. All bug reports and pull requests must pertain to product documentation. 

### Updating the documentation and validating changes

- Clone this repo and create a working branch.
- Edit the markdown (.md) files in **9.3.x/** as needed.  (Ignore the .html files in docs/ directory)
- If you want to check the appearance of your changes in HTML, use MKDocs to build and serve up the html. See [Full Setup](#full-setup) below for more details.

### Submitting documentation changes

- Open a [Pull Request](https://github.com/HCL-TECH-SOFTWARE/leap-doc/pulls).
- Respond to review comments as needed.
- You will be notified when your changes have been merged. They will appear on the public site the next time the documentation is built.

## Full Setup

In general, you will need:

-   Python 3 installed
-   PIP package manager installed
-   You need a text editor (VSCode is recommended)
 
### Install MkDocs and plugins

Run the following commands to install MKDocs:

**Note**: Depending on your local Python setup, you might need to change `pip` to `pip3` for the commands below.

```
pip install mkdocs-material
```

MKDocs has a number of plugins that are used to provide additional functionality. Here is the starting set we use.

```
pip install mkdocs-awesome-pages-plugin
pip install mkdocs-git-revision-date-localized-plugin
pip install mkdocs-macros-plugin
pip install mike
```

### Preview Changes
To see changes in the browser, run `mkdocs serve -f mkdocs-93x.yml`
