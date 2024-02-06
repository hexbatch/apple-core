# Network discovery

Is an api that can scan a specified network and generate new network entry elements that are owned by the user doing this call.

* If a network entry is already made, then a new element is made from the element-type, and the user calling this api owns the element
* If this is a new network entry, then a new element type is made, and the user has an element made from that

The  element put into his own associated-network

# Scanning

This api has plugins that know how to scan for friends and connections for a social network

so there would be a plugin for facebook, masterdon, reddit, etc


# Reservations

Pool stubs help give out elements to people who are not users yet on this instance.
One way to do this is to use the networks, and any stub assigned to a leaf on that network will be converted
to elements for that user when they sign up and that subnetwork is given to them.

The user gets the elements in the reservation.
