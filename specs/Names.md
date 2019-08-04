# Names

This specification defines the schema of the data and metadata for names.

## Data Schema

Here is an example data representation of a person's name:

```javascript
{
    "given": "John",
    "middle": "James",
    "family": "Smith",
    "nickname": "Jonny",
    "honorific": "Dr.",
    "suffix": "Jr."
}
```

The full json schema can be found [here](../schemas/name-schema.json).

## Format Data Schema

Information used to format names for various politeness levels and purposes.

For some locales, you must be careful how you refer to your user. In the US, the
culture is pretty informal, so it is okay to refer to someone you just met by their
first name. In Japan and Germany, you only use the first name if you have been
invited to do so by that other person. For software, that is pretty much never the case
so it should always use the polite forms for referring to the user.

### Politeness Levels

Cultures may like use different parts of a person's name in various politeness/formality
situations. Currently supported politeness levels are:

* formal - used when referring to a person formally (eg. "Dr. Lee") or when referring
to a 3rd person other than the user (eg. "His Excellency Prime Minister Smalley").
* normal - used in many, if not most, situations when you refer to the user. (eg. "George Smalley")
* familiar - used when you would like to address the user in a more familiar way.  (eg. "George")

### Name Lengths

Additionally, each politeness level has various name lengths. When a user has
input all their name parts, it can be cumbersome in the UI to use all of
those name parts in many situations. The length automatically selects a subset
of name parts. Here is what the lengths in the normal politeness level might look
like for English:

* full - "Dr. Richard Wenbo Lee, PhD."
* long - "Dr. Richard Lee"
* medium - "Richard Lee"
* short - "Richard Lee"

And for the formal politeness level in English:

* long - "Dr. Richard Lee"
* short - "Dr. Lee"

And for the familiar politeness level in English:

* long - "Richard Lee"
* short - "Richard"

The full json formats schema can be found [here](../schemas/name-formats-schema.json).

## Meta-data Schema

Meta-data about the fields is used to present input forms to the user and to parse
names into its constituents fields. One metadata file may exist for each locale or
partial locale.

Locale metadata files may inherit from another locale's metadata by using a "parent"
property which gives the locale spec of the parent locale. In this case, the
settings in the current file override any similar settings in the parent file. Any
settings not mentioned in the current file are inherited from the parent. All files
if they do not explicitly name a parent locale will inherit from the "root" locale.

Metadata can include:

* Metadata about each field
    * Translated display name for labels
    * Placeholder text for input fields
    * Tooltip values when a user hovers their mouse over the input field
* Extra information
    * Auxillary words in family names, like "van der" or "de la", which are typically
      included in that family name.
    * List of possible honorific titles or names
    * List of possible prefixes
    * List of possible suffixes
    * Whether or not this locale sorts family names by their head word or their
      auxillary words

The full json metadata schema can be found [here](../schemas/name-metadata-schema.json).

### Reference and Associated material from discussion 2019-07-19

* Implementations
    * iLib - i18n library in JavaScript
        * Name Formatting and Parsing capabilities
        * https://github.com/iLib-js/iLib/blob/development/docs/tutorial/name.md
    * Iconic name-parser library written in PHP
        * https://github.com/theiconic/name-parser
    * Python nameparser
        * https://github.com/derek73/python-nameparser
    * Parse Full Name in JavaScript
        * https://www.npmjs.com/package/parse-full-name
* Wikipedia
    * http://en.wikipedia.org/wiki/List_of_family_name_affixes
    * https://en.wikipedia.org/wiki/Category:Human_names
    * https://en.wikipedia.org/wiki/List_of_common_Chinese_surnames
    * https://en.wikipedia.org/wiki/Chinese_surname
    * https://en.wikipedia.org/wiki/List_of_most_common_surnames_in_Asia#Japan
