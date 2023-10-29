# Tokens
Tokens are the only thing which can change ownership. Tokens always have an owner.

Tokens are made from token types, and have live values of those attributes.
Only the allowed users for a type can make a token from it.

When a token is made, the attributes of the token type have values copied over,
and an on/off state, found in the live attributes.

When the attribute of a token is written to or read from, it is using this live state.

Tokens can have all the attributes of a parent turned off or on by an action.
Tokens have a live parent section that shows which parents are on.

Tokens can have other attributes added to them individually. 
These attributes can be either those are not in the token type,
or can overwrite the attributes that are already live.

Token owners can add in the extra attributes, or those who are in the user admin group.

Tokens have their aggregate values: bounds, affinities, allergies. This is the union of each.
This also means that some tokens cannot be taken to some locations or usable at some times.
Token's behavior in a set depends on these aggregate values for affinities, allergies and path bounds.

Tokens also have an optional location. 
If map bounds is set but not the location, the token will be considered out of bounds.
The time of the token is always the current time. When looking at the time attributes.
Path bounds work by the api making calls using the working set


Only the token owner or those in the user's admin group can change who owns his token. To give it to another user.
Ownership of tokens can take place in bulk via set operations.

A token does not need to be owned to be placed in any set. A token may be in any number of sets at once.
The token location does not change when the set location changes.


      So a token:
          user: must be one user
          token-type:
          location:
            the lat and lon (optional)
          live attributes: (see attributes)
          live parents:  
          script and remote states:  


## Live parents
[live parents overview](live-parent-overview.md)

Each inherited parent has a live state, and can be turned off and on

## Live attributes
[Live attributes](live-attribute-overview.md)

the list of active attributes for a token, it can be added to with attributes not on the list.
The active attributes from the parents are chosen as the top most attribute for each name,
in order of parent inheritance list 