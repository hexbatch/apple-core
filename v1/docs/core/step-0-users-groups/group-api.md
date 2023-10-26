# Users

groups api defined at [users.yaml](../../../api-docs/users.yaml)

Users operations

| Method | Path                    | Operation      | Description                                                                         |
|--------|-------------------------|----------------|-------------------------------------------------------------------------------------|
| Post   | group/create            |                |                                                                                     |
| Post   | group/:id/member/new    | add members    | Adds membership via a single user or a group                                        |
| Delete | group/:id/member/remove | remove members | Removes membership via a single user or a group                                     |
| Delete | group/:id/admin/remove  | remove admins  | Removes admin via a single user or a group, cannot remove some admins               |
| Post   | group/:id/admin/new     | add admins     | Add admin via a single user or a group                                              |
