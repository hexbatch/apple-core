# Marketplace

Any transfer of token sets where ownership is swapped between the two parties. All is sold as is with no refunds.

For example an inventory token starts off as being owned by the organization, but then there is a swap between a set of token owned by the customer and the inventory token.


Flow:
* Set up a lot, owned by a user or group, to be bid on or automatically sold
* Offers can be made
* The lot owner or group member selects the winning offer, or this can be done automatically



There is no sales flow here, or buying rights to use future tokens, all sales are immediate and final when the lot owner accepts an offer


## Lots

What is offered for sale, lots can be created but not changed after the first bid on it is made, lots can have an expiring time or other bounds

Lots can have a set of type-groups any of which can be met to be the price. Or a lot may be made without a price and the owner selects a winning bid.
Type groups can be bounded, so that different prices can be set for different areas or times or bid contexts.
It could be, that in some times, locations or path contexts - that there is no price

Lots that have prices can accept the very first bid made, if there is a price for that bound, and automatically close the sale. 

Lots can be owned by a user or an organization.

## Offers

An offer is an attempt to buy the lot, for an offer to be created, it has to meet a price when its made.

If the owner considers or selects this in a bounds that turns off the price this offer was made on, that offer is still valid. 

An offer can contain text, media, contact details etc

### Auctions

When a lot is set for an auction, the seller cannot choose a winner until a certain time.

Auctions can be closed or open. If closed, the different bidders cannot see the other bids. If open, then anyone can see the bids.

* The marketplace offers some apis to do bids

## Award an offer

When the owner selects the winning offer, or if done automatically, all the tokens in the lot will be transferred to the winner, and the price transferred to the seller

## Compare operations

Checks to see which offers can accept which prices at the current time


## Free stuff to someone 

To just give tokens to someone else, no price required, then just set the requirements to an empty set, and set the first offer to be accepted, and make an empty offer at the same time, 
There is an api thing to make this simple
