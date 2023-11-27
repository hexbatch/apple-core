# Network discovery

Is an api that can scan a specified network and generate new network entry tokens that are owned by the user doing this call.

* If a network entry is already made, then a new token is made from the token-type, and the user calling this api owns the token
* If this is a new network entry, then a new token type is made, and the user has a token made from that

The  token put into his own associated-network

# Scanning

This api has plugins that know how to scan for friends and connections for a social network

so there would be a plugin for facebook, masterdon, reddit, etc


# Reservations

Pool stubs help give out tokens to people who are not users yet on this instance.
One way to do this is to use the networks, and any stub assigned to a leaf on that network will be converted
to tokens for that user when they sign up and that subnetwork is given to them.

The user gets the tokens in the reservation.