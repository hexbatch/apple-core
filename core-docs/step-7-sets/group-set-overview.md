# Group sets

Only the owner of a group can make it into a group set.

When membership of a group becomes more than just permissions, there is the group set. Which is a set that is in sync with a group.

When making a group set, a new type is made that must have one of its parents be from the standard group set type (it can have other parents).

Then an element is made from this to create a set, and all the members and admin user elements are in this set.

The set element has special events that fire on it when members/admins are added or removed. And the element provides standard attributes to describe the group.

The new type can be parents of other things types related to the group. But only one element can be made from this type.

Admins of the group have permissions to write the attributes, and add in new attributes, members have ability to read the attributes

## Events fired

* member_added
* member_removed
* admin_added
* admin_removed


## Restricting the context a group can be used in

The group element can have bounds set on it.
If a subgroup needs to be made, or have some members be in one bounds compared to others, or a group needs to be sorted and organzied,
Then a new group can be made, and put as a child into the parent group set, this can be nested. 
The new group has the members added to it from the parent group.
And, that new group can be restricted to only contain members of the parent group.


## Api calls that list groups

Can search for groups using attributes, values and who owns them, or what set they may belong to
