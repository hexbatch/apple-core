
# List of api operations

# Users 
-- tags: [users](core/users.md), [user_groups](core/user_groups.md)

user and groups api defined at [users.yaml](../api-docs/users.yaml)

Users and User group operations

| Family | Tags               | Method | Path                    | Operation      | Description                                                                         |
|--------|--------------------|--------|-------------------------|----------------|-------------------------------------------------------------------------------------|
| Users  | users              | Post   | user                    | Create User    | Makes a new user, any user can create a new user                                    |
| Users  | users              | Post   | user/login              | Login User     | Logs the user in, makes a new bearer token for it                                   |
| Users  | users              | Delete | user/logout             | Logout User    | Deletes the user token provided (used to authenticate this operation)               |
| Users  | users              | Put    | user/:id                | Edit User      | Edits user information                                                              |
| Users  | users              | Get    | user/:id                | Read User      | Shows the user information the logged in user can read                              |
| Users  | users, user_groups | Get    | groups                  | List groups    | Shows the groups the user belongs to, lists the admin status                        |
| Users  | user_groups        | Post   | group/new               | create group   | Creates a new group that inherits from the user's group, can be ancestor or parent  |
| Users  | user_groups        | Get    | group/:id               | read group     | lists the attributes, and members and admins of this group : can search for members |
| Users  | user_groups        | Delete | group/:id               | delete group   | Owner of group can delete only if not used anywhere for permissions                 |
| Users  | user_groups        | Put    | group/:id               | edit group     | Sets the attributes of the group                                                    |
| Users  | user_groups        | Post   | group/:id/member/new    | add members    | Adds membership via a single user or a group                                        |
| Users  | user_groups        | Delete | group/:id/member/remove | remove members | Removes membership via a single user or a group                                     |
| Users  | user_groups        | Delete | group/:id/admin/remove  | remove admins  | Removes admin via a single user or a group, cannot remove some admins               |
| Users  | user_groups        | Post   | group/:id/admin/new     | add admins     | Add admin via a single user or a group                                              |


# Bounds
-- tags: [bounds](core/bounds.md), [location_bounds](core/location_bounds.md), [time_bounds](core/time_bounds.md)

bounds api defined at [bounds.yaml](../api-docs/bounds.yaml)

Create and manage bounds. Bounds are made up of collections of times and locations.
Bounds can only be edited or deleted if they are not used anywhere.


| Family     | Tags            | Method | Path                                    | Operation                                | Description                                                      |
|------------|-----------------|--------|-----------------------------------------|------------------------------------------|------------------------------------------------------------------|
| Boundaries | bounds          | Post   | bounds                                  | Create Boundary                          | Boundaries are made: the user who made this call and a name      |
| Boundaries | bounds          | Delete | bounds/:id                              | Remove Boundary                          | Deletes an unused boundary                                       |
| Boundaries | bounds          | Get    | bounds/:id                              | List Boundary                            | Lists the locations and times in a boundary, can filter          |
| Boundaries | bounds          | Get    | bounds/:id/time/schedule                | List Boundary's schedule                 | Shows a list of start and stop times for the entire boundary     |
| Boundaries | bounds          | Get    | bounds/:id/location/area                | List Boundary's area                     | Shows a list of polygons for the entire boundary                 |
| Boundaries | bounds          | Get    | bounds/:id/ping                         | Tell if time and/or location in boundary | returns true or false if a time and or location is in a boundary |
| Boundaries | bounds          | Get    | bounds                                  | List Boundaries                          | Lists boundaries, options to filter for used or unused           |
| Boundaries | bounds          | Delete | bounds/:id                              | Remove Bounds                            | Unused boundaries can be removed                                 |
| Boundaries | location_bounds | Post   | bounds/:bound_id/location               | Create Location                          | Makes a new location: a name and at least one polygon            |
| Boundaries | location_bounds | Put    | bounds/:bound_id/location/:id           | Edit Location                            | Changes the polygons or name in a location                       |
| Boundaries | location_bounds | Delete | bounds/:bound_id/location/:id           | Delete Location                          | Removes location                                                 |
| Boundaries | location_bounds | Get    | bounds/:bound_id/location/:id           | List Location details                    | Shows location details : list of polygons                        |
| Boundaries | location_bounds | Get    | bounds/:bound_id/location/:id/ping      | Tells if location is in area             | Returns true or false if a map coordinate is in the locations    |
| Boundaries | time_bounds     | Post   | bounds/:bound_id/times                  | Create Times                             | Makes a new times, a name and at least one rule                  |
| Boundaries | time_bounds     | Put    | bounds/:bound_id/time/:id               | Edit Times                               | Changes the time definition or name in a time                    |
| Boundaries | time_bounds     | Delete | bounds/:bound_id/time/:id               | Delete Times                             | Removes times                                                    |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/:id               | List Times                               | Shows time details, shows the rules here                         |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/schedule/:id      | List Times                               | Shows a list of start and stop times for this time               |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/schedule/:id/ping | Tells if time is in schedule             | Returns true or false if a time is in a schedule                 |




# Attributes

-- tags: [attributes](core/attributes.md)

attribute api defined at [attributes.yaml](../api-docs/attributes.yaml)

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


# Actions

-- tags: [actions](core/actions.md)

actions api defined at [actions.yaml](../api-docs/actions.yaml)

Actions have an owner, version, name, target, lifecycle, recipient, charge, options,script

| Family  | Tags    | Method | Path            | Operation         | Description                                                                                                               |
|---------|---------|--------|-----------------|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| Actions | actions | Post   | action          | Create Action     | Makes a new action with an owner and a name: optional version, name, target, lifecycle, recipient, charge, options,script |
| Actions | actions | Put    | action/:id      | Edit Action       | Edit name, version, name, target, lifecycle, recipient, charge, options,script   : only if not used                       |
| Actions | actions | Delete | action/:id      | Delete Action     | Only if not used                                                                                                          |
| Actions | actions | Get    | action/:id/run  | Run Action        | Run action, giving any parameters, location or set info, get back any (dry run) changes for recipient and charge          |
| Actions | actions | Get    | action/:id/list | Show Action Usage | Gives a list of attributes this action is used at                                                                         |



# Tokens and Types

-- tags [token_types](core/token_types.md)

token type api defined at [tokens.yaml](../api-docs/tokens.yaml)

Token types have an owner, options, attributes, and parents

Token types name and info are in its attributes 

(other api here involve creating the token, getting token attribute values , and making a type-group)

| Family | Tags        | Method | Path | Operation         | Description                                                           |
|--------|-------------|--------|------|-------------------|-----------------------------------------------------------------------|
| Type   | token-types | Post   | type | Create Token Type | Makes a new token type with an owner options, attributes, and parents |

