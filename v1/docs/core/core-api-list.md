
# List of api operations

## Common api

* time is read in unix timestamp or iso-standard.
* any api call can have the wide modifier, showing the attributes, that the user can read, of each token and token type returned
* each top level and secondary level resource returned has a list of action links for it
* Pages is done by cursor, long results are paged
* optional language is chosen by the header of the accept language: the library will choose the best fitting one. `Accept-Language: fr; q=1.0, en; q=0.5`

# Users
[user-api.md](step-0-users-groups/user-api.md)

# User Groups
[groups api](step-0-users-groups/group-api.md)

# User Admin
[user admin api](step-0-users-groups/admin-api.md)


# Bounds
* [map api](step-1-bounds/map-api.md)
* [map api](step-1-bounds/time-api.md)
* [map api](step-1-bounds/path-api.md)


# Attributes
* [standard attribute api](step-2-attributes/standard-attribute-api.md)
* [attribute api](step-2-attributes/attribute-api.md)


# Scripts
[script api](step-3-scripts-urls/script-api.md)


# Remotes
* [remote api](step-3-scripts-urls/remote-api.md)

# Metrics
* [metrics api](step-3-scripts-urls/metrics-api.md)

# Actions
[actions](step-4-actions/actions-api.md)


# Types
[token_types](step-5-types/type-api.md)

# Tokens
[token-api.md](step-6-tokens/token-api.md)
