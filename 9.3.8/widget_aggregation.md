# Aggregation Widgets { #widget_aggregation .concept}

A custom widget with a datatype of `'aggregation'` is a special type of data widget that can achieve the use-case of a "repeating section". The section is a sub-form which the author can design as they wish, with required fields and others. The end-user can then create and fill multiple instances of that section, shown sequentially on the page.  For example, the widget could be used by the app author to ask for a list of vehicles owned by the end-user, with maker, model, and year for each vehicle. 


The data type of the instantiated custom widget will be a "business object list" (BOL). It is expected that a custom repeating section widget will utilize the existing API for BOLs. See [Business Object List (BOL) for lists of Business Objects](ref_jsapi_ref_data_objects.md#business-object-list-for-lists-of-business-objects). It is the responsibility of the custom widget to provide the UI for the end-user to trigger the addition (or deletion) of items in the BOL. In turn, {{shortProductName}} will create an instance of the UI (the sub-form) and pass that to the custom widget to place into its DOM. Hence, it is the manipulation of *data* that drives the UI.

The instantiated custom widget must include the following functions:

- `placeDesignForm(formNode)`: When the {{shortProductName}} app author places a repeating section widget on the canvas, {{shortProductName}} will create a sub-form (ie. `formNode`) for the app author to add fields to. {{shortProductName}} will call this function for the sub-form to be placed into the custom widget's DOM.  

- `addEntry(entryNode, entryId)`: When a new item is added to the custom widget's BOL, {{shortProductName}} will instantiate the corresponding sub-form (ie. `entryNode`) and pass it to this function to be placed into the custom widget's DOM. `entryId` is a transient UUID that can be used by the custom widget to keep track of entries, if needed, for the current user session.

- `removeEntry(entryNode, entryId)`: When an item is removed from the custom widget's BOL, {{shortProductName}} will call this function to ensure the corresponding sub-form (ie. `entryNode`) is removed from the custom widget's DOM.  

**Important**: `formNode` and `entryNode` (and their ancestors), should not be manipulated or inspected in any way; treat each as a black-box.

## Example
This specialized widget is best described with an example:

```javascript
acme.myRepeatingSection = {
  id: "acme.RepeatingSection",
  version: "1.0.0",
  apiVersion: "1.0.0",
  label: {
    "default": "ACME Repeating Section",
  },
  description: {
    "default": "ACME Repeating Section",
  },
  datatype: {
    type: "aggregation"
  },
  category: {
    id: "acme.sampleWidgets",
    label: {
      "default": "ACME Samples",
    }
  },
  iconClassName: "acmeRepeatingSectionIcon",
  builtInProperties: [{ id: "title" }],
  properties: [
    { id: "explanationText", propType: "string", label: { "default": "Explanation Text" }, defaultValue: { "default": "Some default explanation text" } },
    { id: "minEntries", propType: "number", label: { "default": "Min Entries" }, defaultValue: 0 },
    { id: "maxEntries", propType: "number", label: { "default": "Max Entries" }, defaultValue: 10 },
  ],

  // initialize widget in the DOM, with initial properties and event callbacks
  instantiate: function (context, domNode, initialProps, eventManager) {

    const widgetInstance = {
      _disabled: false,
      _mode: null, // 'design', 'preview', or 'run'
      _rootNode: null,
      _titleNode: null,
      _entriesNode: null,
      _addBtn: null,
      _eventManager: null,
      _formDesignNode: null,
      _minEntries: null,
      _maxEntries: null,

      // internal custom mechanics for changing widget props
      _setProp: function ({ propName, propValue }) {
        switch (propName) {
          case "title":
            this._titleNode.innerHTML = acme.makeHTMLSafe(propValue);
            break;
          case "minEntries":
            this._minEntries = propValue;
            break;
          case "maxEntries":
            this._maxEntries = propValue;
            break;
          default:
            // ignore
            break;
        }
        this._updateUI();
      },

      // internal method for creating and initializing the widget
      _init: function (context, domNode, initialProps, eventManager) {
        this._mode = context.mode;
        this._businessObjectList = context.BOA;
        this._eventManager = eventManager;
        const widgetHTML = `
            <div class="acme-rs">
                <div class="acme-rs-title"></div>
                <div class="acme-rs-form-design"><!-- sub-form design will go here --></div>
                <div class="acme-rs-entries"><!-- entries will go here --></div>
                <div class="acme-rs-prompt"></div> 
                <div><button class="acme-rs-add-btn">Add Entry</button></div>
            </div>
        `;
        domNode.innerHTML = widgetHTML;
        this._rootNode = domNode.firstChild;
        this._titleNode = domNode.querySelector(':scope .acme-rs-title');
        this._formDesignNode = domNode.querySelector(':scope .acme-rs-form-design');
        this._entriesNode = domNode.querySelector(':scope .acme-rs-entries');

        this._formDesignNode.style.display = this._mode === 'design' ? '' : 'none';
        this._entriesNode.style.display = this._mode === 'design' ? 'none' : '';

        this._promptNode = domNode.querySelector(':scope .acme-rs-prompt')

        this._addBtn = domNode.querySelector(':scope button');
        this._addBtn.style.display = this._mode === 'design' ? 'none' : '';
        this._addBtn.addEventListener('click', () => {
          // use documented JavaScript API to add a new data entry
          const bo = this._businessObjectList.createNew();
          this._businessObjectList.add(bo);
        });

        Object.keys(initialProps).forEach((propName) => {
          this._setProp({ propName: propName, propValue: initialProps[propName]
          });
        });

      },

      _updateUI: function () {
        if (this._mode === 'design') {
          this._promptNode.innerHTML = 'Drag and drop some widgets above';
        } else {
          this._addBtn.disabled = this._disabled || this._businessObjectList.getLength() >= this._maxEntries;
          this._promptNode.innerHTML = 'No entries';
          this._promptNode.style.display = this._businessObjectList.getLength() > 0 ? 'none' : '';
        }
        this._entriesNode.querySelectorAll('.acme-rs-delete-btn').forEach((btn) => {
          btn.disabled = this._disabled;
        });
      },

      placeDesignForm: function (formNode) {
        return this._formDesignNode.appendChild(formNode);
      },

      addEntry: function (entryNode, entryId) {
        const entryContainer = document.createElement('div');
        entryContainer.className = 'acme-rs-entry';
        entryContainer.id = `${entryId}_container`;

        const deleteBtn = document.createElement('button');
        deleteBtn.className = 'acme-rs-delete-btn';
        deleteBtn.innerHTML = 'Delete';
        deleteBtn.setAttribute('data-entry-id', entryId);
        entryContainer.appendChild(deleteBtn);
        deleteBtn.addEventListener('click', () => {
          // use documented JavaScript API to remove data entry
          const bo = this._businessObjectList.getById(entryId);
          this._businessObjectList.remove(bo);
        });

        entryContainer.appendChild(entryNode);
        this._entriesNode.appendChild(entryContainer);

        this._updateUI();
      },

      removeEntry: function (entryNode, entryId) {
        const entryContainer = document.getElementById(`${entryId}_container`);
        entryContainer.removeChild(entryNode);
        entryContainer.remove();

        this._updateUI();
      },

      getValue: function () {
        // must be present, but is not needed for 'aggregation' widgets
      },

      setValue: function (val) {
        // must be present, but is not needed for 'aggregation' widgets
      },

      setDisabled: function (disabled) {
        this._disabled = disabled;
        this._updateUI();
      },

      // called when properties change in the authoring environment, or via JavaScript API
      setProperty: function (propName, propValue) {
        this._setProp({ propName, propValue });
      }
    };
    widgetInstance._init(context, domNode, initialProps, eventManager);
    return widgetInstance;
  }
}

```


**Parent topic:** [Custom Widget API](customwidgetapi_landing.md)


