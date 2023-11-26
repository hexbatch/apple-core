# Organizations

Organization is a special user, that represents group of users who have shares. All actions of this special user must be voted on.
Any user who owns shares can log in as this special user to read anything. But cannot write or change anything.
This is done by having zero rates for any changing api calls for the organization itself.

Doing changes for this user, or making or changing resources, requires an agreement that has majority ownership winning.
The majority of shares voting for something wins.

Agreements can allow designating specific users to do specific future things without needing a vote. These future things can be limited to one time or repeat times.
Internally this is done by making the user an agent for the organization, and adjusting the rate api for the agent when it's being the org user.
Agreements can cancel any designation.

For example, if the owners want to make a transaction for the org wallet, then they vote on having one of them be an agent for that one transaction.

The organization has a shared wallet, that each owner has a percentage of. A vote is required to do anything with the wallet contents, or part of the contents.
Including transferring tokens of that wallet to the users.


## Shares

Any user can create an organization, the organization has a share token type, inherited from the new org, and a pool of shares of that type.

The number of share tokens owned by this user, combined with the number of shares remaining in the pool, is the total number of shares.

This initial owner can create a sub pool of these shares, and sell them on the marketplace. Any user who buys this now has shares.

Owners can agree to increase the number of shares.
Then there is a choice:
* Each current owner gets their percentage of new shares. 
* Or the shares are given to the organization, and any profit is put into the shared wallet 

People can buy and sell their own shares however they like.

## What can an organization do?

An organization can do anything a regular user can do.

* An organization can be the seller for the marketplace and sales
* An organization can also buy stuff
* There can be contracts to auto transfer profits via the ownership.
* But if there are auto-repeat contracts, then each time its renewed,
* if tokens are being transferred using a ratio of shares, that ratio is recalculated 

# Voting

Organizations do agreements to decide on everything needed to be done. The org user itself is always part of the agreement but has zero weight for its vote.

An organization ties something to be done to these agreements, and can decide how often to repeat this without needing extra votes

Any owner can set up the organization to do anything, but that is put into the agreement

Decisions can be acted on automatically after the vote succeeds. This is done via the deferred layer.
Or the agreement allows people to manually do the stuff, using the agreement.
The layers do not allow direct login to the user organization, but allows owners to do api actions using an agreement as the credentials
