# User Groups

A user group is a collection of users who have permissions.
It is defined by a token that inherits from the user, and inherits the base group token.


The user list of the group, and the admin list, is reflected in the api as attributes, but it's also stored in the db as user lists.
The attributes allow other parts of the api to read it. The attribute type here is created for the group, and inherits from a base user membership attribute.

The admins are also listed as attributes, which inherits from the group admin attribute which inherits from the user memberships. 

The user group base type is not allowed to create tokens unless its by an api call that creates groups.
Attributes that define members and admins are not allowed to be created or destroyed except in api calls that do group lists.

User groups can contain live memberships or admins from other groups. These are represented as attributes that point to the group
and are using the system attribute types for attached member group, attached admin group which inherits from the base user membership attribute

an admin can remove a member, the token owner can remove an admin. When this happens the attribute listing them is removed.

The attributes store the ids of the users and groups in json arrays

## Admins

When a group is created, the creator of the group is the owner of the token , and has special privileges.

A user group has admins, which can alter the membership of the groups. Admins are also members.
Only the token owner,  can add or remove other admins.

A user group membership is not discoverable to non-members, the attributes read list is updated by that. 
But members can see all the other members and admins.
A user can see which groups they belong in.

Any member of a group can see the full roster, and admins, and any attributes of the group they have permissions to see.

A user group can have attributes for image, docs, actions can run on when adding or removing attributes (including the membership attributes)


The token can be used as a regular token anywhere else, but can only represent one group, the group its attached to.
It cannot represent another resource


    So a user-group:
        users: [] who is members in the group
        admins: [] who can directly modify the list using the api.
        token: the token representing the user group


## Restricting the context a group can be used in

The group token can have bounds set on it.
If a subgroup needs to be made, or allowing a subset or geo or time fencing permissions or path restrictions,
then a new group can be made, and the members added to it from the older group.
Membership or administration in the earlier group does not affect status in the newer group



### Multi membership and admin additions that repeat

The admin or membership is the union of all the users added


## Api calls that list groups

Can search for groups using attributes, values and who owns them, or what set they may belong to
