# JavaScript Security {#javascriptsecurity .reference}

The dojox.secure library is used to restrict the JavaScript™-provided clients to a safe sandbox so they cannot do anything malicious. However, this imposes a number of limitations.

The JavaScript in the sandbox generally follows rules to limit dangerous operations:

-   Use of eval, with, ==, !=, and the subscript operator \[\] are not allowed.
    -   Instead of == use ===
    -   Instead of != use !==
    -   Instead of the \[ \] operator, use the forEach\(\), get\(index\), and set\(\) functions provided.
-   Usage of the this keyword is not allowed:
    -   For item level events, the keyword item is used in place of the this keyword.
    -   For page level events, the keyword page is used in place of the this keyword.
    -   For form level events, the keyword form is used in place of the this keyword.
-   Limited access to global variables. Details are provided in the following section.
-   These properties might not be used: apply, arguments, call, callee, caller, constructor, eval, prototype this, unwatch, valueOf, watch, and any property beginning or ending with \_\_.

## Security { .section}

The following global variables are accessible:

|Variable|Description|
|--------|-----------|
|element|This the root element of the sandbox. Sandboxed elements do not have access to relational properties such as parentNode, firstSibling, nextSibling, etc. You can still use DOM methods and string properties like innerHTML. The style object can also be used, accessed, and modified.|
|document|This is a sandboxed document object that provides node creation and basic element searching facilities. The sandboxed document provides the following methods: getElementById, createElement, createTextNode, and write.|

The following standard JavaScript/DOM functions/constructors, and their child functions when applicable, might be called. They can be used only in call position. They cannot be accessed in any other way. They generally behave as the standard JavaScript function, unless otherwise noted:

-   isNaN
-   isFinite
-   parseInt
-   parseFloat
-   escape
-   unescape
-   encodeURI
-   encodeURIComponent
-   decodeURI
-   decodeURIComponent
-   alert
-   confirm
-   prompt
-   Date
-   RegExp
-   Error
-   Number
-   Math
-   setTimeout - This only accepts a function, not a string.
-   setInterval - This only accepts a function, not a string.
-   clearTimeout
-   clearInterval

The following special functions are available to compensate for the JavaScript syntax limitations imposed by the sandbox:

|Function|Description|
|--------|-----------|
|get\(obj,prop\)|This is a special function to handle accessing properties in lieu of the \[\] operator. Calling get\(obj,prop\) is equivalent to obj\[prop\].|
|set\(obj,prop,value\)|This is a special function to handle modifying properties in lieu of the \[\] operator. Calling set\(obj,prop,value\) is equivalent to obj\[prop\]=value.|
|forEach\(obj,func\)|This is a special function to iterate through all the properties in an object, or items in an array. For each item, the func function is called with the item as the first argument, the index as the second object, and the obj as the third object.|

The following functions for DOM manipulation and extra language features are provided by the Dojo library. This represents a safe subset of Dojo. All Dojo library functions are provided as top-level functions. Namespacing is unnecessary because scripts do have access to modify the global object and can't define global variables. Thus, you can call Dojo functions directly, for example, you can call mixin\(obj,mixinObj\). You might also use the traditional syntax \(dojox.mixin\(...\)\). Available functions include:

-   mixin
-   require
-   isString
-   isArray
-   isFunction
-   isObject
-   isArrayLike
-   isAlien
-   hitch
-   delegate
-   partial
-   trim
-   connect
-   disconnect
-   subscribe
-   unsubscribe
-   Deferred
-   toJson
-   fromJson
-   style
-   attr
-   query - This only searches within the sandbox.
-   byId
-   body - This returns the root element of the sandbox.

## Disabling JavaScript Security { .section}

Under some circumstances, the limitations imposed by the dojox.secure library might be too restrictive. Therefore, the dojox.secure library can be disabled server-wide by editing a Java™ properties file called Leap\_config.properties in the FSP extensions directory \(C:\\HCL\\Leap\\extensions on Windows™, /opt/HCL/Leap/extensions on Linux™\). Set the value of the ibm.nitro.ApplicationCompilerService.secureJS key to false. Once the properties file is changed, the HCL Leap server should be restarted to ensure that the configuration takes effect. For more information, see [Configuring the properties file](co_configuring_the_properties_file.md).

Changing this configuration setting should only be done if all the Leaps on the server are known trusted users. Disabling JavaScript Security on a deployment of the Leap that allows anonymous users to create applications could pose a serious security risk.

It should be noted that this configuration only applies to applications that are deployed after making this configuration change. Applications that are deployed before this configuration change must be redeployed for the configuration to take effect.

**Parent topic: **[Reference Objects and Functions](ref_jsapi_objects_and_functions.md)

