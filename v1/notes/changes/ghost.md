Ghost attributes:

Can stick a live attribute on any token you can read, and this attribute is only readable to the user group you specify when sticking it on.
The attribute is writable by the admins of the user group.

* Permissions are ignored when adding this, but it cannot be seen outside the group, not even by the token or type owner.
* Attribute cannot overwrite any attributes not a ghost, and only overwrites another ghost attribute if the same user can see more then one.
    In that case, the most recent is seen.
* Ghost attribute cannot affect the target token in any way, or affect any of the tokens that share a set with it.

Ghost attributes can be added to the token in a set, path, or global context.

Ghost attributes can be used to iterate groups of the same attributes on different tokens, to organize, or tag data