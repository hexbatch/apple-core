# Tokens

Tokens are made from token types, and have live values of those attributes.

Tokens can have other attributes added to them individually, either that are not in the token type, or overwriting the token type's added on to them

Tokens have their aggregate values: bounds, affinities, allergies

the token api will get its live attribute values, some or many of the token attribute depend on the set it is in.

Tokens can have attributes dynamically added to them, even if they are not in the token type. Attributes of the same name added this way overwrite the type attribute.
The user who owns the token can add attributes, also the token type owner can add attributes.

Static values can be changed just for this token. The actions have their own local state for this token.

Tokens also have a location, and an owner.

Having a location allows map bounded attributes to work. Attributes that have location bounds in a token without location automatically do not work, and are off.

This also means that some tokens cannot be taken to some locations or usable at some times.

Only the token owner can change who owns his token next. A set of tokens can have ownership changed.

A token can be affected by some attributes set in the token type, or dynamically.
* lifetime : this sets the bounds that the token can exist in, for instance will be deleted after a certain time.

      So a token:
          user: must be one user
          token-type:
          location:
            the lat and lon (optional)
          live attributes: (see attributes)
          live parents:  

A token has aggregate values made from its attributes: bounds, affinities, allergies 

Tokens have live attributes and live parents

## Live parents

each inherited parent has a live state, and can be turned off and on

## Live attributes

the list of active attributes for a token, it can be added to with attributes not on the list.
The active attributes from the parents are chosen as the top most attribute for each name, in order of parent inheritance list 