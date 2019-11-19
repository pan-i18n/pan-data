# Addresses

This specification defines the schema of the data and metadata for addresses.

## Data Schema

Here is an example data representation of an address in the US:

```javascript
{
    "streetAddress": "900 Jefferson Ave.",
    "locality": "Redwood City",
    "region": "California",
    "regionCode": "US-CA",
    "postalCode": "94063",
    "country": "USA",
    "countryCode": "US"
}
```

Definition of the various fields:

* streetAddress - the street or road along with the house number or name
* building - the building name of this address
* postOffice - the name of the post office that should handle this address. Often
  used in larger cities such as Paris, France.
* locality - the city/town/village of the address
* dependentLocality - the small town/village name when the delivery point is
  outside of the boundary of the main Post Town that serves it
* region - the top-level administrative region of a country. These are often called
  states, provinces, prefectures, cantons, oblasts, etc.
* subregion - the second-level administrative region of a country. Many countries
  do not define these
* subsubregion - the third-level administrative region of a country. Most countries
  in the work do not define these
* regionCode - the ISO region code for the top-level administrative region
* postalCode - the government-assigned postal code of the address. In some countries,
  these are known as "post codes", "postal codes", or "zip codes".
* country - the name of the country in English
* countryCode - the ISO 3166 region code for the country of this address
* postOfficeBox - the P.O. Box of this address

All countries use a subset of the above fields. The metadata schema defines which fields
the country typically uses.

The full json schema can be found [here](../schemas/address-schema.json).

## Format Data Schema

Information used to format an address for various purposes.

The format information for addresses are given in an array of line templates that
may contain static text and one or more fields from the address schema. Each field
is specified as a name surrounded by curly braces. The static text in lines may
also contain formatting characters such as commas or dashes that typically appear
between fields in an address and do not form part of the fields themselves. Lines
are intended to be shown in the order given, and the tab order for input fields
should follow the order of the fields in those lines.

Example format lines for a US address:

```javascript
{
    "international": [
        "{streetAddress}",
        "{locality}, {region} {postalCode}",
        "{country}"
    ]
}
```

In this example, the second line contains a comma which separates the locality
name (a city) and the region name (a state) but which is not normally
specified in either the city or the state value.

### Domestic vs. International

Domestic addresses typically do not need the country, as it is assumed that the country is the
same as the current country. International addresses require the country. When the
country is specified, the countryCode should also be specified as well. A formats
file can specify different formats for domestic and international addresses.

### Locales and Scripts

A few countries in the world have more than one common language and/or script, and
the language/script can sometimes determine the address format. For example, in Hong
Kong, if the address is written in Chinese with the Chinese traditional script, then
the Chinese format is used. If the same address is written in English with the Latin
script, then the English/Western format is used. Address formats can therefore
depend on the locale, even within a single country.

A formats file can specify different formats for different locales typically used
within the country.

## Meta-data Schema

Meta-data about the fields is used to present input forms to the user and to parse
values from those forms into its constituents fields. Only one metadata file may
exist for each locale or partial locale.

Locale metadata files may inherit from another locale's metadata by using a "parent"
property which gives the locale spec of the parent locale. In this case, the
settings in the current file override any similar settings in the parent file. Any
settings not mentioned in the current file are inherited from the parent. All files
if they do not explicitly name a parent locale will inherit from the "root" locale.

Metadata can include:

* Metadata about each field type
    * The name of the field, in English. This can vary across regions. For example,
      in the US, a region is called a "State" and in Canada, a region is called a
      "Province". The translations for "State" and "Province" should appear in
      the address-translations file, not here.
    * A required property which tells whether or not the field is required in
      a valid address.
    * validation information. The validation object can contain information that
      implementations can use to construct and validate input fields.
        * pattern - a regular expression pattern that matches valid inputs
        * enum - a list of valid values for this field
        * aliases - a list of valid inputs, contractions, acronyms, and
          abbreviations that
          can represent valid values of this field. Free-form inputs should match
          one of the values in this list. The list maps valid inputs to normalized
          values, such as the ISO region code within a country.

The full json metadata schema can be found [here](../schemas/address-metadata-schema.json).

## Translation Schema

Translations for the various translatable strings related to addresses. The translations
file gives the translations for the following things:

* field types - translations of meta-information of the various types of fields
    * placeholder - the placeholder text to use in a free-form input text field
      for this type of address field, translated to the current language
    * tooltip - the tooltip text to use for an input form field for this type
      of address field, translated to the current language
    * aria-label - the text used to identify form controls for assistive
      technologies for accessibility compliance, translated to the current language
* field names
    * a mapping from the English name of a region, locality, etc. to the
      commonly used translation for that name translated to the current language.
      For example, the region name "State" used in the United States would be
      translated to "Staat" in Dutch. This would be used when the website and
      input form is in Dutch, but the address that the site is asking for is
      located in the United States.

### Reference and Associated material from discussion 2019-07-19

* PayPal API standards
    * [Address_portable.md](https://github.com/paypal/api-standards/blob/master/v1/schema/json/README_address.md)
      readme
        - describes a json object designed to work with html 5.1 autocomplete fields, Google libaddressinput
          validation data, and the AddressDoctor product from Informatica
    * [address_portable.json](https://github.com/paypal/api-standards/blob/master/v1/schema/json/draft-04/address_portable.json)
      schema. Incudes a detailed address object for more fine-grained addresses
  * We also looked at PayPal's i18n reference application and the formats, field labels, and validations offered.
* Google Address implementations
    * libaddressinput [AddressValidationMetadata](https://github.com/google/libaddressinput/wiki/AddressValidationMetadata)
        - describes the address validation metadata Goolge publishes and includes layouts, required fields,
          postal code validation patterns, field names in English, ISO 3166-2 sub-region codes where
          appropriate, subregion names, and latin layouts for Asian regions
    * The Google libaddressinput data repository: https://chromium-i18n.appspot.com/ssl-address/data/
    * Google Places API [Place Details](https://developers.google.com/maps/documentation/javascript/places#place_details)
       and [supported types](https://developers.google.com/places/web-service/supported_types) for place descriptors
* HTML 5 autocomplete fields
    * Possible [values for the autocomplete attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete#Values).
      Search for _"street-address"_
    * Latest version of [W3C HTML 5.1 autofill field keywords](https://www.w3.org/TR/html51/sec-forms.html#autofill-field)
    * [Example, using Google Places API](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform)
* iLib
    * Address Formatting and Parsing capabilities
    * https://github.com/iLib-js/iLib/blob/development/docs/tutorial/address.md
* UPU - Universal Postal Union
    * Example [Address layout page for Albania](http://www.upu.int/fileadmin/documentsFiles/activities/addressingUnit/albEn.pdf)
        - most all other regions can be found from the UPU "[Postal addressing systems in member countries](http://www.upu.int/en/activities/addressing/postal-addressing-systems-in-member-countries.html)" page
    * We looked at some [S42 address standard](http://www.upu.int/en/activities/addressing/s42-standard.html) syntax for a country and the level of detail supplied.
* Graham Rhind
    * We looked at the [Global Sourcebook for International Data Management](https://www.grcdi.nl/gsb/global%20sourcebook.html)
      and the various [address formats](https://www.grcdi.nl/gsb/world%20address%20formats.html) that
      it describes for every region
* Address microformat
    * http://microformats.org/wiki/adr
