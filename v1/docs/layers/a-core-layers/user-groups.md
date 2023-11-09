# User groups

## Listing Groups

Any member of a groups can see the full list of the group members and admins

## Groups Operation list

* create group
* edit group attributes (any admin)
* view group (any member)
* add group member (any admin)
* remove group member (any admin)
* add admin (only if group owner)
* remove admin (only if group owner)
* change group ownership (only if owner)

## Group data

Can read group data if a member, Can set group data if an admin

All users are admins of their own user group, and members of the regular_user group, and can be added to other groups as needed

Reading group data:
* name : string
* description : markdown
* schedule (same as when setting time boundary)
* area (same as when setting map boundary)
* members: array of user data
* admins : array of user data
* token : guid of the group token if need more


writing group data is done by setting the name and/or description