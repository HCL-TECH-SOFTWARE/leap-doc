# Globalization features {#experiencebuilderglobalization .concept}

The following information describes the languages formatting features supported by HCL Leap.

## Supported languages { .section}

Leap supports the following languages:

-   Arabic
-   Catalan
-   Chinese \(Simplified\)
-   Chinese \(Traditional\)
-   Croatian \(Croatia\)
-   Czech \(Czech Republic\)
-   Danish \(Denmark\)
-   Dutch
-   English
-   Finnish \(Finland\)
-   French
-   German
-   Greek
-   Hebrew
-   Hungarian \(Hungary\)
-   Italian
-   Japanese \(Japan\)
-   Kazakh
-   Korean \(South Korea\)
-   Norwegian Bokmål \(Norway\)
-   Polish
-   Portuguese \(Brazil\)
-   Portuguese \(Portugal\)
-   Romanian \(Romania\)
-   Russian \(Russian\)
-   Slovak
-   Slovenian \(Slovenia\)
-   Spanish
-   Swedish \(Sweden\)
-   Thai
-   Turkish \(Turkey\)

The default language for designing applications is based on your web browser locale, or WebSphere® Portal container. If you do not want to use your default language, you can change to a specific language, or select “User’s Language” so the application applies the user’s web browser language settings when the application is opened.

## Formatting { .section}

Form items, such as currency, date, and time, are based on the locale of the form. For example, if a currency item is set on a form with a locale of Germany, the currency is shown as Euros. It is important to note that no monetary conversion is done if the locale of the form changes. The format of the currency symbol on the form changes, but the amount entered is shown as entered. For example, if a user enters $100 into a currency field with a locale of United States, the currency is shown as $100 US on a form with a locale of Germany. You can edit the currency type, with the Currency field selected, in the Properties side panel.

Locale settings can also affect dates. Countries can have specific requirements for how dates are written. For example, one country might want a date written month/day/year: 06/29/2012. While another country has a standard of day/month/date/year: Friday June 29, 2012. How the date is shown is determined by the locale of the form. You can manually change the date format, with the date field selected, in the Properties side panel.

-   **[Setting a language](gl_setting_a_language.md)**  
The default language for an application is based on the web browser locale. You can change the language of your HCL Leap application in the **Settings** tab.

**Parent topic: **[Creating and managing applications](cr_creating_and_managing_toc.md)

