# Type groups

Type groups are used in token set operations

A token-type can be added into a type-group:

Tokens types can belong to one or more type-groups.

A type-group can be used in token-set operations, where tokens are added or removed between sets

Type-group can have a token to denote who owns it, and any attributes , to give it a name and appearance, or notes, and to provide logic for set operations
* Attributes can have those inherited from the attribute_filter which can look at the set to filter and decide which will be allowed

Ownership is not used when type-groups are used in set operations

The token types can have a max and min amounts. In set operations the exact amount used will default to be either the min,then max if min not set, or all available if neither

The token types can also have needed attributes with a min or max for number ranges, or/and a value to match strings with constants or regex. or and a numeric value.
When attributes are set, the live and inherited attributes that are on for the token are filtered here

    So: a type-group:
        token: (optional) if some description is needed for this type-group, or for identifying it with a set path, or putting bounds of when this can be used
        token-types: [ {
            type: token-type
            minimum_needed: optional
            maximum_needed: optional
            attributes: [{
                attribute id, ( also parent or ancestor)
                attribute_min:
                attribute_max:
                string_value: (constant or regex)
                numeric_value: (numeric)
            }]
        }]