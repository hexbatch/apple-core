# Users



group operations:

when creating a group, the user calling this is the group owner and the first admin

when :id is mentioned here, it's the group element guid, or the name of the group.
The name can be prefixed by the user identifier of the owner. When the owner is calling, prefix is optional.
The owner can be identified by its username, uuid or user element 
    
    `secondary_bastion.other_thing`

when members and admins are mentioned, it's their elements.

If one is not in a group, cannot get any group info


| Method | Path                          | Route Name               | Description                                                       | Args                    |
|--------|-------------------------------|--------------------------|-------------------------------------------------------------------|-------------------------|
| Post   | group/create                  | core.group.create        | create group,returns the group guid                               | required group_name:    |
| Delete | group/:id/destroy             | core.group.destroy       | destroy group.Can only be deleted if not in use anywhere          |                         |
| Put    | group/:id/member/add/:user    | core.group.member.add    | Adds membership to a single user                                  | user element guid or id |
| Delete | group/:id/member/remove/:user | core.group.member.remove | Removes membership for a single user                              | user element guid or id |
| Patch  | group/:id/admin/remove/:user  | core.group.admin.remove  | Removes admin status for a single user, they are still member     | user element guid or id |
| Put    | group/:id/admin/add/:user     | core.group.admin.add     | Add admin status for a single user                                | user element guid or id |
| GET    | group/:id/list                | core.group.list          | lists the membership and admins                                   | iterator for next page  |
| GET    | groups/list                   | core.user.groups.list    | lists the groups by guid, that user is involved in                | iterator for next page  |
| GET    | group/:id/get                 | core.group.get           | shows the group and membership status for this user in that group | iterator for next page  |


    user-group:
        owner: user_id
        users: [] who is members in the group
        admins: [] who can directly modify the list using the api.
        name: any name unique to the user's other groups
