# Users

groups api defined at [users.yaml](../../../api-docs/users.yaml)

group operations:

when creating a group, the user calling this is the group owner and the first admin

When a group is created, no info is given to it, the group attributes can be edited with the returned token

when :id is mentioned here, it's the group token guid, or the name of the group

when members are listed, it's their ids

when adding or removing group members or admins, the adding can be done with groups. If using a group in a non group api, then the current members only are added or removed
When using a group in a group api, then at any future time, that group membership will be used

names of groups: must be unique, starts with the username then a dot, then an alias for 'group', then another dot,  then a unique name for a group

| Method | Path                          | Route Name | Operation                            | Description                                                           | Args                                                  |
|--------|-------------------------------|------------|--------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------|
| Post   | group/create                  |            | create group                         | returns the group token guid made                                     | parent token type guid,optional name of the group     |
| Post   | group/:id/destroy             |            | destroy group                        | Can only be deleted if not in use anywhere                            |                                                       |
| Post   | group/:id/member/add          |            | add members                          | Adds membership via a single user or a group                          | user guid/name, or group guid/name                    |
| Post   | group/:id/member/add-group    |            | add members                          | Adds membership via another group                                     | group guid/name                                       |
| Delete | group/:id/member/remove       |            | remove members                       | Removes membership via a single user or a group                       | user guid/name, or group guid/name                    |
| Delete | group/:id/member/remove-group |            | remove members                       | Removes membership via another group                                  | group guid/name                                       |
| Delete | group/:id/admin/remove        |            | remove admins                        | Removes admin via a single user or a group, cannot remove some admins | user guid/name, or group guid/name                    |
| Delete | group/:id/admin/remove-group  |            | remove admins                        | Removes admin via another group                                       | group guid/name                                       |
| Post   | group/:id/admin/add           |            | add admins                           | Add admin via a single user or a group                                | user guid/name, or group guid/name                    |
| Post   | group/:id/admin/add-group     |            | add admins                           | Add admin via another groupp                                          | group guid/name                                       |
| GET    | group/:id/list                |            | shows group                          | lists the membership and admins                                       | optional wide flag to show group standard attributes  |
| GET    | groups/list                   |            | shows groups the user is involved in | lists the groups by guid                                              | optional wide flag to show group standard attributes  |

