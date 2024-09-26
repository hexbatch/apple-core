
# List of api operations

## Common api

* time is read in unix timestamp or iso-standard.
* any api call can have the wide modifier, showing the attributes, that the user can read, of each element and element type returned
* each top level and secondary level resource returned has a list of action links for it
* Pages is done by cursor, long results are paged
* optional language is chosen by the header of the accept language: the library will choose the best fitting one. `Accept-Language: fr; q=1.0, en; q=0.5`

# Users, groups, admin
* [user-api.md](step-0-users-groups/user-api.md)
* [groups api](step-0-users-groups/group-api.md)
* [user admin api](step-0-users-groups/user-admin-tasks.md)


# Bounds
* [map api](step-1-bounds/location-api.md)
* [time api](step-1-bounds/time-api.md)
* [path bounds api](step-1-bounds/path-api.md)


# Attributes
* [attribute api](step-2-attributes/attribute-api.md)


# Remotes, Metrics
* [remote api](step-3-remotes/remote-api.md)



# Actions
* [actions](step-4-actions/actions-api.md)
* [servers](step-4-actions/server-api.md)

# Types
[element_types](step-5-types/type-api.md)

# Elements
[element-api.md](step-6-elements/element-api.md)

# Sets
* [set-api](step-7-sets/set-api.md)
* [search api](step-7-sets/search-api.md)
* [operations api](step-7-sets/operations-api.md)
