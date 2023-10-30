# Standard Attributes

attribute api defined at [attributes.yaml](../../../api-docs/attributes.yaml)

There are groups of standard attributes: can use this api to find them, and their descriptions and documentation

| Method | Path                  | Route Name                | Operation                                   | Args |
|--------|-----------------------|---------------------------|---------------------------------------------|------|
| Get    | standard/families     |                           | gets list of families (string array)        |      |
| Get    | standard/:family/list | core.standard.family.list | returns a family structure                  |      |
| Get    | standard/:id          |                           | returns single standard attribute structure |      |


Families return for each family
    
    name of family
    

Family structure:

    name:
    standard_attributes:
    docs: markdown string

standard_attribute structure:

    name:
    default_value:
    docs: markdown string


## For all returns 

Docs can be translated to other languages, if it matches the language set in the call it will use that instead.
Name is returned using alias if possible