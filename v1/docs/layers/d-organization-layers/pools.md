# Pools

Pools are a resource that will generate up to X tokens of the same token-type. But the owner can be different for each batch of tokens made

New pools can be made by the owner of the token type for no contract.

Or be created for a one time contract (contract can be free)

Have ability to regenerate market contract, once the pool limit has been reached.

## Batches

The owner of a pool can create a number of new tokens of the pool type for any user they pick. As long as there is enough potential tokes left, this can be done

## Reservations

It may be that a series of tokens for each user will be reserved for a set of network, when the network token has a user assigned, the user gets the tokens in the reservation.

The reservation does count towards the number of tokens used in a pool, even though the tokens have not been made yet.

Reservations can be re-absorbed after a certain time, if needed. This allows other reservations or batches to be made. 

## Sub Polls

A pool can be divided into one or more smaller pools, without changing the total unallocated tokens.
Each of these new pools are just a regular pool.

A new smaller pool still has the same contracts as the older pool, but new contracts can be added. 
This allows resale of pools without breaking older contracts.

A pool can be made to disallow reselling

A sub-pool can be combined back to its parent, destroying the sub-pool and increasing the parent total unallocated  