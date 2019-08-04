# Addresses

This specification defines the schema of the data and metadata for addresses.



### Reference and Associated material from discussion 2019-07-19

* PayPal API standards
    * [Address_portable.md](https://github.com/paypal/api-standards/blob/master/v1/schema/json/README_address.md) readme - describes a json object designed to work with html 5.1 autocomplete fields, Google libaddressinput validation data, and the AddressDoctor product from Informatica
    * [address_portable.json](https://github.com/paypal/api-standards/blob/master/v1/schema/json/draft-04/address_portable.json) schema.  Incudes a detailed address object for more fine-grained addresses
    * We also looked at PayPal's i18n reference application and the formats, field labels, and validations offered.
* Google Address implementations
    * libaddressinput [AddressValidationMetadata](https://github.com/google/libaddressinput/wiki/AddressValidationMetadata) - describes the address validation metadata Goolge publishes and includes layouts, required fields, postal code validation patterns, field names in English, ISO 3166-2 sub-region codes where appropriate, subregion names, and latin layouts for Asian regions
    * The Google libaddressinput data repository: https://chromium-i18n.appspot.com/ssl-address/data/
    * Google Places API [Place Details](https://developers.google.com/maps/documentation/javascript/places#place_details) and [supported types](https://developers.google.com/places/web-service/supported_types) for place descriptors
* HTML 5 autocomplete fields
    * Possible [values for the autocomplete attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete#Values). Search for _"street-address"_ 
    * Latest version of [W3C HTML 5.1 autofill field keywords](https://www.w3.org/TR/html51/sec-forms.html#autofill-field)
    * [Example, using Google Places API](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform) 
* iLib
    * Address Formatting and Parsing capabilities
    * https://github.com/iLib-js/iLib/blob/development/docs/tutorial/address.md
* UPU - Universal Postal Union
    * Example [Address layout page for Albania](http://www.upu.int/fileadmin/documentsFiles/activities/addressingUnit/albEn.pdf) - most all other regions can be found from the UPU "[Postal addressing systems in member countries](http://www.upu.int/en/activities/addressing/postal-addressing-systems-in-member-countries.html)" page
    * We looked at some [S42 address standard](http://www.upu.int/en/activities/addressing/s42-standard.html) syntax for a country and the level of detail supplied.
* Graham Rhind
    * We looked at the [Global Sourcebook for International Data Management](https://www.grcdi.nl/gsb/global%20sourcebook.html) and the various [address formats](https://www.grcdi.nl/gsb/world%20address%20formats.html) that it describes for every region
* Address microformat
    * http://microformats.org/wiki/adr
