# Versioning {#widget_versioning .concept}

This topic describes the widget's `version`.

The widget `version` must follow "Semantic Versioning" \([semver.org](https://semver.org/)\) practices of `MAJOR.MINOR.PATCH`. The following behaviours are expected:

-   `PATCH` increment \(ex. 1.0.0 \> 1.0.1\)
    -   For backwards compatible bug fixes.
    -   **Authors**: any widgets already declared with the same minor version will automatically start using the newest patch version. Newly added widgets will use the newest patch version.
    -   **End-Users**: any widgets declared with the same minor version will automatically start using the newest patch version.
-   `MINOR` increment \(ex. 1.0.1 \> 1.1.0\)
    -   For new functionality that is backwards compatible.
    -   **Authors**: any widgets already declared with the same major version will automatically start using the newest minor version. Newly added widgets will use the new minor version. New *optional* widget properties might appear to the app author.
    -   **End-Users**: any widgets declared with the same major version will automatically start using the newest minor version. End-users might experience some noticeable improvements.
-   `MAJOR` increment \(ex. 1.1.0 \> 2.0.0\)
    -   For major changes that are not backwards compatible.
    -   **Authors**: any widgets already declared with a different major version will remain at that major version. The declaration of previous major versions of widgets must be retained by the customer or failures may occur. The customer will decide which major versions of the widget will display on the palette. See "Upgrading" below for more information.
    -   **End-Users**: any widgets already declared with a different major version will remain at that major version. The declaration of previous major versions of widgets must be retained by the customer or failures may occur. See "[Upgrading](widget_upgrade.md) for more information.

**Note:** This Custom Widget API will also follow "semver" practices.

**Parent topic: **[Custom Widget API](customwidgetapi_landing.md)

