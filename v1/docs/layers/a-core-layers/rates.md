# Rates

Rates are sets that allow api calls.

The bearer of a set can use the api

All layer api are also represented as token types.

Can create a token inheriting from one or more of these, each inherited allows this token to decide if the api call can be made.

Tokens from these are owned by a user, and these tokens can have a custom event that will respond to "can api call be used" event
Scripts in these actions can remember usage counts, by incrementing a counter each time they allow yes, when the usage count reaches limit, then the token can no longer say yes to the api call


These tokens are created and set by the server giving it, and cannot be used outside that server.
However, these tokens can be traded between servers so the bearer can use it for server A or server B (server provide rate set in trade),
Also, these sets can be used by proxies.

Rate sets can be split by the user though, and the tokens given to others. 

it's just the tokens that cannot be modified other than the ownership. Once a token is used up, it can be destroyed. There is really no way to recharge it

A rate set can have multiple tokens for the same api call.

* Rate sets can be used by more than one user, this is recorded in the layers only in this rate api
* Stores rate data in a fast lookup, but layers still passes the rate set to the core for adjustment
* An agent can have different rates for each user they represent.

Rates are changed by admins. (unless no admin layer, then rates are changed by anyone on local ip)


## create rates

## adjust rates

## destroy rates