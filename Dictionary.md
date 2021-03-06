Dictionaries
=============

Dictionaries are objects databases containing the following information:

1. Note Entries
2. Lexical Entries

All entries are described as JSON objects, but they may be mapped to equivalent YAML or XML structures or to a normalized relational model. In JSON form, a dictionary is an object with the fields "notes" and "lexemes".

# Note Entries
The "notes" field contains an object whose keys are the names of entries and whose values are NOTE objects. These are mainly intended for describing things like important cultural points or common metaphors in the language.

A NOTE object has fields whose keys are the names of languages and whose values are strings of free-form text not intended to be machine-interpretable.

strings containing free-form text. 

# Lexical Entries
The "lexemes" field contains a set, implemented as an arbitrarily ordered list, of LEXEME objects.

LEXEME objects contain the following fields:
* "class"
* "values"
* "forms"
* "etymology"
* "notes"
* "senses"

## class
The "class" field contains the name of the lexical class of the given item, referring to the classes defined in the language configuration.

## values
The "values" field contains an object whose keys are feature names as defined for the given class in the language configuration, and whose values are taken from the enumerations of possible values for those features.

## forms
The "forms" field contains an object whose keys are the names of the forms defined for the given class in the language configuration and whose values are either WORD objects or null. The field for any form for which a rule is defined by the language configuration may be omitted, in which case the form is assumed to be regular and may be autogenerated. If a field is present for a form that has a corresponding rule, it is assumed to be irregular. Fields must be present for any form that lacks a rule. A field with a null value indicates a missing form in a defective paradigm.

A WORD object has fields whose keys are the names of representations and whose values are strings containing the corresponding representations of a word. 

## etymology
The "etymology" field may be specified for a LEXEME or for individual word senses. If specified at the LEXEME level, an "etymology" field may not be present on contained definitions. The "etymology" field contains an object with the following fields:
* "derivation"
* "sources"

### derivation
The "derivation" field contains a string describing the type of derivation of the word (e.g., descent from a parent language, borrowing, calquing, compounding, etc.)

### sources
The "sources" field contains a list of SOURCE objects describing the source material for the current lexeme 1 step back; in most cases, this will be a list of length 1, but may be longer for cases such as compounding.

A SOURCE object contains the following fields:
* "language"
* "word"

#### language
The "language" field is the name of the source language as a string.

#### word
The "word" field contains a WORD object based on the configuration for the source language.

## notes
The "notes" field in a LEXEME object contains a NOTE object.

## senses
The "senses" field contains a list of SENSE objects.
A SENSE object contains the following fields:
* "notes"
* "etymology"
* "definitions"
The "etymology" and "notes" fields are as defined above for LEXEMEs.

### definitions
The "definitions" field contains a list of DEFINITION objects.
A DEFINITION object contains the following fields:
* "language"
* "correspondence"
* "text"
* "examples"

#### language
The "language" field contains the name of the target language for this definition as a string.

#### correspondence
The "correspondence" field contains a boolean value indicating that this is a single-lexeme definition that may be used for generating glosses or reverse target-to-source dictionaries if set to true.

#### text
The "text" field is a string of free-form text describing the definition of the lexeme in the target language.

#### examples
The "examples" field is a list of EXAMPLE objects.
An EXAMPLE object contains the following fields:
* "uri" or "text"
* "translation"
* "tags"
* "media"

#####uri or text
The "uri" field, if present, contains a link to an example usage of the lexeme in some corpus. The "text" field, if present, contains a free-form string containing an example of the lexeme's usage.

##### translation
The "translation" field contains the translation of the example text into the target language. This field will be absent for native-language definitions.

##### tags
The "tags" field contains a set implemented as an arbitrarily ordered list of the names of dictionary notes as strings.

##### media
The "media" field contains a list of MEDIA objects.
A MEDIA object contains the following fields:
* "mime"
* "uri"

###### mime
The "mime" field is the mime-type of the media resource as a string.

###### uri
The "uri" field is a URI for the media resource as a string; this may be a data URI.