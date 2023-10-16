
# List of api operations

# Users 
-- tags: [users](core/users.md), [user_groups](core/user_groups.md)

user and groups api defined at [users.yaml](../api-docs/users.yaml)

Users and User group operations

| Family | Tags               | Method | Path                    | Operation      | Description                                                                         |
|--------|--------------------|--------|-------------------------|----------------|-------------------------------------------------------------------------------------|
| Users  | users              | Post   | user/new                | Create User    | Makes a new user, any user can create a new user                                    |
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
| Boundaries | bounds          | Post   | bounds/new                              | Create Boundary                          | Boundaries are made: the user who made this call and a name      |
| Boundaries | bounds          | Delete | bounds/:id                              | Remove Boundary                          | Deletes an unused boundary                                       |
| Boundaries | bounds          | Get    | bounds/:id                              | List Boundary                            | Lists the locations and times in a boundary, can filter          |
| Boundaries | bounds          | Get    | bounds/:id/time/schedule                | List Boundary's schedule                 | Shows a list of start and stop times for the entire boundary     |
| Boundaries | bounds          | Get    | bounds/:id/location/area                | List Boundary's area                     | Shows a list of polygons for the entire boundary                 |
| Boundaries | bounds          | Get    | bounds/:id/ping                         | Tell if time and/or location in boundary | returns true or false if a time and or location is in a boundary |
| Boundaries | bounds          | Get    | boundaries                              | List Boundaries                          | Lists boundaries, options to filter for used or unused           |
| Boundaries | bounds          | Delete | bounds/:id                              | Remove Bounds                            | Unused boundaries can be removed                                 |
| Boundaries | location_bounds | Post   | bounds/:bound_id/location/new           | Create Location                          | Makes a new location: a name and at least one polygon            |
| Boundaries | location_bounds | Put    | bounds/:bound_id/location/:id           | Edit Location                            | Changes the polygons or name in a location                       |
| Boundaries | location_bounds | Delete | bounds/:bound_id/location/:id           | Delete Location                          | Removes location                                                 |
| Boundaries | location_bounds | Get    | bounds/:bound_id/location/:id           | List Location details                    | Shows location details : list of polygons                        |
| Boundaries | location_bounds | Get    | bounds/:bound_id/location/:id/ping      | Tells if location is in area             | Returns true or false if a map coordinate is in the locations    |
| Boundaries | time_bounds     | Post   | bounds/:bound_id/times/new              | Create Times                             | Makes a new times, a name and at least one rule                  |
| Boundaries | time_bounds     | Put    | bounds/:bound_id/time/:id               | Edit Times                               | Changes the time definition or name in a time                    |
| Boundaries | time_bounds     | Delete | bounds/:bound_id/time/:id               | Delete Times                             | Removes times                                                    |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/:id               | List Times                               | Shows time details, shows the rules here                         |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/schedule/:id      | List Times                               | Shows a list of start and stop times for this time               |
| Boundaries | time_bounds     | Get    | bounds/:bound_id/time/schedule/:id/ping | Tells if time is in schedule             | Returns true or false if a time is in a schedule                 |




# Attributes

-- tags: [attributes](core/attributes.md)

bounds api defined at [attributes.yaml](../api-docs/attributes.yaml)

Attribute have an owner, a name, bounds, requirements, permissions, and a value

| Family     | Tags       | Method | Operation         | Description                                                                                            |
|------------|------------|--------|-------------------|--------------------------------------------------------------------------------------------------------|
| Attributes | attributes | Post   | Create Attributes | Makes a new attributes with an owner and a name: optional requirements, permissions, bounds, and value |