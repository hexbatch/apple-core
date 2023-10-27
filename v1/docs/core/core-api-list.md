
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

* [script api](step-3-scripts-urls/script-api.md)


# Remotes
* [remote api](step-3-scripts-urls/remote-api.md)

# Metrics

* [metrics api](step-3-scripts-urls/metrics-api.md)

# Actions

-- tags: [actions](actions.md)

actions api defined at [actions.yaml](../../api-docs/actions.yaml)

Actions have an owner, version, name, target, lifecycle, recipient, charge, options,script

| Family  | Tags    | Method | Path            | Operation         | Description                                                                                                               |
|---------|---------|--------|-----------------|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| Actions | actions | Post   | action          | Create Action     | Makes a new action with an owner and a name: optional version, name, target, lifecycle, recipient, charge, options,script |
| Actions | actions | Put    | action/:id      | Edit Action       | Edit name, version, name, target, lifecycle, recipient, charge, options,script   : only if not used                       |
| Actions | actions | Delete | action/:id      | Delete Action     | Only if not used                                                                                                          |
| Actions | actions | Get    | action/:id/run  | Run Action        | Run action, giving any global or local state, or action info, get back any (dry run) changes for recipient and charge     |
| Actions | actions | Get    | action/:id/list | Show Action Usage | Gives a list of attributes this action is used at                                                                         |



# Tokens and Types

-- tags [token_types](token_types.md)

token type api defined at [tokens.yaml](../../api-docs/tokens.yaml)

Token types have an owner, options, attributes, and parents

Token types name and info are in its attributes 

(other api here involve creating the token, getting token attribute values , and making a type-group)

| Family | Tags        | Method | Path | Operation         | Description                                                           |
|--------|-------------|--------|------|-------------------|-----------------------------------------------------------------------|
| Type   | token-types | Post   | type | Create Token Type | Makes a new token type with an owner options, attributes, and parents |

