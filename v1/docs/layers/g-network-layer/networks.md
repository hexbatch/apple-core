# Networks

Networks are things online related to a user. These resources might become future users, or become other resources.
Tracks social accounts that are not users, and then later are

Each network has a type of network, so there is an api to create different types of networks

For example, some network types might be:
* Facebook
* Skype
* Some email list somebody bought

Then a network entry is some information that has a network type, each network type has some minimum required info. For example facebook must require an account name,
an email entry must require an email address.

Each user can have a set for associated network entries they know about.

Two sets for a user:
* network entries that are connected to them -such as their friends in social platform. This called associated-network
* network entries that are part of their identity - such as their username on skype. This is called identity-networks


When a network entry is made, its information is scanned against the users who have the same attribute type (ie facebook account name),
If a user already exists that matches this, then that network entry is added to the identity-networks set each user can have that is their network entries.


Later, when a user is registered, that scan is done for that user.

A pool can listen to a user's network entry set, and when an entry is added to a new user's identity-set, then if there is a pool reservation for that network entry, tokens are given.



Sets of associated-networks (the full set or something filtered) can be traded on the marketplace

Network Discovery is a layer that searches a network for user friends and adds them to their associated-network

# Network entities can be assigned tokens

There is a set for this network entity called the possession-set, that tokens and pools can be added to. But the ownership of the tokens is not changed until the network entity is resolved to a user.
Each network entity can have many possession sets and these sets can have expiration dates or other bounds set on them to be released at

Tokens in a possession set here cannot be sold because there is an attribute that prevents this from being added to any lot set

