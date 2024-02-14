# User Groups

A user group is a collection of users who have permissions.
It is a basic data type used by this library and has an owner, a guid, and name.

When a group is created, it only has the owner (the user who created the group) as a member and an admin

## Admins

The creator of the group is the owner of the element , and has special privileges.
The owner is always a member, and an admin. Nobody can remove the owner as admin or member (cannot be kicked out of own group)

Admins are also members. Only the element owner can add or remove other admins. Any admin can add or remove a member

A user group membership is not discoverable to non-members, the attributes read list is updated by that. 
But members can see all the other members and admins.
A user can see which groups they belong in.

Any member of a group can see the full roster, and admins, and any attributes of the group they have permissions to see.

Group ownership cannot be transferred


    So a user-group:
        owner: user_id
        guid: string
        user group parent: (optional)
        parent_combine_strategy (optional) : and, or 
        users: [] who is members in the group
        admins: [] who can directly modify the list using the api.
        name: any name unique to the user's other groups


# group parents
a group can optionally have a single parent, and this restricts or adds to the user group here based on the strategy
* and - the working membership list includes the common users in  the parent and the current
* or - the working membership list includes anyone in the parent and child
