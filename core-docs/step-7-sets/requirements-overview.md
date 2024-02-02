# Requirements

Requirements are used in token set operations and to restrict the types, amounts, and attributes going into a set, or being part of a set operation
A requirement can be used in token-set operations, where tokens are added or removed between sets

Requirements are owned by a user. It can also have a token to explain more about it. This token can also give it a name, appearance, and notes and bounds.
The requirement token can be used anywhere else in the system at the same time, and one token can do many requirements


A type in the group can have a max and/or min amounts. If only a max or min is set, then that is the only rule used.

A type can further restrict the needs, with attributes that must be present on the type.
These attributes can be restricted by value
There can be  min or max for number ranges, or/and a value to match strings with constants or regex. or and a numeric value.
When attributes are set, the live and inherited attributes that are on for the token are filtered here.
When an attribute is filtered, so are all its descendants.

When attribute requirements are added, then any rules set up for compatibility are ignored

Requirements can have a token:
(only for top leve) Sets ownership,adds some description is needed for this requirement, or for identifying it with a set path, or putting bounds of when this can be used

Requirements can have children, and be a tree

    So: a requirement:
        id
        user_id:
        token: (optional)
        parts: [ {
            part_id: each part has a unique id
            type: type,
            weight: optional,
            parent_part_id: (optional)
            children: [] (read only)
            required: (default false)
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

options:
* weight of the part allows sorting of search results, as well as prioritizing which types are the best or more preferred
* some parts are optional, some are required. More than one can be required, or none at all
* Can have maximum_needed be zero to disallow something

## Requirement events

Because the requirement has an optional token, events here can be done on it when it's used to filter
* allow_token event

## Requirement trees

Parts can be done in stages, from the bottom most leaves on up, each layer passes the allowed tokens to the parent node
