# Contracts

# (changelist todo or ponder about)
------------------------
Now using transactions to power this
Now using agreements too (because of transactions)

---------------------------------------------
---------------------------------------------

Deals with the selling, terms, and use of token types

Contracts is the ability to use a token type, owned by someone else, as a parent for new token types.

Contracts can also just be auto payments, to be cancelled by either party with or without penalty

* Can set up rates, terms, limits and costs
* Can set up how the costs are paid

I think contracts will use the marketplace in a automatic job and offer and acceptance when a new token is made,
or every N tokens, or when conditions are met. 

Basically it sets up an action to call the api and see if permission is given, and looking at the contract, to see if its time to do another auto marketplace


## subscriptions

Is the terms and conditions for doing the automatic job/offer/accept

Subscriptions have info and the api allows them to be listed and cancelled.

Subscriptions can be set or edited to be expired after N time, by either the buyer or user.
The buyer can choose to set an earlier date.

### Penalties

A contract can have penalties for early cancellation by either party. If a marketplace job and offer and sell cannot be created immediately, then the contract cannot be cancelled

### Arrears

Penalties can be done for arrears, these can stack up. When a user has new tokens then a watcher api set can automatically transfer owned tokens

The api can list a user's arrears

### Cancellation 

Contracts can be set up to be cancelled by seller, buyer, both or none. With or without penalties

### Selling of contracts

The seller of the contract can put up the contract via the selling api, contracts can be sold that are in arrears


## Auto transfer

Contracts can be set up to automatically transfer a percentage or set amount in a wallet to another user, using either a schedule or when the wallet has enough
(watcher api)