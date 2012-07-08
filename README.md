Lexicographer
=============

A system for maintaining natural language dictionaries. 

This is currently in extremely early design stage work. The planned project consists of several core components:

1. A standard data format for storing & describing lexicographic information such as would be necessary to automatically generate a human-redable dictionary or to do automatic glossing or other markup of foriegn-language texts. This in turn consists of two parts:
    * A specification for a language-description language that sets out the relevant grammatical and semantic categories of a language that need to be represented in its dictionary.
	* A specification for the storage format for actual dictionary information.
2. A user interface, configurable by language description files, to allow entry, search, and editing of lexical information. This may have multiple implementations.
3. A templating system to allow auto-generation of human-readable dictionaries in HTML or PDF formats.