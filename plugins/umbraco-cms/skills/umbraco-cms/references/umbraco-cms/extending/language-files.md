# Language Files & Localization | CMS

This article overviews how an Umbraco CMS website uses and manages localization with language files.

Language Files & Localization

Supported Languages

Last updated

Was this helpful?

This article overviews how an Umbraco CMS website uses and manages localization with language files.

Language Files & Localization

Language files are used to localise the Umbraco backoffice, so Users can use Umbraco in their native language. This is particularly important for content editors who do not speak English.

With language files, you can also:

Override existing (core) localizations.

Define localization for your own package.


Defines how to use the UI Umbraco Localization. This is the primary source of localization for the backoffice.

Defines how to use the .NET Core Umbraco Localization. This is only relevant for localization that happens server-side - for example, for sending emails.

You can use localization files for Document and Media Types as well. You can find more information about this in the [Document Type Localization](/umbraco-cms/fundamentals/data/defining-content/document-type-localization) article.

Supported Languages

Current with their ISO codes that are included in new Umbraco installations are:

`bs-BS`

- Bosnian (Bosnia and Herzegovina)`cs-CZ`

- Czech (Czech Republic)`cy-GB`

- Welsh (United Kingdom)`da-DK`

- Danish (Denmark)`de-DE`

- German (Germany)`en`

-**English (United Kingdom)**(fallback language)`en-US`

- English (United States)`es-ES`

- Spanish (Spain)`fr-FR`

- French (France)`he-IL`

- Hebrew (Israel)`hr-HR`

- Croatian (Croatia)`it-IT`

- Italian (Italy)`ja-JP`

- Japanese (Japan)`ko-KR`

- Korean (Korea)`nb-NO`

- Norwegian Bokmål (Norway)`nl-NL`

- Dutch (Netherlands)`pl-PL`

- Polish (Poland)`pt`

- Portuguese (Portugal)`pt-BR`

- Portuguese (Brazil)`ro-RO`

- Romanian (Romania)`ru-RU`

- Russian (Russia)`sv-SE`

- Swedish (Sweden)`tr-TR`

- Turkish (Turkey)`ua-UA`

- Ukrainian (Ukraine)`zh-CN`

- Chinese (China)`zh-TW`

- Chinese (Taiwan)

Last updated

Was this helpful?

Was this helpful?

## .NET Localization | CMS

NET Umbraco Core Localization files.

Use cases

Where to find the core localization files

```
Umbraco-CMS/src/Umbraco.Core/EmbeddedResources/Lang/
```

User localization files

```
/config/lang/{language}.user.xml
```

Using the localizations

Help keep the language files up to date

Last updated

Was this helpful?
