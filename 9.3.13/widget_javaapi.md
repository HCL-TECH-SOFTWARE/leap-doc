# Usage of JavaScript API { #widget_javaapi .concept}

Custom widgets can use {{shortProductName}}'s JavaScript API to help achieve their objectives.

The API can be accessed via the global `NitroApplication` object or by the passed-in `context` object. For example, the following is a widget that renders itself appropriately based on the form's currently selected page:

```javascript
const myPageNavigator = {
    ...
    instantiate: function (context, domNode) {
        if (context.mode === 'run' || context.mode === 'preview') {
            const currentPage = context.page;
            context.form.getPageIds().forEach((pageId) => {
                const page = context.form.getPage(pageId);
                const btn = document.createElement('button');
                btn.innerHTML = makeHTMLSafe(page.getTitle());
                if (page === currentPage) {
                    btn.setAttribute('disabled', 'true');
                } else {
                    btn.addEventListener('click', () => {
                        context.form.selectPage(pageId);
                    });
                }
                domNode.appendChild(btn);                    
            });
        } else {
            ...
        }
        return { ... };
    }
}
```

**Parent topic:** [Custom Widget API](customwidgetapi_landing.md)

