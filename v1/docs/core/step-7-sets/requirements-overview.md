# Requirements

Requirements are used in token set operations and to restrict the types, amounts, and attributes going into a set, or being part of a set operation
A requirement can be used in token-set operations, where tokens are added or removed between sets

Requirement has a token to denote who owns it. This token can also give it a name, appearance, and notes and bounds.
the requirement token can be used anywhere else in the system at the same time, and one token can do many requirements


A type in the group can have a max and/or min amounts. If only a max or min is set, then that is the only rule used.

A type can further restrict the needs, with attributes that must be present on the type.
These attributes can be restricted by value
There can be  min or max for number ranges, or/and a value to match strings with constants or regex. or and a numeric value.
When attributes are set, the live and inherited attributes that are on for the token are filtered here.
When an attribute is filtered, so are all its descendants.

When attribute requirements are added, then any rules set up for compatibility are ignored

    So: a requirement:
        id
        token: Sets ownership,adds some description is needed for this requirement, or for identifying it with a set path, or putting bounds of when this can be used
        parts: [ {
            part_id: each part has a unique id
            type: token-type
            minimum_needed: optional
            maximum_needed: optional
            attributes: [{
                attribute id, ( also parent or ancestor)
                numeric_min:
                numeric_max:
                string_value: (constant or regex)
                numeric_value: (numeric) min and max ignored
            }]
        }]


## Requirement events

Because the requirement has an optional token, events here can be done on it when it's used to filter
* Allow token