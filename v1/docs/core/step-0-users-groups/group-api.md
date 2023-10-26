# Users

groups api defined at [users.yaml](../../../api-docs/users.yaml)

group operations:

when creating a group, the user calling this is the group owner and the first admin

| Method | Path                    | Route Name | Operation                            | Description                                                           | Args                     |
|--------|-------------------------|------------|--------------------------------------|-----------------------------------------------------------------------|--------------------------|
| Post   | group/create            |            | create group                         |                                                                       | parent token type guid   |
| Post   | group/:id/destroy       |            | destroy group                        | Can only be deleted if not in use anywhere                            |                          |
| Post   | group/:id/member/add    |            | add members                          | Adds membership via a single user or a group                          | user guid, or group guid |
| Delete | group/:id/member/remove |            | remove members                       | Removes membership via a single user or a group                       | user guid, or group guid |
| Delete | group/:id/admin/remove  |            | remove admins                        | Removes admin via a single user or a group, cannot remove some admins | user guid, or group guid |
| Post   | group/:id/admin/add     |            | add admins                           | Add admin via a single user or a group                                | user guid, or group guid |
| GET    | group/:id/list          |            | shows group                          | lists the membership and admins                                       |                          |
| GET    | groups/list             |            | shows groups the user is involved in | lists the groups by guid                                              |                          |

