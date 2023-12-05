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
When an attribute is off, the bounds are still counted, but the allergies and affinities are not.

Tokens by themselves do not have a location, they can have an attribute though that is standard defined, called current_location.
This is only valid for lat and lon. The current_location can be anywhere in the token bounds, and this is not used to determine if the token matches a set location.
A single token can have many current_location values at once, if the values are not global, but set based.

The cartesian bounds also can set their current location too, with current_location_cartesian attributes
 
Tokens can describe their shape or area, this description is clipped to their locations bounds. The standard attributes shape_cartesian, shape_map.
if there are more than one attribute that inherits from this, on the token, then each family of attributes is unionized to make the shape, which is still clipped to the bounds.
The shape is centered at the current location (map to map and cartesian to cartesian never the two shall meet )


When a token defines a set, it's location bounds is what defines the membership in a set:
deciding how it interacts with entering or being visible in a set that has a bounds or no bounds.


The time of the token is always the current time. When looking at the time attributes.
Path bounds work by the api making calls using the working set


Only the token owner or those in the user's admin group can change who owns his token. To give it to another user.
Ownership of tokens can take place in bulk via set operations.

A token may be in any number of sets at once.
The token bounds does not change when the set bounds changes.

A token can have the date set so that after it, it's not used or usable, and eventually is recycled. This is determined by the types time to live option


      So a token:
          user: must be one user
          token-type:
          expiration_at: (optional by type)  
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


## time to live

is like a very hard set time boundary for the token, and in many ways is just that, it's factored into any time boundaries the token.
Once its past the time to live, the token is not usable, because of the time boundary ending, and there is an api in the admin area to start gc