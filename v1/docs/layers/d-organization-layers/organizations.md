# Organizations

Organization is a special user, that represents group of users who have shares. All actions of this special user must be voted on.

The majority of shares voting for something wins.

The organization has a shared wallet, that each owner has a percentage of. A vote is required to do anything with the wallet contents, or part of the contents.
Including transferring tokens of that wallet to the users.

Many things can be automated to be kept on doing, again and again, once a vote is made. Another vote is required to stop the automated thing.

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

Organizations can do polls 

Polls can be made automatic, when they close by all answering or after a set time, to do what the majority of shares wants.

Any owner can set up the organization to do anything, but that is put into a voting queue first, then acted on automatically after the vote succeeds.

This queue is done via the deferred action attribute on the user of the organization, see deferred actions in the user section.
Here, the permissions are set so that nobody can set this to be off. So, everything the organization does is put into the deferred queue until 
the deferred-action-job attribute for the job is made. 


The permission for the org are set so that the only way for that deferred attribute to be set, is when a vote attribute is set for the job, which is done via the polling result 