# User Groups

A user group is a collection of users who have permissions.

## Admins 

When a group is created, the creator is recorded as the owner , and has special privileges. 
The group owner is the owner of the token-type, the token, and is automatically an administrator.

A user group has admins, which can alter the membership of the groups. Admins are also members.
Only the group owner, or the group's super admin, can remove other admins.

A super admin is the owner of the group's owner:
By explanation, the group's owner is a user. This user has a token type that is either owned by the system, or another user.
The owner of that user's token type is called the super_admin of the group.
The super admin is also a member of the group, and an admin.


if the user's token type's owner is changed, then this changes out the superuser, both for admin and its membership.

The group owner cannot remove the admins placed by the super admin.


A user group is not discoverable to non-members, but a user can see which groups they belong in.
Any member of a group can see the full roster, and admins, and any attributes of the group they have permissions to see.

The layers can maintain a public user directory, where any user in the public directory can see all the other users

A user group can have attributes for image, docs, but scripts do not run here.

Each user group inherits from a base user group token type. For example, if a company creates a group.





When adding attributes to the token-type, the attributes have to be readable and writable by the owner and whoever is editing

Actions do not run on the token of the user group

    So a user-group:
        users: [] who is members in the group
        user_groups: [] list of groups, any member here is a member of this group 
        admins: [] who can directly modify the list using the api. This also records who added this admin
        admin_groups: list of groups, any member here is an admin of this group. This also records who added this admin group
        token-type: made new for the group, inherits from the system group token type (see system tokens and attributes), the owner of the group is the owner of the token type
        token: the token representing the user group


## Inherited groups to restrict or put conditional membership

The group owner, or superadmin, can change the token type rules for who can use this to make new token types: so can restrict or allow this to be inherited.

Groups that inherit from other group token-types also inherit their memberships and admins.
The superadmin is calculated from the group's owner token type owner. So if a group is inherited , then the super admin will be calculated, and not copied over.
Then, the admin list can change the superadmin entry.

These tokens can be restricted by space and time, and have extra or fewer members and admins

Inherited groups are good for allowing a subset or geo or time fencing permissions for attribute or sets
