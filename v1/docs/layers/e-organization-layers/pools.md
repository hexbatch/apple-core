# Pools

Pools can give anyone the ability to give out tokens before they are created.

Pools are a resource that will generate up to X tokens of the same token-type.
But pools generate stubs, not tokens.
The stub owner is anyone who possesses the stub.
The stub can be automatically or manually redeemed for a new token which the stub owner will now own.

A pool is created by the type owner or his admin, they can allocate it to themselves or give or sell it to anyone.
The pool owner and his admins are the only ones that can give out stubs from the pools they own.

Tokens created from a pool can be subject to a contract. The per token contract has to be completed before the stub
is released to be used or given.
Once the stub is allowed, then any token it makes after that is not based on any type contract.

## Stubs
A pool stub is the identifier given by the pool which can be created into a token.
Stubs themselves can be given an expiration date.
If a stub is not converted to a token after its expiration date, 
then that stub is now invalid and does not count towards any quota .

The expired stubs can be regenerated for further use without any attached contract, they are already paid for.



## Sub Pools

The owner of a pool can sell out subdivisions of his pool.
A pool can be divided into one or more smaller pools, without changing the total unallocated tokens.
Each of these new pools are just a regular pool.

A new smaller pool still has the same contracts as the older pool, but new contracts can be added. 
These newer contracts will be executed after the older contracts.
This allows resale of pools without breaking older contracts.
If any contract fails, then the stub is not created

A pool can be made to disallow reselling

A sub-pool can be combined back to its parent, destroying the sub-pool and increasing the parent total unallocated

