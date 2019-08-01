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

## Meta-data Schema

Meta-data about the fields is used to present input forms to the user.

* Field names
* Placeholder text
* Default values
* Tooltip text
* Translations of field names

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
