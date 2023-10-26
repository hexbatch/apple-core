
# List of api operations

## Common api

* time is read in unix timestamp or iso-standard.
* any api call can have the wide modifier, showing the attributes, that the user can read, of each token and token type returned
* each top level and secondary level resource returned has a list of action links for it
* Pages is done by cursor, long results are paged

# Users 
    
[user-api.md](step-0-users-groups/user-api.md)

# User Groups

[groups api](step-0-users-groups/group-api.md)

# User Admin

[user admin api](step-0-users-groups/admin-api.md)

# Rate Limits

[rate limit api](step-0-users-groups/rate-limits-api.md)


# Bounds
* [map api](step-1-bounds/map-api.md)
* [map api](step-1-bounds/time-api.md)
* [map api](step-1-bounds/path-api.md)


# Attributes

-- tags: [attributes](attributes.md)

attribute api defined at [attributes.yaml](../../api-docs/attributes.yaml)

Attribute have an owner, a name, bounds, requirements, permissions, and a value.

While attributes have a lot to set, most of this is done in hte create and edit

| Family     | Tags       | Method | Path                      | Operation                    | Description                                                                                            |
|------------|------------|--------|---------------------------|------------------------------|--------------------------------------------------------------------------------------------------------|
| Attributes | attributes | Post   | attribute                 | Create Attribute             | Makes a new attributes with an owner and a name: optional requirements, permissions, bounds, and value |
| Attributes | attributes | Put    | attribute/:id             | Edit Attributes              | Edits the attribute, if the user can                                                                   |
| Attributes | attributes | Put    | attribute/:id/value       | Edit Value                   | Edits the attribute value, if the user can                                                             |
| Attributes | attributes | Get    | attribute/:id             | Edit Attributes              | Reads the attribute details, if the user can                                                           |
| Attributes | attributes | Get    | attribute/:id/value       | Read Value                   | Reads the attribute value, if the user can. Optional to set position, uses time                        |
| Attributes | attributes | Get    | attribute/:id/bounds/ping | Ping Attributes              | Determines if the attribute is at the location and time asked about                                    |
| Attributes | attributes | Get    | attribute/:id/permissions | Ask about permissions        | returns permission about this user and this attribute                                                  |
| Attributes | attributes | Get    | attribute/:id/list        | Show where attribute is used | returns list of tokens and other where the attribute is used                                           |
| Attributes | attributes | Delete | attribute/:id             | Delete Attributes            | Deletes the attribute, if the user can and if the attribute is not used anywhere                       |


# Scripts

todo add scripts 

-- tags: [scripts](scripts.md)


# Urls
-- tags: [urls](urls.md)

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

