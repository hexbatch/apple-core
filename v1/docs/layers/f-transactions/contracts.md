# Contracts and Memberships

Api for selling inclusion in a user group for a period of time or permanently .
Sell or subscription for membership in a group.

Subscriptions can have penalties for early cancellation by either party.

Membership in a group also determine token creation rights.

Here can be offered to sell a membership to a group for a single time frame,
or a subscription that auto-renews 
* as long as can be paid for and is not cancelled.
    
Breakdown of a subscription or single sell:
* the transaction for the initial cost to move a token to a protected group.
  * this can be missing for no cost, but then no txn recording in auditing
  * If provided, then the txn should already be agreed on and optionally done
  * has the time this membership expires. If missing then its forever.
  
* The transaction for each subscription cost to keep from moving the token out of the group
  * must have a txn
  * must have an end time
  * At the end time, will try to do the re-subscription using that txn (unless limits to resubscribing)
    * txn failure will move the token out
    * agreement failure will move the token out (someone cancelled)

With subscriptions, can set up rates, terms, limits and costs
* Can set up how the costs are paid
* the costs can be based on number of tokens created, when moving the user to a type creation group.
* can set up how many renewals, or min renewals without penalty, then add a fail penalty
* Can set up auto transaction for each usage, paid before token created from type

The rates are then set up to be calculated by a js script that is generated from a script template.
And the script md5 is put into the agreement.

Re-subscriptions provide an unchangeable subscription cost until cancelled.
Can hook on agreements to this agreement's fail condition for penalties.

Setting a new transaction before the subscription period ends can be done automatically or manually.
If automatic, then will use a script to determine the cost (can md5 the script as part of the agreement)

Subscriptions are optional, and can be priced in any way.
If a subscription is missing, then the token will stay in the group for as long as the initial cost has set.

The moving the token into the user group can also include admin rights or not.


# Usages

## Membership sold in transactions

Membership offers can be sold in transactions,
and the transaction completing allows for the user to be an admin or member.


# Membership invites

An invitation is a membership set up to run when a person is given a selected token, or a pool stub is created to be a token  

When the invite is activated by the ownership or token creation, then the owner is the one given membership.
Invites need to have no up front costs.

A membership offered to bearer can also be made, whoever has a token can give (transaction) in exchange for membership.
Perhaps other tokens will also be required, that is up to whoever makes the invitation.

Can use the token's or stub's bounds and expiration, and permissions (only some users can use it).


The subscription template can be set up to generate new subscriptions when sold or ownership is given to a token.
Templates are complete membership deals, but the user who gets the template or who pays is not defined.
When a template has a new subscription made, then the user is picked.

Subscription templates can have descriptions and media attached.

## Contracts for pools

A contract can be made for a pool, and then the stubs created are treated like created tokens for that type
Once a stub is paid for, then the token it later creates is not subject to a contract.

Pools can be subcontracted out, and there is no limit to nesting of these contracts.
The older ones are done first, and all contracts have to transfer the needed tokens before the stub is created.

Pool templates can be made to give the contract to the user it is rendered for.
