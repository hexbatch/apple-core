# User Groups

A user group is a collection of users who have permissions. It is defined by a token that inherits from the user, and the base group token

## Admins 

When a group is created, the creator of the group is recorded as the owner , and has special privileges. 

A user group has admins, which can alter the membership of the groups. Admins are also members.
Only the group owner,  can add or remove other admins.


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
        admins: [] who can directly modify the list using the api. 
        admin_groups: list of groups, any member here is an admin of this group. 
        token-type: made new for the group, inherits from the system group token type (see system tokens and attributes), the owner of the group is the owner of the token type
        token: the token representing the user group


## Inherited groups to restrict or put conditional membership

The group owner, o can change the token type rules for who can use this to make new token types: so can restrict or allow this to be inherited.

Groups that inherit from other group token-types also inherit their memberships and admins.

These tokens can be restricted by space and time, and have extra or fewer members and admins

Inherited groups are good for allowing a subset or geo or time fencing permissions for attribute or sets


## Api calls that list groups

Search results give back iterators and a page contents, use the iterator id to get the next page,
iteration is one way only and can have duplicates in the results as things are updated in between calls for a page
