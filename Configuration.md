Language Configurations
=============

Language configurations are defined as JSON structures. They may be mapped to YAML or XML equivalents.

The top-level of a language configuration is an object containing the following fields:
* "enumerations"
* "representations"
* "classes"

#enumerations
The "enumerations" field contains an object whose keys are the names of properties or collections of values that see heavy use in the language (e.g., grammatical gender, number, person, or other agreement triggers). Values are lists of strings whose values must be locally unique.

#representations
The "representations" field contains an object whose keys are the names of recording modes for the language and which must contain at least one field. Values are strings containing URLs to fonts used for rendering the named mode, or an empty string to indicate "default". Typical keys might be "Native script" and "IPA transcription".

#classes
The "classes" field contains an object whose keys are the names of the lexical classes of the language. Each value is a CLASS object.

##CLASS
A CLASS object contains the following fields:
	* "classes"
    * "features"
	* "forms"
	* "rules"
	* "lemmas"
	
###classes
The "classes" field within a CLASS object has the same meaning as the top-level "classes" object, and contains descriptions of subclasses, of which there may be zero or more. Any fields of a subclass may be ommitted, in which case values for the omitted fields are determined by examining the ancestor class. The features and forms specified in a subclass description are added to those defined for all ancestor classes to determine the total number of forms and features for that class. Rules and lemmas in ancestor classes are shadowed by rules for the same forms and lemmas specified on subclasses. If subclasses are present, then any member of the parent class *must* be specified for subclass as well; thus, there should be zero, 2, or more subclasses for any given class.

###features
The "features" field contains an object whose keys are the names of grammatical features of words in the given class. Values may be strings indicating the name of an enumeration, in which case all of the elements of the named enumeration are taken as possible values for the feature; FORM objects with optionally omitted values for irrelevant features, in which case the possible values of the feature include any words whose FORM descriptions match the given object; or a list of explicitly enumerated values.

###forms
The "forms" field contains an object whose keys are the names of different morphological forms of the lexical entry. Each value is a FORM object

####FORM
A FORM object contains the following fields:
    * "class"
	* "values"

#####class
The "class" field contains a string which is the name of the lexical class to which this form belongs. For inflected forms, this will likely be the same as the name of the class being described. For derivational forms, it will likely be the name of a different class. To select a particular subclass, periods are used to separate parent and child class names; e.g. "verb.strong".

#####values
The "values" field contains an object whose keys are the names of features of words of the class named by the "class" field, and whose values are taken from the enumerations of possible values defined for the features of that class. Within a "forms" object, all values must be specified for all features that apply to the given class; within a "features" object, only values that must match should be given, and a list may be used to indicate that multiple values are acceptable for a given feature.

###rules
The "rules" field contains an object whose keys are the names of forms and whose values are RULE objects. Within any class, there may be zero or one rules given for any form; however, there must be at least one form with no rule given to indicate the root or principle part of a lexical entry.

####RULE
A RULE object has fields whose keys are the names of representations and whose values are rules for generating the given form in the given representation. 

###lemmas
The "lemmas" field contains a prioritized list of the names of forms to be used as dictionary head words. In the case of a lexical entry witha  defective paradigm for which the most preferred lemma form does not exist, the first form in the "lemmas" list that exists for the given entry will be used to choose the head-word for the entry.