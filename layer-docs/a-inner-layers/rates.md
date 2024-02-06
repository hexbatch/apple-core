# Rates

Rates are sets that allow api calls.

The bearer of a set can use the api

All layer api are also represented as element types.

Can create an element inheriting from one or more of these, each inherited allows this element to decide if the api call can be made.

Elements from these are owned by a user, and these elements can have a custom event that will respond to "can api call be used" event
Scripts in these actions can remember usage counts, by incrementing a counter each time they allow yes, when the usage count reaches limit, then the element can no longer say yes to the api call


These elements are created and set by the server giving it, and cannot be used outside that server.
However, these elements can be traded between servers so the bearer can use it for server A or server B (server provide rate set in trade),
Also, these sets can be used by proxies.

Rate sets can be split by the user though, and the elements given to others. 

it's just the elements that cannot be modified other than the ownership. Once an element is used up, it can be destroyed. There is really no way to recharge it

A rate set can have multiple elements for the same api call.

* Rate sets can be used by more than one user, this is recorded in the layers only in this rate api
* Stores rate data in a fast lookup, but layers still passes the rate set to the core for adjustment
* An agent can have different rates for each user they represent.

Rates are changed by admins. (unless no admin layer, then rates are changed by anyone on local ip)


## create rates

## adjust rates

## destroy rates
